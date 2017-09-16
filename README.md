# What is remote port forwarding?
I'm glad you asked. Someone did a great writeup on that already: http://blog.trackets.com/2014/05/17/ssh-tunnel-local-and-remote-port-forwarding-explained-with-examples.html

# How do I set this up?

Run the following on your remote proxy to enable the ability for it to send requests (to your machine!):

```
sudo vim /etc/ssh/sshd_config
```

Then add the following line to that file:

```
GatewayPorts yes
```

Then restart:
```
sudo service ssh (or sshd) restart
```

Then you only need to run some docker stuff using the LetsDeploy workflow.

But what is Let's Deploy? Check it out here:
Check it out here: https://github.com/lukeswart/docker-shareabouts#letsdeploy

These are mostly just my hacky personal scripts. But hey, it's a start.
(TODO: detail how to run remote port forward within the context of Let's Deploy)

# How do I run this thing?
Now that you have remote port forwarding set up on your remote proxy server, just enable your locally running server to listen and respond to requests coming from the remote proxy. 

For example, say your local server is running on port 3000, and your remote proxy is configured to forward requests to port 8010. Then you just run the following command:

```
ssh -nNt -g -R 0.0.0.0:8010:localhost:3000 my-proxy-server
```

Now navigate to https://example.com (as configured in your remote proxy above), and voila! You can test your app on SSL, mobile devices, or have friends around the world view your latest work right on your machine.


