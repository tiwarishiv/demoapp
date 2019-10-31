# Sample Python Application to demonstrate loadbalancing & application update strategies in Openshift 
   - Rolling Updates
   - Blue/Green Deployments
   - A/B Deployments
This will display the pod hostname which is servicing the web request

This is a fork of the below github repository
https://github.com/openshift/django-ex.git


Create a New Project for the sample application deployment (Optional)
   
    $ oc new-project demoproject --display-name="Demo Project" --description="Project for demo purpose"
    $ oc project demoproject

Deploy the sample python application and create route to expose it 

    $ oc new-app python:3.6~https://github.com/dineshsadasivam/demoapp --name=demoapp
    $ oc expose svc demoapp --name=demoapp

Display pods servicing demoapp

    $ oc get pods -o wide -l app=demoapp

Change the route loadbalacing algorith from the default Source IP to roundrobin and disable cookies for testing.
This will enabled testing of application loadbalacing from single workstation.

    $ oc annotate route/demoapp haproxy.router.openshift.io/balance=roundrobin 
    $ oc annotate route/demoapp haproxy.router.openshift.io/disable_cookies=true 

Command to validate load-balancing from CLI 

    $ while true; do curl http://demoapp-demoproject.router.default.svc.cluster.local 2>/dev/null |grep -i version ; done
    

