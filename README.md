# Assignment

This assignment is a take home test from Cribl. It consists of 4 hosts, agent, splitter, target_1 and target_2.
The agent will consume an input file and will forward it to the splitter where the data is distributed among target_1 and target_2.
Both targets will write the data into another file, events.log.

## My solution
As the splitter and the targets are running on the same port, it's better to run the 4 hosts in docker containers. 
To have each host running in a docker container separately, I have implemented a Dockerfile for each host so that they can have different configuration or commands, if any. I have then decided to use docker-compose to configure the ports and networks, also to run the hosts in the appropriate order that is Targets, Splitter, Agent.

Also, in my docker-compose file, I have added volumes to export each events.logs file from both targets hosts. By doing this, I will be able to carry out my tests using those files. The two exported files are events-target_1.log and events-target_2.log. 

The test folder consists of all test cases such as:
* Validates data received on Target hosts: I have validated if data received on the Target hosts are correct by checking if each lines in input file has been correctly propagated in both events_logs from both targets. For example, my test will check if line 1 in the input file exists in any of the events_log file.

* Validates files generated by Target hosts are not empty: This test case is checking if the target hosts is writing in the events.log file.

* Validates uniformity of data distribution between Target hosts: This test case validates if data has been distributed almost evenly between the two targets.

* Validates completeness of data on Target nodes: This test case checks if all the data has been sent to the 2 target hosts.

Once the tests are executed a report of the test result is generated in the mochawesome-report directory. It can be viewed as an html file or json file.

Please note that, I have added comments to my code to explain each line.

## Prerequisites
You should have the following installed:
* latest docker
* latest docker-compose
* Node.js v12+ and npm

## Installation

In the root directory install the dependencies by running:

```bash
npm i
```

## Running the application locally 
To run the application locally (on your machine), you should build each host image by running these commands from the root directory:

```bash
docker-compose build
```
Once the images are built, you can run the 4 hosts/docker containers:

```bash
docker-compose up
```
This command will run the images of the hosts in separate docker containers. Each host will have its own docker container. You will have the logs displayed in the console but you can run docker-compose in detach mode to hide the logs by running:

```bash
docker-compose up --detach
```
Once the containers are up and running, you can access each host on these ports:
* target_1:port 9996
* target_2:port 9998
* splitter:port 9999
* agent:port 3000

## Shutdown the application locally
Once the application is running on your local machine, you can shut it down by:

```bash
docker-compose down
```
This command will shut down all the hosts/docker containers.

## Run the tests
After all the steps above are successfully completed, you can now run the test by:

```bash
npm test
```

This command is added to the package.json file as a script to run the test.
```bash
"scripts": {
    "test": "mocha --reporter mochawesome"
  }
```
I have added a simple/basic script to run the test but other config or environment variables can be added to it in the future. Also, I have specified to have mochawesome as reporter for the test results.

## GitHub Actions
I have chosen to use Github actions as I have my code on Github already. 
In the workflow named "Assignment Test Workflow", there are two jobs, build and test.
* Build job - in the build process, each hosts are built in docker images
* Test job - in this process, the application is started and running and the tests are performed.

The action/CI will automatically be triggered whenever there is a push or pull request on the main branch but you can also trigger it manually by going to Actions on Github and selecting the workflow. Then click on Run Workflow, select the branch and click on run workflow.

Please note that one test is failing and the CI would fail but I've allowed failure.

## Test Results from Github Actions
You can view the test results in the artifacts of Github Actions workflow.