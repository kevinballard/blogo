---
title: In the Nix of Time
date: 2013-05-31
draft: true
---
*This article was originally published to the TellApart Engineering Blog on 2013–05–31*

<center>

![](https://cdn-images-1.medium.com/max/2000/0*mTAFcIe3lDbu9wwm.gif)

</center>

Back during the 2011 holiday season I was speaking with Josh, TellApart’s CEO, about a piece of custom hardware I had just built for the office — an “[Easy Button](http://blog.makezine.com/2011/04/08/the-awesome-button/)” that launches new clients. Josh is an avid follower of what’s hot at the intersection of design and technology (see [3D printed lapel pins](https://www.shapeways.com/product/UUPVHB8QK/tellapart-lapel-pin?li=shortUrl)), and since we were on the topic of hardware, our conversation led to the resurgence of Nixie tubes for decorative displays. He wondered if there was some TellApart themed way of using them, and offered to commission any interesting idea I could come up with.

<center>

![IN-18 Nixie Tube](https://cdn-images-1.medium.com/max/2000/0*PXktjdMVA_YEw-Tq.jpg)

*IN-18 Nixie Tube*

</center>

I didn’t give the proposal too much thought at the time. Nixie tubes are an old technology, requiring high voltages and driver chips that fell out of production decades ago. It was also the middle of the holiday season — by far the busiest time of year for TellApart, so my attention turned to other projects. But the idea was lodged in the back of my head, where it sat percolating.

Many months later, I came across the newly launched [Electric Imp](https://www.electricimp.com/) — a hardware, software, and web service combination that can trivially connect small, cheap devices to the Internet. Something in my head clicked, and I knew what I had to build. I brought a proposal to Josh, who promptly handed me the corporate credit card, and I was off to work.

<center>

![Testing with the Electric Imp hardware](https://cdn-images-1.medium.com/max/2000/0*MVh2ND7cxxwcPdmu.jpg)

*Testing with the Electric Imp hardware*

</center>

I knew what I wanted to build: an Internet-connected counter with 10 [IN-18 Nixie](http://www.tube-tester.com/sites/nixie/data/in18.htm) tubes. There was a catch though: Josh wanted to show off the finished product at the 2012 TellApart holiday party, which gave me just 6 weeks to pull it all together.

IN-18 tubes have been out of production for more than 20 years, and were only made in the former USSR, making them somewhat hard to find. Things like connectors and driver circuits have to be custom made. To make things harder, all the modern reference designs are for 1 to 6 tubes — driving 10 tubes takes more current and more I/O pins than these designs allow for. I raced to cobble together a solution, which ultimately involved an importer in Los Angeles, parts from a hobbyist in the UK, a pair of .5mm pitch 100-pin I/O expanders that pushed the limits of my soldering skill, and some custom parts from TAP Plastics in Mountain View.

Once I had the parts, assembly was straightforward, albeit extremely tedious. I didn’t have time for the back-and-forth needed to make a custom printed circuit board, so I did all the wiring by hand. All told, there are over 500 solder points or connector crimps, which ate into pretty much every night and weekend from the moment the pieces arrived until the unveiling.

<center>

![So many wires](https://cdn-images-1.medium.com/max/2000/0*j6sE3sof4qhkydpy.jpg)

*So many wires*

</center>

Fortunately I finished just in time, and the result turned out better than I had anticipated:

<center>

![](https://cdn-images-1.medium.com/max/2000/0*rhZ5229eGb73n1AX.jpg)

![](https://cdn-images-1.medium.com/max/2000/0*s_uK4ZeM9OrWk6ZM.jpg)

![](https://cdn-images-1.medium.com/max/2000/0*Sy5LWTya81SnEn6X.jpg)

</center>

That just left filling out the software and tying into the TellApart real-time reporting service. I setup a stream of Ad Impression and Click data pointed at the Electric Imp servers. From there the data is forwarded to the counter over its Wi-Fi connection. Finally, I made some (literally) last minute tweaks to the I2C driver to get the animation just right. The result is a real-time counter of global TellApart Ad Impressions, rendered in glass and neon, right in our lobby:

<center>

<iframe width="560" height="315" src="https://www.youtube.com/embed/UQEd7o0Nww0" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/8ajeo33llVQ" frameborder="0" allowfullscreen></iframe>

</center>

It was a huge hit at the party; a few people even wanted to know how they could get their own. It was also the center of attention at our PyCon booth and drew quite a crowd. There are a few improvements I’d like to make: adding an OLED character display to tell you what it’s counting, adding new transition effects, and possibly making a proper printed circuit board. For now though, I’m happy to just watch the impressions count up.