# Sample Python APP to demonstrate Rolling Updates & A/B Deployments
This will display the pod hostname which is servicing the web request

This is a fork of the below github repository
https://github.com/openshift/django-ex.git

Change the route loadbalacing algorith from the default Source IP to roundrobin. 
This will enabled testing of application loadbalacing from single workstation.

#oc annotate route/demoapp haproxy.router.openshift.io/balance=roundrobin
