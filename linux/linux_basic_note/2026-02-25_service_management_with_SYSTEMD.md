<h1>Creating a SYSTEMD Service</h1>
We need to create a service unit file. For instance, the unit file is called project-mercury.service, needs to be created under /etc/systemd/system directory. 

/etc/systemd/system/project-mercury.service

The command that need to run in the backgroud, in this case is /usr/bin/project-mercury.sh

```console
[Service]
ExecStart = /bin/bash /usr/bin/project-mercury.sh
```
There is a directive called ExecStart, which is used to run a command or an application. Since this is a Bash script, we will specify the command as /bin/bash, followed by the absolute path to the script as the argument. 

The service definition can be created with just these two lines.

<h4>Run the Service in the background </h4>
Issue the command systemctl start project-mercury.service.
```console
 $ systemctl start project-mercury.service
```
We must use sudo command, as the service is set to run as the root user. 

<h4>Check if the Service is running in the background </h4>
 ```console
 $ systemctl status project-mercury.service

 * project-mercury.service
    Loaded: loaded (/etc/systemd/system/ report-manager; statics;
 vendor preset: enabled)
    Active: active (running) Fri 2020-04-10 00:52:15 EDT; 6min ago
 Main PID: 25041 (project-mercury.sh)
    Tasks: 2 (limit: 4915)
    CGroup: /system.slice/ project-mercury.service
            6494 sleep 80
            25041 /bin/bash /usr/bin/project-mercury.sh
 ```
<h4>Stop the Service </h4>
 ```console
 $ systemctl stop project-mercury.service
 ```
<h4>Update Sections </h4>
 ```console
 $ sudo systemctl edit /etc/systemd/system/name_of_service
 $ sudo systemctl edit <name_of_service>

 $ sudo vi /etc/systemd/system/sample.service
 $ # add /bin/bash /rott/sample_script.sh to ExecStart

 ```

https://loldle.net
<h4> Allow the Service to start during boot </h4>
We need to add another service called install/ 
 ```console
 [Service]
 ExecStart = /usr/bin/project-mercury.sh

 [Install]
 WantedBy graphical.target
 ```
 Use the WantedBy directive, whose value should be the system dtargetm or runlevel you want to enable it for. Since we are running in graphical mode, we will set the value to graphical.target. 

<h4>Add the Service account to use the service instead of root</h4>
 ```console
 [Service]
 ExecStart - /usr/bin/project-mercury.sh
 
 User=project_mercury
 Restart=on-failure
 RestartSec = 10

 [Install]
 WantedBy graphical.target
 ```
 Restart directive defines how and when to restart the service. In the case, the value is set to on-failure. This will ensure that the system attempts to restart the service should it fail for some reason. 
 
 RestartSec directive is used to set the time in seconds to wait before the system attempts to restart it. 

 With SYSTEMD, the service events are automatically logged. 

<h4>Define a dependency </h4>
 In our example: the Python Django application depends on the PostgreSQL service, we can define a dependency that makes sure that our new service is started only after the PostgreSQL database is read. 

 ```console
 [Unit]
 Description=Python Django for Project Mercury
 Documentation=http://wiki.caleston-dev.ca/mercury
 After=postgresql.service

 [Service]
 ExecStart= /usr/bin/project/-mercury.sh

 User=project_mercury
 Restart=on-failure
 RestartSec= 10

 [Install]
 WantedBy graphical.target
 ```

<h4> System to detect the changes</h4>
 ```console
 $ systemctl daemon-reload
 ```

<h3>Directives</h3>
`ExecStart`= is a key directive in systemd unit file [Service] that defines the command or scrpit to execute when a service is started. Can be sepecified multiple times, or used in conjuction with ExecStartPre= (commands before) and ExecStartPost = (commands after)

`User`= allows unprivileged users to manage their own services and daemons. 

*Daemons are background processes that operate independently of user interaction, typically starting at boot to manage system tasks, network requests, or services.

`Restart`= restart a SYSTEMD service.

`RestartSec`= specify the amount of time to wait before attempting to restart a service. The default delay is 100ms.

`WantedBy`= specifies which other unit(s) should start the current serbice or unit whn the listed united is enabled via systemct1 enable. It defines a weak dependency. 

*Weak dependency means if the "wanted" unit fails to start or stop, the "wanting" unit (the target) will continue to run. The most common value for WantedBy = in a standard service unit is multi-user.target. This means the service should be stated when the system reaches the non-graphical multi-user state. 

<h3>SystemD Tools</h3>
The two major tools we will see are the `systemctl` and `journalctl`.

<h4>Systemctl </h4>
 ```console
 Manage system state on systemd managed server
 START/STOP/RESTART/RELOAD a service
 ENABLE/DISABLE a service to start during the system boot
 Used to view information about and manage the system state
 List and manage Units 
 List and update Targets
 ```
 Useful systemctl commands
 ```console
 $ # start the service
 $ systemctl start docker

 $ # stop the service
 $ systemctl stop docker

 $ # restart the service
 $ systemctl restart docker

 $ # reload the service without interrupting normal functionality
 $ systemctl reload docker

 $ # enable a service and make it persistent to cross reboot
 $ systemctl enable docker

 $ # disable the service at boot
 $ systemctl disable docker

 $ # provides information about the state of the service
 $ # if running properly, it should show a state of active running
 $ systemctl status docker
 
 $ Active active (running) since Sat 2020-03-21 00:45:22 EDT; 43s ago
 $ # there are few other states 

 $ active : service running
 $ inactive : service stop
 $ # there are transient states called activating and deactivating , which are in between two states

 $ failed : crashed/error/timeout etc
 ```
 ```console
 $ # running this command after making changes to a service unit file
 $ # reload the system manager configuration
 $ # and make systemd aware of the changes
 $ systemctl daemon-reload
 ```
 A running service whose unit file has been updates on disk can only be restarted after running the systemctl deemon-reload command
 ```console
 $ # make changes to unit file
 $ systemctl edit <unit_name>
 
 $ # open the service configuration file with a text editor
 $ # units edited this way apply the changes immediately
 $ # without having to run the daemon reload
 $ systemctl edit project-mercury.service --full
 ```
<h4>Systemctl to manage state</h4>
 ```console
 $ # see the current runlevel or the target
 $ systemctl get-default

 $ # change to a different target
 $ systemctl set-default multi-user.target

 $ # list all the unit systemd has loaded or attempted to load
 $ # prints all units that are active, inactive, failed, or in  other transient states
 $ systemctl list-units --all
 
 $ # see only information about the active units 
 $ systemctl list-units
 ```
<h4>Journalctl  </h4>
 ```console
 Query the contents of the systemd loggging system called journal
 Troubleshooting tool for issues like service failures
 ```
 ```console
 $ # prints all the log entries from the oldest entry to the newest
 $ journalctl

 $ # see the logs from the current boot
 $ journalctl -b

 $ # see the log entries for a specific unit
 $ journalctl -u <unit_name>
 $ journalctl -u docker.service
 ```
 The data provided by the log enrires for a service file, gernerally provides the r eason why a service unit is in a inactive or failed state. 
 Great for debugging issues with the config files, or issues with the service dependencies, etc. 
