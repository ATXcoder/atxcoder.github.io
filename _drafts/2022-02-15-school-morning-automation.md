---
Title: School Morning Automation
excerpt: "A nice detail screen and automation to keep us all on track on school mornings"
classes: wide
categories:
- home assistant
tags:
- automation
- dashboard
---
I am not a morning person and doing anything that requires any real cognitive skills is typically out of the question (my brain doesn't turn on until I have had my coffee). Unfortunately my wife and I are up in the mornings getting our three kids up and off to school. This typically means:

- Keeping track of how long before the bus arrives
- Checking the weather for the day to see if they need a jacket, umbrella, etc.
- Being aware of any events that the kids have for school (practices, pep rallies, etc.)

Because this information is constantly changing, hanging a simple check-list by the door will not work (nor is it considered "decoration" by the wife). So I needed to find a way to gather all this information in a single location and automate as much of it as I could. Enter Home Assistant.

# Requirements
As I mentioned, a number of things we need to be aware of in the mornings changes each day like the weather and kid's events. I also needed some way for everyone in the family to be able to see all this information. So I sat down and listed out all the requirements and came up with the following:
- A countdown displaying the amount of time remaining before the school bus arrives
- A listing of any events happening at the kid's school for the day
- A overview of the day's weather forecast
- Finally, a display for all this information that is easily viewable by everyone

## A countdown displaying the amount of time remaining before the school bus arrives
The bus arrives pretty consistently at 6:23 every morning (maybe a minute or two later, but never earlier then that). Since I knew the bus arrival time I just needed to pick a start time, subtract that from the bus arrival time, and that would get me my *time until the bus arrives* countdown. I already had a [Input DateTime](https://www.home-assistant.io/integrations/input_datetime/) control that I used as a trigger for some wake-up automations that allowed me to set a wak-up time from the UI. 

```yaml
{% raw %}
time_to_bus:
      value_template: "{{(as_timestamp(strptime(states('input_datetime.bus_arrival'),'%H:%M:00'))-as_timestamp(now().strftime('1900-01-01 %H:%M:00')))|int/60}}"
{% endraw %}
```


## Display for all this information
This requirement was pretty easy as we already have a wall mounted tablet in the living room. It was easily accessible and in a high-traffic area guaranteeing that everyone would see it in the mornings.