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

## API design guidelines

API design has Saga as cornerstone of data storage and journaling the data on in-game
date. 

### Entity
An entity is an object stored in the API. It contains properties, and allows creation
of a snapshotp of data on it. 
- Properties may be links to other entities creating dependency between owner and linked.
- Non-entity properties are identified by the GUID of the ownning entity.
- The properties are separated into a safely changeable fluff properties, and guarded properties.
  - Guarded properties with links are guarded against changes of the past altering future of
    other entities.
  - Guarded properties without links can be safely altered like unguarded properties.
  - Forced changes on linked guarded properties creates a new copy of the entity with a new GUID.
- Creating a copy of an entity creates a new branch linking the state copypied to the new entity.
  - Enties with copies thus are always Guarded with links. 

### GUID - Global Uniqued Identifiers
The API uses UUIDv4 for GUIDs of all stored entities.

### The difference between plan and past
All entities support planning, and planning does not create links nor prohibit changes on present or
past. Plan can be executed creating entity changes according to the planned change. 
- An executed plan becomes part of the past.
- Invalidated plan entities are just removed. 

### The base storage of all data is Saga
The saga is the base storage of all data. 
