---
layout: post
title: BananaPi
published: true
tags:
- bananapi
- homeserver
summary: Eine (hoffentlich sinnvolle) Verwendung für den BananaPi
---

## Die Idee
Nachdem mein BananaPi nun schon ein halbes Jahr hier bei mir herumlag und irgendwie keine so richtige Aufgabe erfüllte (man beachte die ansprechende Staubpatina), hatte ich kürzlich einen Einfall, wie er vielleicht doch noch etwas sinnvolles zu tun bekommen könnte.

[<img src="{{ site.url }}/images/bananapi_blue_sm.jpg" alt="DustyBananaPi" style="width: 50%;max-height: 100%"/>]({{ site.url }}/images/bananapi_blue_sm.jpg)

Wir haben hier bei uns mittlerweile eine kleine Zahl an lokalen Serverdiensten am laufen, die sich munter auf verschiedene Rechner und virtuelle Maschinen verteilen. Nun ist es natürlich ein mühsames Unterfangen immer wieder einzelne Maschinen starten zu müssen, nur weil man gerade mal diesen oder jenen Serverdienst benötigt oder man etwas ausprobieren möchte.  
Weiterhin gibt es auch Serverdienste, die immer erreichbar sein sollen. Da ist es ja naheliegend solche Dienste auf einen ḱleinen sparsamen Rechner wie den BananaPi auszulagern. Auf diese Weise ist es auch nicht so tragisch, wenn der mal eine Zeit lang vor sich hin läuft und gerade nicht verwendet wird.

## Noch mehr Text

{% highlight bash %}.
putty -ssh -u fez -pw 1234 192.168.178.26
{% endhighlight %}

Wann ist das endlich zu Ende...
