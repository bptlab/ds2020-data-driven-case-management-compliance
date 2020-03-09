# Checking Compliance in Data-Driven Case Management

Case management approaches address the special requirements of knowledge workers.
In fragment-based case management (fCM), small structured parts are modelled and loosely coupled through data dependencies, which can be freely combined at run-time. 
When executing business processes, organizations must adhere to regulations, to laws, to company guidelines etc.
Business process compliance comprises methods to verify designed and executed business processes against certain rules.
While design-time compliance checking works well for structured process models, flexible knowledge-intensive processes have been rarely considered despite increasing interest in academia and industry.

In this paper, we present (i) formal execution semantics of fCM models using Petri nets.
We also cover concurrently running fragment instances and case termination.
We (ii) apply model checking to investigate the compliance with temporal logic rules; finally, we (iii) provide an implementation based on the open-source case modeler Gryphon and the free model checker LoLA.

## Screencast

<video src="bpm2019ws-fcm-compliance.webm" controls preload>
<a href="bpm2019ws-fcm-compliance.webm">Click here</a> to download the screencast.
</video>

## How to run it yourself

The compliance-enabled fCM system consists of three components:

* [Gryphon](https://github.com/bptlab/gryphon), a web-based fCM modeller. Use the **compliance** branch.
* [Chimera](https://github.com/bptlab/chimera), an execution engine for fCM. Use the **compliance** branch.
* [LoLA webservice](https://github.com/bptlab/lola-webservice), a web service wrapper for LoLA.

Ideally, the components are used together via [Docker Compose](https://docs.docker.com/compose/):

* Clone the three repositories locally to a new folder.
* Check out Gryphon's **compliance** branch.
* Check out Chimera's **compliance** branch.
* Build the Gryphon image: `docker build -t bptlab/gryphon:dev gryphon/`
* Build the Chimera image: `cd chimera && make build_docker && cd ..`
* Download the LoLA webservice image: `docker-compose -f lola-webservice/docker-compose.yml pull`
* Start all three components: `docker-compose -f chimera/docker-compose.yml -f gryphon/docker-compose.yml -f lola-webservice/docker-compose.yml up -d gryphon database lola-webservice chimera`
* Navigate to `http://localhost:3000` to access Gryphon.
* Stop all three components: `docker-compose -f chimera/docker-compose.yml -f gryphon/docker-compose.yml -f lola-webservice/docker-compose.yml down --remove-orphans`

In order to check compliance, the case model must be deployed to Chimera.

## The example case model

The example [Emergency case model](Emergency.json) can be downloaded and imported into Gryphon.