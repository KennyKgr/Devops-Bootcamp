# Elite Corporations Project

## AIM: Build a lightweight Task Management API that can run in a Docker container without requiring a database. 

### setting up requirements for the task which will permit Employees

     Add
     View  
     Update
     Delete various Tasks
  
- I launched an Ec2 instance on the **aws cloud service** for this purpose
  
![start](/DevAdv/Pj3/images/1_launch_instance.jpg)

- SSH into the linux Ubuntu instance
  
![ssh](/DevAdv/Pj3/images/2_ssh_into_my_instance.jpg)

- I updated the linux package using 
 
      **sudo apt update**

![sudoupdatelinux](/DevAdv/Pj3/images/3_sudo_apt_update.jpg)

- Created a directory with the command
  
      **mkdir elite-task-api**

- cd into the directory with
  
      **cd elite-task-api**

![mkdirandcd](/DevAdv/Pj3/images/4_mkdir_elite_api_and_cd_to_it.jpg)

- I initialized **node.js**

     **sudo apt install npm**

![installnpm](/DevAdv/Pj3/images/5_sudo_apt_install_npm_for_node_js.jpg)

- Initialized and created **package.json** with
  
      **npm init -y**

![init](/DevAdv/Pj3/images/6_npm_init_-y_to_create_package_json.jpg)

- Went ahead to install necessary dependencies for **express** with the following command

     **npm install express**

![express](/DevAdv/Pj3/images/7_npm_install_express_to_install_dependencies_for_express.jpg)

- Created a file app.js by running 

     **vi app.js**

- Input my Configuration.

       // app.js

       const express = require('express');
       const app = express();
       app.use(express.json()); // This is to parse JSON bodies

       let tasks = [
        { id: 1, title: "Fix server issue", status: "Pending" },
        { id: 2, title: "Deploy new feature", status: "Completed" }
       ];

       // POST /tasks - Add a new task
       app.post('/tasks', (req, res) => {
       const { title } = req.body;
       const id = tasks.length + 1; // Generate new ID
       const newTask = { id, title, status: "Pending" };
       tasks.push(newTask);
       res.status(201).json(newTask);
       });

       // GET /tasks - Get all tasks
       app.get('/tasks', (req, res) => {
        res.json(tasks);
        });

       // PUT /tasks/:id - Update a task
       app.put('/tasks/:id', (req, res) => {
       const { id } = req.params;
       const { title, status } = req.body;
       const task = tasks.find(t => t.id === parseInt(id));

        if (!task) return res.status(404).send('Task not found');
  
        task.title = title || task.title;
        task.status = status || task.status;
  
          res.json(task);
        });

       // DELETE /tasks/:id - Delete a task
       app.delete('/tasks/:id', (req, res) => {
       const { id } = req.params;
       const taskIndex = tasks.findIndex(t => t.id === parseInt(id));

        if (taskIndex === -1) return res.status(404).send('Task not found');

        tasks.splice(taskIndex, 1);
        res.status(204).send();
        });

        // Set up the server
        const port = 3000;
        app.listen(port, () => {
        console.log(`Server running on http://localhost:${port}`);
        });
   
   
![appjs](/DevAdv/Pj3/images/9_app_js.jpg)

- Created a **Dockerfile** by using this command below to create the file

     **touch Dockerfile** 

![touch](/DevAdv/Pj3/images/10_create_Dockerfile_with_touch_Dockerfile.jpg)

- Edited the Dockerfile using
  
     **vi Dockerfile**

![inputcode](/DevAdv/Pj3/images/11_vi_Dockerfile_to_input_my_code.jpg)

- Input the needed configuration

       FROM node:18-alpine
       # Uses the Node.js 18 Alpine Linux base image (lightweight).

       WORKDIR /app
       # Sets the working directory inside the container.

       COPY package*.json ./
       # Copies package.json and package-lock.json to the container.
       # This is done before copying the rest of the application code to leverage Docker's caching.

       RUN npm install
       # Installs Node.js dependencies.

       COPY . .
       # Copies the rest of the project files.

       EXPOSE 3000
       # Exposes port 3000.

       CMD ["node", "app.js"]
       # Runs the Node.js application.



![input](/DevAdv/Pj3/images/12_Dockerfile_script.jpg)

- Created a docker ignore file to stop docker from copying unnecessary files using

     **vi dockerignore**

- input the following to the file

     node_modules
     npm-debug.log

![dockerignore](/DevAdv/Pj3/images/dockerignore.jpg)

- Installed Docker using

     **sudo apt install docker.io**

![docker](/DevAdv/Pj3/images/3_1_sudo_apt_install_docker_dot_io.jpg)

#### Execution of Project

- Proceeded to build the docker image and got an error
  
![error](/DevAdv/Pj3/images/13_tried_to_build_and_this_error.jpg)

- Went on to solve the error with the following command
  
     **sudo usermod aG docker ubuntu**

![usermod](/DevAdv/Pj3/images/14_applied_sudo_usermod_-aG_docker_ubuntu.jpg)

- Then used the following command for changes to take effect
  
     **newgrp docker** 

![effect](/DevAdv/Pj3/images/15_newgrp_docker_to_restart_and_take_effect.jpg)

- Build finally successful after error correction
  
     **docker build -t elite-task-api .**     

![build](/DevAdv/Pj3/images/16_docker_buid_error_corrected_successful_build.jpg)

- Ran the Docker image and made my containerized docker accessible vis port 3000 on my system using

     **docker run -p 3000:3000 elite-task-api**

- Having made my port 3000 accessible I went ahead to add and inbound rule to my Ec2 instance allowing me access port 3000.
  
![port3000](/DevAdv/Pj3/images/Add_inbound_rule_3000.jpg)

- Docker image is running live on **port 3000** of my instance
  
![dockerlive](/DevAdv/Pj3/images/docker_running_live.jpg)

##### Testing

- To test the **Elite Corporation** api using **postman** I setup mmy postman for the various test as follows

- **GET**
  
-  Created a new http task where I input my ip address, port and set content type to json in the body 
  
     content-type  json
     (http://18.224.70.207:3000/tasks)

- Sent get task in dropdown menu and got the tasks available
  
![get](/DevAdv/Pj3/images/GET_get_tasks_on_postman.jpg)

- **POST**
   
- Created a new http task where I input my ip address, port and set content type to json in the body 
  
     content-type  json
     (http://18.224.70.207:3000/tasks)

- POST task set in the dropdown menu

![post](/DevAdv/Pj3/images/POST_1setting_up_postman.jpg)

- Body where I input task to be added and selected json
  
![post2](/DevAdv/Pj3/images/POST_2setting_up_body_on_postman.jpg)

- Result as task was added successfully

![post3](/DevAdv/Pj3/images/POST_3send_on_postman.jpg)



- **PUT**
  
-  Created a new http task where I input my ip address, port, task Id and set content type to json in the body 
  
     content-type  json
     (http://18.224.70.207:3000/tasks/2) 
  
- PUT task in the dropdown menu and the task was modified to in progress
  
![put](/DevAdv/Pj3/images/PUT_modifid_task_to_inprogress.jpg)

- **DELETE**

-  Created a new http task where I input my ip address, port,task ID and set content type to json in the body  
  
     content-type  json
     (http://18.224.70.207:3000/tasks/3)
  
![verify](/DevAdv/Pj3/images/DELETE_task3_achieved_on_postman.jpg)

- Deleted and verified by sending a Get request and just two task were available in the array and new added task was deleted

![finaldel](/DevAdv/Pj3/images/verified_only_two_tasks_left_on_postman.jpg)

