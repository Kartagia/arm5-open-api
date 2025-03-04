# arm5-open-api
The Ars Magica Open License API repository for Open License content entities. 

## Introduction

As Atlas Games have announced Ars Magica Open License, this project became feasible.
The goal is to create an API allowing storing Sagas, Tribunals, Covenants, and Personae,
and everything linked to them for everyone to use.

The authors of the books may use the API to maintain details of their product in the API, a
API tries to ensure consistency of the content. It would react to any changes invalidating
other content stored, telling author which previous details requires checking or altering. 

The players, story guides, and troupes can maintain their saga records with similar automatic
checking for contradictions, and allowing them to plan, and execute events in the game. 

## Installation

The API specifications are not installed. 


## Generating your own API implementation from API

There is several tools allowing creation a new API.

### Azure installation with Kiota

[Download and install Kiota](https://learn.microsoft.com/en-us/openapi/kiota/install?tabs=bash) according to [Kiota documentation](https://learn.microsoft.com/en-us/openapi/kiota/overview).


#### Python

Run generation script for Python project.
```bash
kiota -d "openapi/openapi.yaml" -l Python
```

Create a Python Virtual Environment at output directory using Python3.
```bash
cd output && python3 -m venv .venv
```

To activate hte environment, give following command on the "output" directory.
```bash
source .venv/bin/activate
```

Produces Python API implementation for Azure into "output"-directory, and creates
virtual environment for installation of the packages. 
- The user may move the result into any directory.
- The user must then follow Kiota suggestions for additional downloaded libraries
  after activating the environment with pip.
