---
title: Self-Hosting Diagrams.net (draw.io)
excerpt: Host your own instance of Diagrams.net, a free web-based flowchart and diagram making (Visio alternative) application.
categories:
- Containerization
- Self-Hosting
- Open Source
tags:
- docker
- tutorial
---
When it comes to making flowcharts and diagrams [Visio](https://www.microsoft.com/en-us/microsoft-365/visio/flowchart-software) is probably one of the more well known applications out there. Throw in the fact that is has a both a web and desktop application and integrates into most Office 365 services and you have a pretty robust tool. The downside though would be the fact that pricing starts out at $5.00 USD a month for each user, and that only gets you a limited, web based version.

So if you are looking for a solid flowchart and diagraming tool and don't have need to "integrate" with Office 365 then [Diagrams.net](https://diagrams.net). Diagrams.net (formally known as Draw.io) is a powerful Visio alternative. It come with:
- both a web app and a desktop app
- collaboration features
- integration with a number of storage systems (Gitlab, OneDrive, Google, etc)
- a large number of integrations and add-ons for 3rd party applications
- and can be self-hosted

# Requirements
- [Docker](https://docs.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/) (optional, but this guide uses it)
- [Diagrams.Net Docker Image](https://hub.docker.com/r/jgraph/drawio)

# Install Diagrams.Net in Docker
1.  Create a new folder for your docker container. I typically do this for every container I create to house my docker-compose files, container volumes, etc. 

2.  If you are using Docker Compose then create a new *docker-compose.yaml* file and copy-and-paste the following

    ```yaml
    #This compose file adds diagrams.net (ex draw.io) to your stack
    version: '3.5'
    services:
    drawio:
        image: jgraph/drawio
        container_name: drawio
        restart: unless-stopped
        ports:
        - 9080:8080
        - 9443:8443
        environment:
        PUBLIC_DNS: domain
        ORGANISATION_UNIT: unit
        ORGANISATION: org
        CITY: city
        STATE: state
        COUNTRY_CODE: country
        healthcheck:
        test: ["CMD-SHELL", "curl -f http://localhost:8080 || exit 1"]
        interval: 1m30s
        timeout: 10s
        retries: 5
        start_period: 10s
    ```
    You will need to change a few parts of your *docker-compose.yaml* file as follows
    ## Ports

    ```yaml
    ports:
        - 9080:8080
        - 9443:8443
    ```
    Docker defines ports as **EXTERNAL:INTERNAL**. So in our case you would add "9080" to the end of your docker server ip to access the diagrams.net web app

    ```
    https://your-docker-server:9080
    ```
    The **EXTERNAL** port needs to be a open, unused port on your docker server. You will leave the **INTERNAL** port alone as that is the port the application uses (docker will take care of mapping all incoming traffic on the **EXTERNAL** port to the **INTERNAL** port for you). You will need to update each **EXTERNAL** port listed.

    ## Environment Variables

    ```yaml
    environment:
        PUBLIC_DNS: domain
        ORGANISATION_UNIT: unit
        ORGANISATION: org
        CITY: city
        STATE: state
        COUNTRY_CODE: country
    ```
    Environmental variables are variable passed into the docker application from the outside. The variables replace "placeholders" in the config files for diagrams.net. These variables deal with creating a SSL cert with Lets Encrypt. I left them as-is for the most part since I generate my own SSL certs. If you want to learn more about them, you can check out the documentation [here](https://hub.docker.com/r/jgraph/drawio)

3. Run the following command `docker-compose up -d`

{% capture notice-1 %}
#### Not Using Docker Compose
If you are not using Docker Compose then the command to run your container would be as follows

```bash
docker run -it --rm --name="draw" -p 9080:8080 -p 9443:8443 jgraph/drawio
```
{% endcapture %}
<div class="notice--info">{{ notice-1 | markdownify }}</div>

Open a browser windows and enter `http://your-docker-server-ip:9080`. If successful you should see the following
{% include figure image_path="/assets/images/2022/drawio-01.png" alt="this is a placeholder image"%}

Once the loading screen completes you will see the following screen which lets you pick if you want to save your drawings to either your device or in the browser.
![drawio-02](/assets/images/2022/drawio-02.png)

In an upcoming article we will go over linking to [GiLabs](https://gitlab.com) so you can store your images directly in GitLab.