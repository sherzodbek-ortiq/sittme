# Sittme

## Description
**API only Cursor-based pagination (aka keyset pagination)** built with Ruby and Ruby on Rails.<br> App runs in two Docker containers: 1 - rails app, 2 - postgres database. <br>
The volume binding is used in development to map container files and folders to host machine.<br> Volume binding makes it possible to exclude files from mapping.<br>
There are separate Docker and Docker compose files for development and test environments.<br>

## Tech stack
Docker<br>
Docker compose<br>
Ruby<br>
Ruby on Rails<br>
Postgres<br>

## How to make it work
**For VS Code remote container development environment:**<br>
Install VS Code remote containers extension.<br>
Create VS Code remote container configurations from **docker-compose-vs_code.yml**.<br>
Choose servise (for rails app choose **api**).<br>
Open the project root folder in container from VS Code remote containers extension command pallete.<br>
Install all the host VS Code's stack related extensions within container,<br>
settings are kept in **devcontainer.json**.<br>
Now the VS code development environment within container is ready to use.<br>
Don't forget to run migrations before starting server: `rails db:migrate`.<br>
Fire up rails server with: `rails server --binding 0.0.0.0 --port 3000`.<br>
You may need to remove manually the `<rails app root folder>/tmp/pids/server.pid` to successfully start the server.<br><br>

**For development environment:**<br>
cd to project root folder.<br>
We have 2 containers in development environment.<br>
Create images + create and run containers:<br>
`docker-compose -f ./docker-compose-dev.yml up`<br>
Stop and remove containers:<br>
`docker-compose -f ./docker-compose-dev.yml down`<br>
Rebuild images + create and run containers:<br>
`docker-compose -f ./docker-compose-dev.yml up --build`<br>
List services:<br>
`docker-compose -f ./docker-compose-dev.yml ps`<br><br>

**For test environment:**<br>
cd to project root folder.<br>
We have 2 containers in test environment.<br>
Create images + create and run containers:<br>
`docker-compose -f ./docker-compose-test.yml up`<br>
Stop and remove containers:<br>
`docker-compose -f ./docker-compose-test.yml down`<br>
Rebuild images + create and run containers:<br>
`docker-compose -f ./docker-compose-test.yml up --build`<br>
List services:<br>
`docker-compose -f ./docker-compose-test.yml ps`<br><br>

**Route to create babysitter**<br>
Post first_name and last_name to `localhost:3000/api/v1/babysitters`<br>
last_name is optional, first_name is requred.<br><br>

**Route to pagination**<br>
**Get direction: forward**<br>
`localhost:3000/api/v1/babysitters?end_cursor=50&direction=forward`<br>
**Get direction: backward**<br>
`localhost:3000/api/v1/babysitters?start_cursor=50&direction=backward`<br>

**direction** is the direction from cursor, it can be forward and backward.<br>
**end_cursor** is the id of the last babysitter in array of paginated babysitters.<br>
**start_cursor** is the id of the first babysitter in array of paginated babysitters.<br>

**Use end_cursor with direction=forward and start_cursor with direction=backward**