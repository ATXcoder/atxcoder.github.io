---
Title: School Morning Automation
excerpt: "A nice detail screen and automation to keep us all on track on school mornings"
toc: true
category: Home Assistant
tags:
- automation
- dashboard
---

I am not a morning person and doing anything that requires any real cognitive skills is typically out of the question (my brain doesn't turn on until I have had my coffee). Unfortunately, my wife and I are up in the mornings getting our three kids up and off to school. This typically means:

- Keeping track of how long before the bus arrives
- Checking the weather for the day to see if they need a jacket, umbrella, etc.
- Being aware of any events that the kids have for school (practices, pep rallies, etc.)

Because this information is constantly changing, hanging a simple checklist by the door will not work (nor is it considered "decoration" by the wife). So I needed to find a way to gather all this information in a single location and automate as much of it as I could. Enter Home Assistant.

## Requirements
As I mentioned, several things we need to be aware of in the mornings change each day like the weather and kid's events. I also needed some way for everyone in the family to be able to see all this information. So I sat down and listed out all the requirements and came up with the following:
- A countdown displaying the amount of time remaining before the school bus arrives
- A listing of any events happening at the kid's school for the day
- An overview of the day's weather forecast
- Finally, a display for all this information that is easily viewable by everyone

## Countdown timer
The bus arrives pretty consistently at 6:23 every morning (maybe a minute or two later, but never earlier than that). Since I knew the bus arrival time I just needed to pick a start time, subtract that from the bus arrival time, and that would get me my *time until the bus arrives* countdown. I already had an [Input DateTime](https://www.home-assistant.io/integrations/input_datetime/) control that I used as a trigger for some wake-up automations that allowed me to set a wake-up time from the UI. 

{% highlight yaml %}
{% raw %}
time_to_bus:
      value_template: "{{(as_timestamp(strptime(states('input_datetime.bus_arrival'),'%H:%M:00'))-as_timestamp(now().strftime('1900-01-01 %H:%M:00')))|int/60}}"
{% endraw %}
{% endhighlight %}

## Displaying the information
This requirement was pretty easy as we already have a wall-mounted tablet in the living room. It was easily accessible and in a high-traffic area guaranteeing that everyone would see it in the mornings.

Since I use [UI Lovelace Minimalist](https://ui-lovelace-minimalist.github.io/UI/) to create my dashboards, the following YAML code gave me a nice school morning dashboard

{% highlight yaml linenos %}
{% raw %}
  - title: "School"
    path: "school"
    type: custom:grid-layout
    layout:
      grid-template-columns: 20% 20% 20%
      grid-template-rows: auto
      
    cards:
      - type: custom:bignumber-card
        view_layout:
          grid-area: 1/1/ span 1/ span 4
        entity: sensor.time_state
        scale: 60px
        style: '#4287f5'
      
      - type: picture
        image: /local/img/bus.svg
        view_layout:
          grid-area: 2/1/ span 1/ span 1
        card_mod:
        style: |
          img {
            height: 100%;
      
      - type: custom:bignumber-card
        view_layout:
          grid-area: 2/2/ span 1/ span 3
        entity: sensor.time_to_bus
        title: Minutes until Bus Arrives
        scale: 60px
        style: '#4287f5'

      - type: custom:simple-weather-card
        view_layout:
          grid-area: 3/1/ span 1/ span 3
        entity: weather.k3t5_hourly
        name: " "
        backdrop: true
      
      - type: custom:atomic-calendar-revive
        view_layout:
          grid-area: 3/4/ span 2/ span 1
        entities:
          - calendar.kids_school
        name: Kids School Calendar
        enableModeChange: true
        firstDayOfWeek: 1
        maxDaysToShow: 1
        sortByStartTime: true
{% endraw %}
{% endhighlight %}

which gives me a dashboard that looks like this

![school-dashboard](/assets/images/dashboard-school.png)

## Automation
The final piece was creating some automations to:
 - Change the display from the home dashboard to the school bus dashboard
 - Provide audible alerts at 15 and 5 minutes before it was time to leave for the bus, as well as a "time to leave for the bus" alert

### Change display dashboard
The first automation ensures the dashboard changes from the standard home dashboard to the one I created for the school bus countdown. The YAML code is a little long, so I'll break it down bit-by-bit.

The automation triggers when the current time equals `input_datetime.wake_up_time`. Conditions then check to make sure it is a weekday and not a school holiday. 

{% highlight yaml linenos %}
{% raw %}
- id: '1619494346459'
  alias: School Wakeup
  description: Morning automation for a school day
  trigger:
  - platform: time
    at: input_datetime.wake_up_time
  condition:
  - condition: state
    entity_id: binary_sensor.workday_sensor
    state: 'on'
  - condition: state
    entity_id: calendar.school_holidays
    state: 'off'
{% endraw %}
{% endhighlight %}

Actions then run that turn on several lights in the house.

{% highlight yaml linenos %}
{% raw %}
action:
  - service: fully_kiosk.load_url
    data:
      url: http://10.0.10.9:8123/desktop-dashboard/school
    target:
      device_id: 17e783f5c55accf9ffe7b12c836bf0cf
  - service: light.turn_on
    target:
      entity_id: light.front_porch_light
    data: {}
  - service: light.turn_on
    target:
      entity_id: light.thomas_nightstand
    data:
      brightness_pct: 5
  - service: light.turn_on
    target:
      entity_id: light.living_room_lamp
    data:
      brightness_pct: 70
  - service: light.turn_on
    target:
      entity_id: light.dinning_room_lights
    data:
      brightness_pct: 25
{% endraw %}
{% endhighlight %}

Last, we wait 1 hour and 20 minutes after the last light turned on to start turning the lights back off. This is because the lights turn on roughly 1 hour before the bus arrives and the extra 20 minutes give my wife and I time to make coffee and get settled. Also, the sun is usually up by this time.

{% highlight yaml linenos %}
{% raw %}
 - delay:
      hours: 1
      minutes: 20
      seconds: 0
      milliseconds: 0
  - service: light.turn_off
    target:
      entity_id:
      - light.thomas_nightstand
      - light.front_porch_light
    data: {}
  - service: fully_kiosk.load_url
    data:
      url: http://10.0.10.9:8123/desktop-dashboard/home
    target:
      device_id: 17e783f5c55accf9ffe7b12c836bf0cf
  - wait_for_trigger:
    - platform: time
      at: 07:30:00
    timeout: 02:00:00
  - service: light.turn_off
    target:
      entity_id: light.living_room_lamp
    data: {}
  mode: single
{% endraw %}
{% endhighlight %}

### School bus arrival

The next automation provides us with audible alerts about the school bus arriving. First, we trigger by checking to see if the current time is 15 minutes before the "bus arrival" time. Then in our trigger conditions, we make sure it is a workday (basically a weekday) and the calendar in Home Assistant that tracks the kids' school holidays is in a *off* state

{% highlight yaml linenos %}
{% raw %}
- id: '1614743327502'
  alias: School Bus Arriving
  description: Announce the bus will be arriving in 15 minutes. Triggers 15 minutes
    before "Bus Arrival" time (input_datetime.bus_arrival). It then waits 10 minutes
    and announces the bus will be arriving in 5 minutes and what the current temperature
    is outside or if there are any calendar events.
  trigger:
  - platform: template
    value_template: '{% set time_now = as_timestamp(states(''sensor.date_time'').replace('','',
      '''')) %} {% set bus_today = state_attr(''input_datetime.bus_arrival'',''timestamp'')
      + (as_timestamp(states(''sensor.date''))-15*60) %}  {{time_now == bus_today}}'
  condition:
  - condition: state
    entity_id: binary_sensor.workday_sensor
    state: 'on'
  - condition: state
    entity_id: calendar.school_holidays
    state: 'off'
{% endraw %}
{% endhighlight %}

Next we move into the actions. First we set the volume high on the speakers we will be using for auditory alerts

{% highlight yaml linenos %}
{% raw %}
- service: media_player.volume_set
    data:
      volume_level: 1
    target:
      entity_id:
      - media_player.kitchen_speaker
      - media_player.tristian_bedroom
{% endraw %}
{% endhighlight %}

Then we speak that the school bus will be arriving in 15 minutes and then delay for 10 minutes.

{% highlight yaml linenos %}
{% raw %}
- service: tts.cloud_say
    data:
      entity_id: media_player.kitchen_speaker, media_player.master_bedroom_clock,
        media_player.tristian_bedroom
      message: Attention, the school bus will be arriving in 15 minutes.
      cache: false
- delay:
      hours: 0
      minutes: 10
      seconds: 0
      milliseconds: 0
{% endraw %}
{% endhighlight %}

After the 10-minute delay, we check to see if the calendar that holds all our kids' school events has anything for today. If so we alert that the bus will be arriving in 5 minutes and to check the kid's school calendar for events happening today. If not, we alert that the bus will be arriving in 5 minutes and states the current temperature outside.

{% highlight yaml linenos %}
{% raw %}
  - choose:
    - conditions:
      - condition: state
        entity_id: calendar.kids_school
        state: 'on'
      sequence:
      - service: tts.cloud_say
        data:
          cache: false
          entity_id: media_player.kitchen_speaker, media_player.master_bedroom_clock,media_player.tristian_bedroom
          message: The school bus will be arriving in 5 minutes. Please review kids
            school calendar for events occurring today.
    - conditions:
      - condition: state
        entity_id: calendar.kids_school
        state: 'off'
      sequence:
      - service: tts.cloud_say
        data:
          entity_id: media_player.kitchen_speaker, media_player.master_bedroom_clock,
            media_player.tristian_bedroom
          message: Attention, the school bus will be arriving in 5 minutes. It is
            currently {{states('sensor.weather_temperature')}} degrees outside.
    default: []
{% endraw %}
{% endhighlight %}

The next action it to delay for 5 minutes and then announce that it is time to leave for the school bus

{% highlight yaml linenos %}
{% raw %}
- delay:
      hours: 0
      minutes: 5
      seconds: 0
      milliseconds: 0
  - service: tts.cloud_say
    data:
      cache: false
      entity_id: media_player.kitchen_speaker, media_player.master_bedroom_clock,media_player.tristian_bedroom
      message: It is now time to leave for the school bus.
{% endraw %}
{% endhighlight %}

Finally, we wait 30 seconds (to make sure everything is done playing) and lower the volume on the speakers to 70%

{% highlight yaml linenos %}
{% raw %}
- delay:
      hours: 0
      minutes: 0
      seconds: 30
      milliseconds: 0
- service: media_player.volume_set
    data:
      volume_level: 0.7
    target:
      entity_id:
      - media_player.kitchen_speaker
      - media_player.master_bedroom_clock
      - media_player.tristian_bedroom
  mode: single
{% endraw %}
{% endhighlight %}