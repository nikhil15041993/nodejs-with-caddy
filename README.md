# nodejs-with-caddy

## Step 1. Clone the GitHub repository for nodejs code

```
git cone <repo name>
```
Go to the file demo_express ``` cd demo_express ```

use the command ``` npm i ``` for install the all dependancy for the project

Now we are going to Start the appliction By using the command ``` node app.js ```

Now the application started with port 3000 

we can acess this appication by server ip:3000


Now we are going change the  access of our application only from localost not remotly 

for checking the port we use the command ```netstat -tln``` 

for that stop our server and edit our app.js file 

add the following code 

```
app.listen(PORT,'localhost' () => console.log(`🚀 @ http://localhost:${PORT}`))
```
start our app ``` node app.js ```

and check it by ```netstat -tln ``` now we can see the output ```127.0.0.1:3000```



## Step 2. Access this app using caddy server by reverce proxy


Stop the application and install the caddy server 

```
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo tee /etc/apt/trusted.gpg.d/caddy-stable.asc
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
sudo apt update
sudo apt install caddy
```
 After that we check ```netstat -tln``` we can see some limited ports are opening only
 
 our caddy server not yet started, so we can start our caddy server by using ``` caddy run ``` ( inside the demo_expess directory)
 
 now the ``` netstat -tln ``` show the new port eg: 127.0.0.1:2019
 
 
 ## Step 3. Create the Caddyfile
 
 First stop the server and create a file called Caddyfile (inside demo_express directory)
 
 edit it by your fav editor ``` vi Caddyfile ```
 
 And copy the following code
 
 ```
 mytestingserver.xyz {
          reverse_proxy 127.0.0.1:3000
          }
 ```
 
 ## Step 4. Install process manger pm2 to run thi application
 
 ```
 sudo npm install pm2 -g
 ```
 this will run our  aplication in backgroud
 
 Now we can start our application using pm2 ```pm2 start app.js```
 
 use command ```pm2 ls ``` for running application details
 
 If we use ```netstat -tln``` we can see our application is running ```127.0.0.1:3000```
 
 ## Step 5. Point the ip of our server to demain mytestingserver.xyz
 
 Go to domain website and selete manage domain add 2 A records 
 
  Name = @ Value = server ip
  Name = www Value = srver ip
  
  Start the caddy server ```sudo caddy run```
  
  
  now we can access our application by typing oru domain in browser 


## Step 6. Enable caddy to run as a service

if we close the ssh section the application will stop that why we need to run our caddy to run as a service

first stop the application by ```pm2 stop app.js``` check by ```pm2 ls```

we need to run as a service both pm2 and caddy

```pm2 startup``` start pm2 when server reboot ( copy and paste the out put command)
Caddy as a service ```sudo systemct start caddy``` and ```sudo systemctl enable caddy```

Copy the content of caddy file in demo_expess directory and paste it on /etc/caddy/Caddyfile

now start te caddy  by ``` sudo caddy start``` ifit get an error msg just stop the caddy and re run it ```sudo caddy start```

now start pm2 ```pm2 start app.js```
  
  
  
  
  



