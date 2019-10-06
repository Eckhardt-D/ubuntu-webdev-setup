# Setting up my linux machine for web development

### Todos

- [x] Update apt-get
- [x] Install curl & other essentials
- [x] Install Google Chrome
- [x] Download Node Version Manager
- [x] Install Node LTS version & Latest
- [x] Install Git
- [x] Setup Git SSH
- [x] Install VScode
- [x] VScode theme
- [x] VScode settings
- [x] VScode extensions
  - [x] Live sass compiler
  - [x] Prettier
  - [x] Vetur
  - [x] vscode-icons
- [x] Install lite-server
- [x] Install MongoDB & run as service

### Commands

1. `sudo apt-get update`

2. `sudo apt-get install curl build-essential libssl-dev`

3. `curl https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb`
   `sudo dpkg -i google-chrome-stable_current_amd64.deb`

4. `curl https://raw.githubusercontent.com/creationix/nvm/v0.35.0/install.sh | bash`
   `source ~/.profile`

5. `nvm install node`
   `nvm install --lts`
   `nvm use --lts`

6. `sudo apt-get install git-core`
   `git config --global user.name "Eckhardt-D"`
   `git config --global user.email "eckhardt.dreyer@gmail.com"`

7. `ssh-keygen -t rsa -b 4096 -C "eckhardt.dreyer@gmail.com"`
   `eval "$(ssh-agent -s)"`
   `ssh-add ~/.ssh/id_rsa`

8. `sudo snap install code --classic`

12. `npm i -g lite-server`

13. `sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10`
    `sudo apt-get update`
    `sudo apt-get install -y mongodb`
    `sudo nano /etc/systemd/system/mongodb.service`


    copy the following into file:

    ```bash
    #Unit contains the dependencies to be satisfied before the service is started.
    [Unit]
    Description=MongoDB Database
    After=network.target
    Documentation=https://docs.mongodb.org/manual
    # Service tells systemd, how the service should be started.
    # Key `User` specifies that the server will run under the mongodb user and
    # `ExecStart` defines the startup command for MongoDB server.
    [Service]
    User=mongodb
    Group=mongodb
    ExecStart=/usr/bin/mongod --quiet --config /etc/mongod.conf
    # Install tells systemd when the service should be automatically started.
    # `multi-user.target` means the server will be automatically started during boot.
    [Install]
    WantedBy=multi-user.target
    ```

    `systemctl daemon-reload`
    `sudo systemctl start mongodb`

    check if running
    `sudo systemctl status mongodb`

    run mongo on startup
    `sudo systemctl enable mongodb`

    create user (replace <password>)
    `mongo -u admin -p <password> --authenticationDatabase admin`
