# Minecraft Server Init

This init script provides a service wrapper around minecraft_server.jar. It
allows the init system to make start/stop/restarts/status calls while allowing 
the server to start under a service account along with the physical server.

## Installation

## Commands

To start a service manually using a system like Upstart (Ubuntu):

	sudo service minecraft_server start

Likewise, to stop the service:

	sudo service minecraft_server stop

And to restart the service: 

	sudo service minecraft_server restart

Commands can be passed to the server by passing "command":

	sudo service minecraft_server command "<command>"

## Multiple Instances

The script can be copied multiple times and used to host multiple servers
provided that...

* Each script has a unique name
* $MCPATH in each script points to a unique location
* $SERVERNAME in each script has a unique value
