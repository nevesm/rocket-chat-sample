# rocket-chat-sample
Sample diagram to illustrate how to achieve the SLA, SLO and Availability requirements of rocket.chat


## Introduction
The company provided us a blank AWS account to setup the environment with one condition, we must use kubernetes.
We fired up the environment with two subnets, one private that will hold all of our backend, database and private connectivity components, and one public, that will hold our API Gateways and VPC Links.

## The architecture
In this example, we are using a microservice architecture, the applications are hosted in kubernetes, as well as the observability components, including the [**OpenTelemetry collector**](https://opentelemetry.io/docs/concepts/components/#collector), [**Prometheus**](https://prometheus.io/) and [**Grafana**](https://grafana.com/).

The databases and cache layer are hosted in the same private subnet as the applications, so it can be accessible without problems and without exposure to the internet.

- We've implemented: 
    - A application responsible for the payments, its a simple API with a database
    - A application responsible for the real-time interaction, chat messages and more, its a websocket application.
    - A application for searching historical messages, this can be heavy for the database, so we have a cache layer and isolated this small function into a single application.


## How we meet the requirements
Since we have all the applications instrumented by OpenTelemetry, we can simple monitor these, create dashboards, create alarms and even configure custom events in the applications for some key data like: UserSubscriptionEvent, UserAddedEvent, PaymentEvent and much more.

## Diagram
![](/rocket-chat-diagram.png)
