# check_host_not_alive
nagios check to confirm a host is down

# NOTES

nagios check to report if a host is UP.  
This is the opposite of the built-in check-host-alive command, and is used for hosts that SHOULD always be down.
In other words, alert with PROBLEM if the host is up, send OK message if host is down.

This script is intended to be used for hosts that have been decommissioned but still exist in the environment in a powered off state, and should NOT be powered on.

This script is executed on the nagios server as the host_check directive that is part of the host definition.

# USAGE 

Add a section similar to the following to the commands.cfg file on the nagios server:
```
    # This is the opposite of check-host-alive, where the host SHOULD always be down, so send a PROBLEM alert if host is UP, send OK if host is down.
    # 'check-host-not-alive' command definition
    define command{
       command_name    check-host-not-alive
       command_line    $USER1$/check_host_not_alive $HOSTADDRESS$
       }
```

Update the hosts.cfg file on the nagios server to look similar to:
```
    define host{
         use                     generic-host
         host_name               myhost.example.com
         alias                   myhost.example.com
         address                 myhost.example.com
         check_command           check-host-not-alive    <----- use this check_command
         }
```


# OUTPUT

<img src=images/up.png>


