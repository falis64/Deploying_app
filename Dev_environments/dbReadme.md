# Deploying the app

- In your VScode, run vagrant destroy
Now in the vagrant file:
- change app.vm.box to us "ubuntu/bionic64
- And change database.vm.box to use "ubuntu/bionic64" (the datablase might be saved as db like mine was)
It should look like this once saved
![img.png](img.png)

Do vagrant up
- open 2 bash terminals and login with ```vagrant up/db``` (seperately)
- Do check in vagrant app -  ```ls```, to see if app is there, ```nodejs --version```, ```pm2 --version```
- check on db - ```sudo systemctl status mongod```


On the DB bash terminal
- ```sudo nano /etc/mongod.cong```
This should open the mongod nano file
- scroll down to the network interforce and change the bindIp: to 0.0.0.0 - bindip dictates who can access it
- now control x, y then enter to save 
- now ```sudo systemctl restart mongod``` - to restart and save the changes - you won't get anythingfrom this
- ```sudo systemctl enable mongod``` - this will start and ensure that all the changes are put into place
- now ```sudo systemctl status mongod``` - to check that it's working
- you can do control z to get out of it
- we're done with the db machine

On the bash terminal (in app)
- make it persistent by using the command - ```sudo nano .bashrc```
This will open the bashrc nano file
- scroll all the down to the bottom where the last line is fi and add the following:
- ```export DB_HOST=mongodb://192.168.20.150:27017/posts``` - the developers have hosted an environmental variable called DB_HOST
- now save this by controlx, y and enter
- now you can exit by control z and do the following commands
- ```printenv DB_HOST```
- ```source .bashrc```
- ```printenv DB_HOST``` - now it should print out the data
- now clear
- ```cd app``` and ```ls```
- ```npm install``` - this will take a while and when it runs you'll see warnings
- now we want to seed the database by using ```node seeds/seed.js```
- now you can start the app by using ```node app.js```
You should get a message saying the app is ready
now copy the ip address and add :3000/posts in the browser