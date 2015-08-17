usage: check_nping [-h] -H <IP or URI> -M <mac> [-w <msec>] [-c <msec>] [-C <times>]

Check with nping if HOST is alive routing through a router MAC.

Mandatory arguments:
-M <mac>        the mac address of the gateway
-H <IP or URI>  the host to check

Optional arguments:
  -h, --help      show this help message and exit
  -w <msec>       the WARNING time (Default: 3000ms)
  -c <msec>       the CRITICAL time (Default: 5000ms)
  -C <times>      Ping count (Default: 5)
  


Place this file in libexec folder

Create the command in Nagios:

# $ARG1$ Host to ping
# $ARG2$ MAC address of the gateway to check
# $ARG3$ Ping count
# $ARG4$ Warning value in ms
# $ARG5$ Critical value in ms
#
define command{
        command_name            check_nping
        command_line            $USER1$/check_nping -H $ARG1$ -M $ARG2$ -C $ARG3$ -w $ARG4$ -c $ARG5$
}


Use the command:

define service{
        use                     generic-service
        host_name               ROUTER-90-1
        service_description     Ping to Google
        check_command check_nping!www.foo.com!ff:ff:ff:ff:ff:ff!4!3000!5000
}
