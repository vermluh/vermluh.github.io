---
layout: post
title: svn:externals und ein Umzug zu git
published: true
tags:
- entwicklung
- svn
- git
summary: Behandlung von svn:externals verlangen bei einem Umzug zu git nach kreativen Lösungsansätzen
---

## Der Hintergrund
Aufgrund der besseren Verfügbarkeit wollte ich einige meiner Projekte von einem lokal verwendeten Subversion Server in entsprechende Repositories auf Github umziehen. Dabei kam es zu einigen Problemchen, die ich so vorher nicht bedacht hatte. Diese möchte ich hier kurz darstellen. Natürlich hätte ich einiges davon umgehen können, wenn ich die betroffenen Projekte vor dem Umzug an die neuen Gegebenheiten angepasst hätte, aber das vorrangige Ziel war ein Umzug, der die Projekte erst einmal soweit wie möglich unangetastet lässt.  
