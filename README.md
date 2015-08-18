# Minecraft Server Init

This init script provides a service wrapper around minecraft_server.jar. It
allows the init system to make start/stop/restarts/status calls while allowing 
the server to start under a service account along with the physical server.

## Installation

The script requires a service account: 

	sudo adduser minecraft

Then copy the minecraft_server script to /etc/init.d/

	sudo cp ./minecraft_server /etc/init.d/

Under some Linux systems, the service needs registered under the default
runlevel:

	sudo update-rc.d minecraft_server defaults

Because the service relies on a screen daemon, Ubuntu may have an issue with
screen and the priority of the service. By changing the priority of the startup
script, I was able to get it to work with screen while avoidng the error message
"Cannot make directory '/var/run/screen': Permission denied" which seems linked
to severel Ubuntu bugs.

	sudo update-rc.d minecraft_server defaults 99 10

## Commands

To start a service manually using a system like Upstart (Ubuntu):

	sudo service minecraft_server start

Likewise, to stop the service:

	sudo service minecraft_server stop

And to restart the service: 

	sudo service minecraft_server restart

Commands can be passed to the server by passing "command":

	sudo service minecraft_server command "<command>"

The script supports updating the server binary, but at this time it relies on an 
outdated URL to fetch minecraft_server.jar. DO NOT attempt to update the 
Minecraft server with this script at this time until this issue is patched.

## Multiple Instances

The script can be copied multiple times and used to host multiple servers
provided that...

* Each script has a unique name
* $MCPATH in each script points to a unique location
* $SERVERNAME in each script has a unique value
