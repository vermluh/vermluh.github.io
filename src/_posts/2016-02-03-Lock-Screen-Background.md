---
layout: post
title: MATE Lock Screen Background anpassen
published: true
tags:
- mint
summary: Anpassung des Standard Lock Screen Hintergrundes in Linux Mint MATE
---

* TOC
{:toc}

Hat man ein Wunsch-Wallpaper für seinen Desktop gefunden und eingerichtet, dann möchte man natürlich auch diesen Hintergrund auf dem Lock Screen sehen. Zumindest geht es mir so.  
Wenn ich mir nun den Lock Screen von MATE ansehe, dann fällt dieser immer wieder auf einen Standrad Hintergrund zurück. Das ganze sieht dann so aus:

[<img src="{{ site.url }}/images/default_lockscreen.jpg" alt="Lock Screen mit Standard-Hintergrund" style="width: 100%;max-height: 100%"/>]({{ site.url }}/images/default_lockscreen.jpg)

Ein wenig Recherche brachte dann die Information, dass dieser verwendete Standard Hintergrund in `/usr/share/backgrounds/linuxmint` definiert ist. Schaut man sich den Inhalt dieses Pfades an, ergibt sich folgendes Bild.

![Standard Hintergrund]({{ site.url }}/images/default_background.jpg "Standard Hintergrund")

Aha. Der Standard-Hintergrund ist also lediglich ein Link auf ein andere Bilddatei. Wenn man diesen Link nun anpasst und auf sein gewünschtes Wallpaper verweisen lässt, dann müsste doch...  
Nach einem schnellen  
{% highlight bash %}
sudo rm default_background.jpg
sudo ln -s /home/fez/Pictures/desktops/wallhaven-318296.png default_background.jpg
{% endhighlight %}
zeigt sich in `/usr/share/backgrounds/linuxmint` das folgende Bild.

![Eigener Standard Hintergrund]({{ site.url }}/images/own_default_background.jpg "Eigener Standard Hintergrund")

Wenn alles klappt wie gewünscht, dann sollte der Lock Screen nun auch mit dem Wunsch-Wallpaper aufwarten. Und siehe da:

[<img src="{{ site.url }}/images/own_lockscreen.jpg" alt="Lock Screen mit Wunsch-Hintergrund" style="width: 100%;max-height: 100%"/>]({{ site.url }}/images/own_lockscreen.jpg)

Es hat also alles geklappt. Der Lock Screen hat ab jetzt ebenfalls das Wunsch-Wallpaper.  

*Shiny.*
