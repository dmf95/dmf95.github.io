---
category: Data Engineering
title: Public NHL data modeling
description: A data engineering journey towards modernizing NHL data
date: 2022-06-05
image: /images/datarena/hockey-analytics-meme.png
tags: [all-projects, data-engineering, python, singer, meltano, bigquery, dbt]
---
This is first of a series of posts that delves into exploring, organizing, and modeling on public Hockey (NHL) data. I am one of the two developers of this work alongside my colleague [Gavin He](https://github.com/gavh3). I will occasionally cross-post the cool work we do within our "organization" (called [the-data-base](https://the-data-base.github.io/)) here on fullstaxx.

> A modern application of data-engineering to enable data science on public Hockey (NHL) data for the purposes of learning & development

## Table of contents
* [Introduction](#introduction)
* [Architecture](#architecture)
* [Setup](#setup)
* [Resources](#resources)
* [Developer contact](#developer-contact)

## Introduction

The motivation behind this project was simple: make public hockey data available using modern technologies for the purposes of data-science & data-visualization. We wanted to be able to answer questions like...
* Which players are most likely to have a breakout season next year?
* Which draft prospects are most likely to succeed in the NHL?
* How many goals should we expect from elite players like Connor McDavid or Auston Matthews next season?
* Where on the ice are individual players most efficient with their shooting? 


## Architecture 

In order to get to this state of-course, a lot of data-engineering was necessary. Below is a visual representation of the project architecture.

![Miro project architecture](/images/datarena/hockey-project-architecture.png)


### Data extraction

Currently, we only have a single source of data: the NHL Stats API. The Github repo that we built to extract the data is called `tap-nhl`. It is a Singer tap for the NHL Stats API.

Built with the [Meltano Tap SDK](https://sdk.meltano.com) for Singer Taps.


Below is a flow diagram explaining how it works:

![Mermaid Plot](/images/datarena/hockey-analytics-mermaid.png)


Resources
* Repo: [tap-nhl](https://github.com/bicks-bapa-roob/dbt-nhl-breakouts)

### Data transformation & loading

All of this work is contained within a Github repo called `dbt-nhl-breakouts` and uses dbt to model our raw data. It contains the source code used to transform raw nhl data from the NHL Stats API into analysis-ready models. 

In other words, this is where the SQL magic happens using dbt. Ultimately, this work converts confusing raw data into:
  * Data analyst/scientist friendly datasets all within one data warehouse (BigQuery)
  * Well-documented tables, field definitions, and queries
  * Reliable data that is tested and validated before ever making it into production

Resources
* Repo: [dbt-nhl-breakouts](https://github.com/bicks-bapa-roob/dbt-nhl-breakouts)
* Documentation: [dbt generated documentation](https://bicks-bapa-roob.github.io/dbt-nhl-breakouts/#!/overview)

### Data science

Consider this section separate from the rest. Each question that we decide to answer of our newly modeled data will live in this bucket. For example, one of the projects that spawned from this was the [nhl-breakouts project](https://github.com/bicks-bapa-roob/nhl-breakouts)


## Resources
- Learn more about dbt [in the docs](https://docs.getdbt.com/docs/introduction)
- Check out [Discourse](https://discourse.getdbt.com/) for commonly asked questions and answers
- Join the [chat](https://community.getdbt.com/) on Slack for live discussions and support
- Find [dbt events](https://events.getdbt.com) near you
- Check out [the blog](https://blog.getdbt.com/) for the latest news on dbt's development and best practices

## Developer contact
* [@dmf95](https://github.com/dmf95)
* [@gavh3](https://github.com/gavh3)