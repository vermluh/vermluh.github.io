---
layout: post
title: Remote Script Execution
published: true
tags:
- diesunddas
summary: Scripts per SSH ausführen ist auf verschiedene (mal mehr, mal weniger sinnvolle) Weisen möglich.
---

Kürzlich kam ich in die Situation, dass ich auf einem RaspberryPi ein Script ausführen musste, welches ein angeschlossenes Gerät initialisieren sollte. Klar, nichts außergewöhnliches:

* per SSH anmelden
* Script ausführen
* fertig

Da diese Initialisierung aber später in einen extern ablaufenden Prozess auf einer anderen Maschine eingebunden werden soll, musste ein Weg her, die Initialisierung aus einem Prozess auf einem anderen (Windows) System anzustoßen.  

## PuTTY
Bei Windows und SSH landet man natürlich zwangsläufig bei [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/).  
PuTTY bietet einem nun verschiedene Möglichkeiten auf einem entfernten System mit aktiviertem SSH Zugang Skripte (bzw. beliebige Kommandos) auszuführen. Um dies zu demonstrieren legt man zuerst ein Python Skript auf dem Zielsystem mit folgendem Inhalt an:

{% highlight python %}
#!/usr/bin/python

print("Initialization successful...")
exit(0)
{% endhighlight %}  

Mit dem Kommandozeilenparameter `-m` kann man PuTTY nun eine lokale Datei übergeben, deren Inhalt als Kommandos innerhalb der aufzubauenden Verbindung interpretiert werden sollen. Angenommen das oben gezeigte Skript liegt als `initialize.py` im `home` Verzeihnis des Benutzers, der per SSH am entfernten System angemeldet wird, dann würde die folgende Datei `remote_commands.txt`

{% highlight bash %}
./initialize.py
{% endhighlight %}

mittels folgender Kommandozeile

{% highlight bash %}
putty -ssh -l fez -pw <PASSWORD> -m d:/tools/putty/remote_commands.txt 192.168.178.36
{% endhighlight %}

an PuTTY übergeben, zu folgendem Ergebnis führen:

![Command file result]({{ site.baseurl }}/images/putty_command_file_result.jpg "Command file result")

Die Ausführung eines Kommandos auf einem entfernten System funktioniert also soweit.  
Allerdings hat diese Vorgehensweise auch Nachteile.  
Zuerst ist es nicht sonderlich komfortabel alle auszuführenden Kommandos in speziellen Kommandodateien abzulegen, die dann als PuTTY Kommandozeilenparameter übergeben werden müssen. Bei einem oder zwei zu verwendenden Kommandos mag das noch gehen, aber irgendwann wird diese Herangehensweise unübersichtlich. Der weitaus größere Nachteil ist aber der, dass man keine Möglichkeit hat den Exit-Code und somit die erfolgreiche Abarbeitung des oder der Kommandos zu überprüfen.  

## Plink
Auftritt **Plink**.  
Plink (PuTTY Link) stellt eine kommandozeilenbasierte Schnittstelle zum PuTTY Backend dar und ist von der Funktionalität ähnlich dem bekannten `ssh`.

{% highlight python %}
#!/usr/bin/python

print("Initialization failed...")
exit(42)
{% endhighlight %}  
