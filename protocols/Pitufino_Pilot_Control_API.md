# Pitufino's unified Autopilot Control API

An autopilot can be controlled by an app by sending **HTTP POST** requests to Pitufino's HTTP server (URL path **/cmd**). The request needs to contain a single name-value pair as in submitting an HTML form using either the content type application/x-www-form-urlencoded or multipart/form-data. The name of the required field is "pilot" and possible values are: "-10", "+10", "-1", "+1", "stby", "auto", "wind", "nav".

    pilot = -10 | +10 | -1 | +1 | stby | auto | wind | nav

The HTTP client needs to be capable to perform **digest access authentication** as the user may not allow unauthenticated access. Any libcurl-based client should be able to do so.

## Examples using curl on the command line

Switching to compass mode (without authentication, application/x-www-form-urlencoded):

    curl -d "pilot=auto" pitufino.local/cmd

Using content type multipart/form-data:

    curl -F "pilot=auto" pitufino.local/cmd

If the client cannot resolve the mDNS hostname, the IP address needs to be used:

    curl -d "pilot=auto" 192.168.4.1/cmd
    
With digest authentication:

    curl --digest -u user:passwd -d "pilot=auto" pitufino.local/cmd
    

