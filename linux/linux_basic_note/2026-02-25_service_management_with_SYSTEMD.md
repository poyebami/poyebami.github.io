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
ExecStart= is a key directive in systemd unit file [Service] taht defines the command or scrpit to execute when a service is started. Can be sepecified multiple times, or used in conjuction with ExecStartPre= (commands before) and ExecStartPost = (commands after)

User= allows unprivileged users to manage their own services and daemons. 

*Daemons are background processes that operate independently of user interaction, typically starting at boot to manage system tasks, network requests, or services.

Restart= restart a SYSTEMD service.

RestartSec= specify the amount of time to wait before attempting to restart a service. The default delay is 100ms.

WantedBy = specifies which other unit(s) should start the current serbice or unit whn the listed united is enabled via systemct1 enable. It defines a weak dependency. 

*Weak dependency means if the "wanted" unit fails to start or stop, the "wanting" unit (the target) will continue to run. The most common value for WantedBy = in a standard service unit is multi-user.target. This means the service should be stated when the system reaches the non-graphical multi-user state. 
