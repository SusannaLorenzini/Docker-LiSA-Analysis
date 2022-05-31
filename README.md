# Docker for LiSA Analysis 
You can use LiSA Analysis, without having PHP 8 and Java 11 installed in your computer, by using Docker.  

## Requirements
- Docker.

<br>
   
## Installation with git
Follow these steps to build docker image and to start containers that will allow you to use LiSA Analysis in your local browser.
<br><br>
***NB***: if you don't have git installed follow steps from 1 to 3 of paragraph [*Installation without git*](#install_no_git) and then come back here to finish with steps from 4 to 6.  

Use your local shell:


### 1. Clone this repository
This repository contains files to build a docker image that will be used to run LiSA Analysis container. The folder *lisa-analysis* that will be created will be your working directory.  

```
	git clone https://github.com/SusannaLorenzini/Docker-LiSA-Analysis lisa-analysis
```


### 2. Enter lisa-analysis folder
Enter the folder that you just created. At the moment it contains this repository's files.

```
	cd lisa-analysis
```

### 3. Clone LiSA Analysis repository 
LiSA Analysis repository contains the source code that will be run from the docker container. 

```
	git clone https://github.com/SusannaLorenzini/LiSA-WEB src
```
***Important***: do not change the name "src", it is used by docker-compose file and by the container itself.

<a name="step-4-6"></a>
### 4. Build the docker image
Use *docker-compose build* to build two docker images: the first for alpine with PHP 8 and Java 11; the second for nginx web server.  
The main files used to build the two images are docker-compose.yml and dockerfile (in config/dockerfile).


```
	docker-compose build
```
***NB***: be sure to run this command from the folder lisa-analysis, which contains the docker-compose.yml file.

### 5. Run the docker container
Run the two docker containers in detached mode (in background), that are based on docker images that you just built. The following command will run both according to instructions contained in docker-compose.yml.

```
	docker-compose up -d
```
***NB***: be sure to run this command from the folder lisa-analysis, which contains docker-compose.yml file.

After running this command a local network will be created, it will be used by the two containers to communicate. You can check the presence of the network (called *lisa-analysis_network*) with ***docker network ls***.    

You can ensure that the two containers are running with ***docker ps***. They are called: *lisa-analysis_container* that is the container where source code of LiSA Analysis is placed and where PHP 8 and Java 11 are installed; *nginx_container* that is the container of the webserver.    

You can also check the presence of the two docker images that we created with ***docker image ls***. 

### 6. Open the browser at localhost:80
Now everything is good to go. You can open your browser at localhost:80 and you can use LiSA Analysis.  

   
<br>  


## <a name="install_no_git"></a>Installation without git (steps 1-3) 
If you don't have git installed follow the next steps 1-3 and then go back to complete with steps 4-6:

### 1. Download this repository
Enter the [home page](https://github.com/SusannaLorenzini/Docker-LiSA-Analysis) of this repository and click on the green <span style="color:green">***Code*** </span>button and select *Download ZIP* from the menu.  
Unzip the folder and place it where you want to have your working directory. 

***Rename the folder*** from *Docker-LiSA-Analysis-main* to *lisa-analysis*.

### 2. Download LiSA Analysis repository 
Enter LiSA-WEB repository's [home page](https://github.com/SusannaLorenzini/LiSA-WEB) and click on the green <span style="color:green">***Code*** </span>button and select *Download ZIP* from the menu.  

Unzip the folder and ***rename it*** from *LiSA-WEB-main* to *src*.     
***Important***: do not change the name "src", it is used by docker-compose file and by the container itself.

### 3. Place src into lisa-analysis folder
Place *src* folder into *lisa-analysis* folder.


### Follow steps from 4 to 6
Open your local terminal in *lisa-analysis* folder. Now you can follow [remaining steps](#step-4-6). 

<br>

## Info

* ***src*** is a ***shared folder*** between your computer and the container.  
⚠️ ***If you modify the src folder in your computer, it will be modified also in the container!***  
This allows you to:
	* Access to analysis results directly from the folder src/analysis/
	* Modify the source code of LiSA Analysis as you like
* Docker will map the port 80 of you computer to the port 80 of LiSA Analysis container. This allows you to use LiSA Analysis from localhost (localhost:80) of your browser.

<br>
   
## Additional commands
There are a few more docker commands that can be useful.

### Interact with the shell of LiSA Analysis container
You can interact with the shell of the container that contains LiSA Analysis and its dependencies by writing the following command:

```
	docker exec -it lisa-analysis_container /bin/ash
```
Now you're inside the container!   

You can navigate it using **Linux shell commands**. For example, you can use the command *ls* to see what's inside a folder and you can use *cd* to move from folder to folder.  
You can check PHP version by using *php -v* and Java version with *java -version*.  
  
When you want to exit the container and go back to your computer just type ***exit*** and hit enter. 

### Stop containers
You can stop both containers with one command. Place in the folder lisa-analysis and use the following command.

```
	docker-compose stop
```
If you open the browser and refresh the page you can see that LiSA Analysis is turned off. 

### Start containers 
Don't worry, you can start LiSA Analysis again! Place in the folder lisa-analysis and start the two containers again as follows.

```
	docker-compose start
```
Now you can use LiSA Analysis again in your browser at localhost:80.  

   
<br>  
   

## General docker commands

### Images
As mentioned before, you can use ***docker image ls*** to see images downloaded in your local docker.

### Containers
You can see which containers are currently running with ***docker ps***  and you can use ***docker ps -a*** to see all containers, also the stopped ones.  
These commands will show the two containers individually.

### Docker-compose containers
You can also see docker-compose containers running with ***docker-compose ls*** and you can also see docker-compose containers that are stopped with ***docker-compose ls -a***.  
This will show the two containers of LiSA Analysis grouped in one line.


