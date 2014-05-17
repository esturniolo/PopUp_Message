PopUp_Message
=============

Enviar popups a otras pc de la red utilizando Zenity

Creditos para Matt: http://askubuntu.com/users/17448/matt
Informacion tomada de http://askubuntu.com/questions/31582/send-messages-between-2-ubuntu-pcs-net-send-style

First we need a "daemon" to run in the background. Second, we need a program to make the alert pop up. I have zenity installed. If you do not, please install it, or edit the script to use whatever you like [e.x. xmessage, but that is ugly]. Next, paste this into 'daemon.sh':

```bash
#!/bin/bash
port=3333
nc -l $port | while read msg; do zenity --info --text "$msg"; done
```

Now, make it executable chmod +x daemon.sh, now run it in the background: ./daemon.sh &

Now you're done! Well, you actually need to do this on each computer. You also will want to automate the start of the daemon. Open the 'startup' applications from the menu, and add your script. Once that's done, to send a message to the other computer, type in:

nc 192.168.1.X 3333 then type your message and hit Enter. Each enter line will make a message pop up. To exit nc, press Ctrl +C, or Ctrl +D.

Just make sure to replace 192.168.1.X with the real local IP of the other PC. [You can use ifconfig to find the IP address]

I see you already have accepted an answer for this question :( But if my solution works for you, please at least give me a Upvote! Thanks. Also, you could also make another script, say, message.sh. In that, paste:

``` bash
#!/bin/bash
nc 192.168.2.X 3333
```

Then chmod +x message.sh. Then you can just type ./message.sh then type your message, then enter, and your message is sent. Also, now that I think of it, you could also add a sound notification. I would recommend mplayer, it's a CLI media player. Shouldn't be too hard to figure out, but if you have any questions, please don't hesitate to ask!
