---
published: true
header:
  overlay_image: #/assets/images/rocky-mtns.jpg
  caption: #"[CC License](https://creativecommons.org)"
categories:
        #- Testing
---
I recently built a set of RV gates to get into the back half of our property.  I acquired a pair of Mighty Mule MM360 gate openers to open the gates.  The MM360 is a medium duty gate opener, but was more than capable of controlling the gates I welded, despite them being constructed of oil field pipe and weighing probably around #300 lbs each.  One of these I won on an auction site and the  only thing wrong with it was that the transmitter didn't work.  After a bit of tinkering I realized that the on board connections to control various accessories worked fine. I was able to activate the gate by simulating a momentary button press by shorting the two wires together between 'Common' and 'Cycle'.  

![GateCircuit](/assets/images/circuit.jpg){:height="600px" width="800px"}

# The strategy
# WiFi connected:
I want something that will connect over Wifi. I have a Unifi UAP-AC-M Access point out on our horse barn that gives me a really good wifi signal at the gate.

# Maintain original function:
I don't want something that should my WiFi network go down that the gate is unusable.  I want to maintain a local network control as well as local physical control (fancy speak for a doorbell switch). 

# Aesthetically pleasing:
It's too easy to create something that looks like it fell out of the pocket of one of the Borg members.  I want something to fit the aesthetic of the property while giving me the geeky goodness I so desire.



The Shelly One controller can be powered by 12V or 120 depending on the jumper setting.

![Shelly Voltage Select](/assets/images/ShellyVoltageSelect.jpg)



# Script required for comments to be enabled.
<script src="https://utteranc.es/client.js"
        repo="shaunandersonaz/shaunandersonaz.github.io"
        issue-term="pathname"
        theme="github-dark"
        crossorigin="anonymous"
        async>
</script>

