---
layout: post
title: Installation von RubyMine unter Linux Mint 17.3
published: true
tags:
- entwicklung
- ruby
- rubymine
- mint
summary: Eine kurze Anleitung zur Installation von RubyMine unter Linux Mint 17.3 "Rosa"
---

Eine kurze Anleitung zur Installation von RubyMine unter Linux Mint 17.3 "Rosa". Der hier gezeigte Weg hat bei mir gut funktioniert. Es gibt aber sicherlich auch andere...

* TOC
{:toc}

## Oracle JDK installieren

### Entfernen aller 'Nicht - Oracle Java' Pakete
{% highlight bash %}
sudo apt-get update
sudo apt-get remove openjdk* icedtea* default-jre default-jdk gcj-jre gcj-jdk icedtea-{6..7}-plugin icedtea-plugin
{% endhighlight %}

### Aufräumen
{% highlight bash %}
sudo apt-get autoremove
sudo apt-get autoclean
{% endhighlight %}

### Hinzufügen des webupd8team Java Repository und Installation des Oracle Java SDK
[Install Oracle Java 8 in Ubuntu or Linux Mint via PPA repository](http://www.webupd8.org/2012/09/install-oracle-java-8-in-ubuntu-via-ppa.html)
{% highlight bash %}
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
{% endhighlight %}

## RubyMine installieren

### RubyMine Archiv herunterladen
[Download](https://www.jetbrains.com/ruby/download/)

### Erstellen des Zielverzeichnisses und Verschieben des Archivs
{% highlight bash %}
sudo mkdir /opt/rubymines
sudo mv ~/Downloads/RubyMine-X.Y.Z.tar.gz /opt/rubymines
{% endhighlight %}

### Archiv entpacken
{% highlight bash %}
cd /opt/rubymines
sudo tar -xzf RubyMine-X.Y.Z.tar.gz
sudo rm RubyMine-X.Y.Z.tar.gz
{% endhighlight %}

### Symlink Erstellen
Optional. Dies dient nur der Einfachheit.
{% highlight bash %}
sudo ln -nfs /opt/rubymines/RubyMine-8.0.3 /opt/rubymine
{% endhighlight %}

### Menüeintrag erstellen
{% highlight bash %}
sudo touch /usr/share/applications/jetbrains-rubymine.desktop
sudo nano /usr/share/applications/jetbrains-rubymine.desktop
{% endhighlight %}
Folgenden Inhalt einfügen:
{% highlight bash %}
[Desktop Entry]
Type=Application
Name=RubyMine
Icon=/opt/rubymine/bin/RMlogo.svg
Exec="/opt/rubymine/bin/rubymine.sh" %f
Comment=Develop with pleasure!
Categories=Development;IDE;
Terminal=false
{% endhighlight %}
Speichern... Schließen...

## Fertig
![Menu entry](/images/rubymine_menu.jpg "Menu entry")
