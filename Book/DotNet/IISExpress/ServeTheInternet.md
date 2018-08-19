# IISExpress For Everyone
Want to expose your application to the world, but don't want to use full IIS? No problem!
With the following steps, you can easily allow anybody to access your IISExpress web server.


## Get It Running
Steps:
- Open a firewall rule on the router for 8060 on my static internal IP
- Open an outbound rule on your firewall for 8060
- Set IIS Express to serve on 8060
- Run from Powershell: `netsh http add urlacl url=http://*:8060/ user=everyone`
- Add in your `.vs/config/applicationhost.config` (in the bindings for your site):
`<binding protocol="http" bindingInformation="*:8060:*" />`

## Close It Up
If you need to stop exposing your server to the world, you will have to reverse the previous steps.
Make sure you:
- Remove the firewall rule on your router that allows the connection to port 8060 on your local machine
- Remove the outbound firewall rule on your local machine
- Run the following from powershell: `netsh http delete urlacl url=http://*:8060`
- Remove or comment-out the binding in `.vs/config/applicationhost.config`

