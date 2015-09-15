---
layout: post
title: Remote Script Execution
published: true
tags:
- diesunddas
summary: Scripts per SSH ausführen ist auf verschiedene (mal mehr, mal weniger sinnvolle) Weisen möglich.
---

* TOC
{:toc}

Kürzlich kam ich in die Situation, dass ich auf einem RaspberryPi ein Script ausführen musste, welches ein angeschlossenes Gerät initialisieren sollte. Klar, nichts außergewöhnliches:

* per SSH anmelden
* Script ausführen
* fertig

Da diese Initialisierung aber später in einen extern ablaufenden Prozess auf einer anderen Maschine eingebunden werden soll, musste ein Weg her, die Initialisierung aus einem Prozess auf einem anderen (Windows) System anzustoßen.  

## PuTTY
Bei den Themen Windows und SSH landet man natürlich zwangsläufig bei [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/).  
PuTTY bietet uns verschiedene Möglichkeiten auf einem entfernten System mit aktiviertem SSH Zugang Skripte (bzw. beliebige Kommandos) auszuführen. Um dies zu demonstrieren legt man zuerst ein Python Skript auf dem Zielsystem an. Folgender einfacher Inhalt soll für eine Demonstration ausreichen:

{% highlight python %}
#!/usr/bin/python

print("Initialization successful...")
exit(0)
{% endhighlight %}  

Die neu erstellte Datei noch ausführbar machen (`chmod +x ...`) und schon kann es losgehen.  
Mit dem Kommandozeilenparameter `m` kann man PuTTY nun eine lokale Datei übergeben, deren Inhalt als Kommandos innerhalb der aufzubauenden Verbindung interpretiert werden sollen. Angenommen das oben gezeigte Skript liegt als `initialize.py` im `home` Verzeihnis des Benutzers, der per SSH am entfernten System angemeldet wird, dann würde die folgende Datei `remote_commands.txt`

{% highlight bash %}
./initialize.py
{% endhighlight %}

mittels folgender Kommandozeile (der Pfad für den Parameter `m` muss natürlich an die jeweiligen Gegebenheiten angepasst werden)

{% highlight bash %}
putty -ssh -l fez -pw <PASSWORD> -m d:/tools/putty/remote_commands.txt 192.168.178.36
{% endhighlight %}

an PuTTY übergeben, zu folgendem Ergebnis führen:

![Command file result]({{ site.baseurl }}/images/putty_command_file_result.jpg "Command file result")

Die Ausführung eines Kommandos auf einem entfernten System funktioniert also soweit.  
Allerdings hat diese Vorgehensweise auch Nachteile.  
Zuerst ist es nicht sonderlich komfortabel alle auszuführenden Kommandos in speziellen Kommandodateien abzulegen, die dann als PuTTY Kommandozeilenparameter übergeben werden müssen. Bei einem oder zwei zu verwendenden Kommandos mag das noch gehen, aber irgendwann wird diese Herangehensweise unübersichtlich.  
Der weitaus größere Nachteil ist aber der, dass man keine Möglichkeit hat den Exit-Code und somit die erfolgreiche Abarbeitung des oder der Kommandos zu überprüfen.  

## Plink
Auftritt **Plink**.  
Plink (PuTTY Link) stellt eine kommandozeilenbasierte Schnittstelle zum PuTTY Backend dar und ist von der Funktionalität ähnlich dem von UNIX Systemen bekannten `ssh`.  
Um die Funktionsweise von Plink zu demonstrieren modifiziert man zuerst das eben erstellte Python Skript auf dem Zielsystem  folgendermaßen:

{% highlight python %}
#!/usr/bin/python

print("Initialization failed...")
exit(42)
{% endhighlight %}

Dieses modifizierte Skrip soll eine fehlgeschlagene Initialisierung auf dem Zielsystem simulieren. Dazu wird der Exit-Code des Skripts auf einen Wert ungleich 0 geändert. Bei der bisherigen Vorgehensweise des Aufrufs über den `m` Parameter und die Datei `remote_commands.txt` hätte man ohne weiteres keine Möglichkeit die erfolgreiche Abarbeitung der gewünschten Kommandos automatisiert zu überprüfen.  
Führt man das Skript aber nun über folgendes `plink` Kommando aus

{% highlight bash %}
plink.exe -ssh -pw <PASSWORD> fez@192.168.178.36 ~/error42.py
{% endhighlight %}

führt dies zu folgender Ausgabe:

![plink result]({{ site.baseurl }}/images/plink_command_result.jpg "plink result")

Über das bekannte

{% highlight bash %}
echo %ERRORLEVEL%
{% endhighlight %}

ist es nun auch möglich, den Rückgabewert der Kommandoausführung abzufragen und somit die erfolgreiche Abarbeitung automatisiert zu überprüfen.

![plink errorcode]({{ site.baseurl }}/images/plink_errorcode.jpg "plink errorcode")
