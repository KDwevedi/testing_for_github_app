# C4GT Community Support App LLD

# Introduction
## About 
This document describes the backend for the [﻿C4GT Community Support App](https://github.com/apps/c4gt-community-support/).
It is primarily an event driven application based around [﻿Github Webhooks](https://docs.github.com/en/webhooks/webhook-events-and-payloads) received via a [﻿Github App Installation](https://docs.github.com/en/apps/creating-github-apps/registering-a-github-app/using-webhooks-with-github-apps).

This document aims to anchor the future development of this application into a scalable and modular architecture.

## Problem Statement
[﻿Code for Govtech](https://codeforgovtech.in/) is an ecosystem initiative to foster a community of [﻿open source](https://opensource.com/resources/what-open-source) contributors to tech in the [﻿digital public goods](https://digitalpublicgoods.net/about/) ecosystem.

For us, Github is the platform of choice to anchor this community building effort. 

The [﻿C4GT Community Support Github App](https://github.com/apps/c4gt-community-support/) enables us to interact with activities on select github repositories belonging to [﻿participating organisations](https://github.com/Code4GovTech/C4GT/wiki/How-to-participate-as-an-organisation) in the C4GT initiative.

[﻿Installing](https://docs.github.com/en/apps/using-github-apps/installing-a-github-app-from-a-third-party) the app allows us [﻿consented](https://docs.github.com/en/apps/using-github-apps/authorizing-github-apps) [﻿and](https://docs.github.com/en/apps/using-github-apps/approving-updated-permissions-for-a-github-app) [﻿transparent](https://docs.github.com/en/apps/using-github-apps/reviewing-and-revoking-authorization-of-github-apps) access to event-driven [﻿webhook payloads](https://docs.github.com/en/webhooks/webhook-events-and-payloads)﻿ pertaining to these select repositories and enable features such as:

- [﻿Listing C4GT Tickets](https://www.codeforgovtech.in/community-program-projects)﻿
- Awarding [﻿points](https://github.com/Code4GovTech/C4GT/wiki/Point-System-for-Contributors) for contributions
- ...

The objective is to design a modular, configurable and scalable architecture for these functions.

# System Overview
## Architecture Type
The application is designed as an event-driven app with:

- **Event Producers**: These are (in this case, external) systems that create and publish events.
    - Github Webhook Events
    - Discord Bot (Registrations)
- **Event Subscriber Module:** Listens to and authenticates events. Passes events to relevant modules to drive appropriate actions.
    - Listener Module
- **Event Consumer Modules:** Modules tailored to consuming entity-specific events and driving relevant actions. These are called by the event subscriber module
    - Issues Events Consumer
    - Pull Requests Events Consumer
    - ...
- **Data Models:** Classes modeled after event related entities. Relevant for data validation and .
    - Issue
    - Pull Request
    - Issue Comment
    - App Installation
    - ...
- **Helper Classes:** Primarily used to call database and github apis
## Tech Stack
**Github App Server:**
- [Quart](https://pgjones.gitlab.io/quart/) as the primary web framework
- [aiohttp](https://docs.aiohttp.org/en/stable/) for async http requests
- [Supabase Python Client](https://supabase.com/docs/reference/python/introduction) as the database interface
- Github API:
  - [REST](https://docs.github.com/en/rest?apiVersion=2022-11-28)
  - [GraphQL](https://docs.github.com/en/graphql)
  - [Webhooks](https://docs.github.com/en/webhooks)
**Database:**
[Supabase](https://supabase.com/docs)


