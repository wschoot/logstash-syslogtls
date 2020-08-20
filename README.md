# logstash / syslog / tls



# Used components
## cfssl 1.4.1
Used to create a small PKI with a CA rootkey/cert which signs two certificates, one for the (logtash)server and one for the (syslog)client. It also validates the client and makes sure the correct hostnames are used.

## ELK
Major v7 is used for the ELK stack

### elasticsearch
Used to store messages, relayed from logstash

### logstash
Listens to messages on port 6514, which is configured with a TLS certificate. Outputs to both elastichsearch and to a logfile for easy viewing.

### kibana
Dashboard for viewing syslog messages

## rsyslog
rsyslog v8, configured with TLS 

Config based on https://www.rsyslog.com/doc/v8-stable/tutorials/tls_cert_client.html

## vagrant
Creates two virtual machines, both CentOS/7 as of now.

## ansible
Provisions the servers

# Notes
For now, SElinux should be disabled on the clienthost as it prevents from propery loading its modules

A cronjob is created to periodically (default, every minute) send a syslog message to the remote logstash server

Starts logstash (and some other tools) in a tmux session which you can pickup by ssh'ing into the logstash host, use `sudo -s` to get root and use `tmux at` to attach the terminal multiplexer. This is also described in the motd.

