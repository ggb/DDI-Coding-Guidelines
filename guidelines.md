<!-- author: Jens Beckmann, Gregor Große-Bölting

email: beckmann@leibniz-ipn.de. ggb@informatik.uni-kiel.de

version: 0.0.1

language: de

narrator: US English Female

comment: https://vm077.test.rz.uni-kiel.de/?https://cloud.rz.uni-kiel.de/index.php/s/kkx3K8XSBG52iyY/download/guidelines.md -->

# Coding Guidelines: Gute Pattern - schlechte Pattern

<center><img src="https://imgs.xkcd.com/comics/good_code.png" style="height: 25em;" alt="XKCD: Good Code" />[^1]</center><br/>

Wie eine Studie des [Richard Paul Astleius-Instituts](https://www.youtube.com/watch?v=dQw4w9WgXcQ) zeigt, haben allein Bachelorstudierende für ihre Abschlussarbeiten im Jahr 2021 in Summe 25,7 Millionen Stunden an Arbeitszeit aufgewandt.[^2] Diese enorme Arbeitsleistung steht nicht im Verhältnis zu dem, was häufig aus den mühevoll angefertigten Projekten folgt: Die Arbeiten verstauben, Projekte werden nicht weitergeführt und für die Projekte geschriebener Code wird niemals eingesetzt.

Diese enorme Verschwendung von Lebenszeit ist betrüblich. Daher möchten wir, dass deine Prgrammierprojekte so gut und so lebensnah sind, dass wir sie in unsere größeren Projekte wie [CoMapEd](https://www.comaped.de/), [Levumi](https://levumi.informatik.uni-kiel.de/), usw. integrieren können. Damit das funktioniert, sind jedoch einige *best practices* zu beachten, die auch generell eine gute Praxis darstellen:

Programmierende verbringen deutlich mehr ihrer Zeit damit Code zu lesen als Code zu schreiben![^3] Lesbarer, verständlicher, gut strukturierter Code ist daher von großer Wichtigkeit. Das ist insbesondere dann der Fall, wenn man nicht mit einem Projekt von null anfängt, sondern eigenen Code in eine schon bestehende Struktur integriert: Diese folgt häufig einer eigenen, etablierten Logik, mit eigenen Konventionen, Hoffnungen und Wünschen.

Die folgenden Erläuterungen geben daher eine grobe Richtschnur, was man beachten sollte, um sich gut mit seinem Code in bestehenden Code zu integrieren, Projekte zu schreiben, die von anderen Programmierenden gut gelesen werden können und — was am wichtigsten ist — wie du Frust bei der Korrektur verhinderst und garantiert[^4] eine 1 bekommst.

[^1]: 'Good Code' by Randall Munroe available at https://xkcd.com/844/ licensed under a Creative Commons Attribution-NonCommercial 2.5 License.

[^2]: Obwohl diese Studie ganz klar ausgedacht ist, könnte sie fast stimmen: Wenn jeder, der etwa [257.000 Bachelorabsolventen](https://de.statista.com/themen/1159/studium/#dossierKeyfigures) in Deutschland 100h für seine Arbeit aufgewandt hat...

[^3]: "Indeed, the ratio of time spent reading versus writing is well over 10 to 1. We are constantly reading old code as part of the effort to write new code. ...[Therefore,] making it easy to read makes it easier to write." ― Robert C. Martin, Clean Code: A Handbook of Agile Software Craftsmanship, 2008

[^4]: Das ist natürlich nicht garantiert: Der Code muss nicht nur lesbar, sondern auch sinnvoll sein. Außerdem sollte er lauffähig sein und die Aufgabenstellung erfüllen; wir hoffen, dass versteht sich von selbst.

<div style="page-break-after: always;"></div>

## Ein paar generelle Dinge vorweg

Im Folgenden findet ihr viele Hinweise dazu, wie Code aussehen sollte. Diese Empfehlung können auf den ersten Blick sehr strikt und einschüchternd erscheinen. Das ist auf der einen Seite berechtigt, denn Code-Qualität ist wichtig und hochwertiger, gut dokumentierter Code gehört in der Informatik zu den [Grundsätzen guter wissenschaftlicher Praxis](https://www.uni-kiel.de/gf-praesidium/de/recht/ordner-gute-wissenschaftliche-praxis/cau-richtlinie-gute-wissenschaftliche-praxis)[^1]. Auf der anderen Seite werdet ihr sehen, das einige Sachen trotzdem vage sind und vielfach gute Empfehlungen gar nicht so einfach. Das liegt daran, dass Code- und Dokumentationsqualität zu einem Stück im Auge des Betrachters liegt bzw. auf der Aushandlung von Standards in einem Team von Entwickler:innen beruhen. Zwischen diesen beiden Extremen gilt es einen klugen Mittelweg zu finden. Im Zweifel hilft euch dabei die euch betreuende Person, die ihr natürlich jederzeit um Rat fragen könnt. 

Viele der hier angesprochenen Punkte drehen sich um die Lesbarkeit. Natürlich ist es am Ende des Tages ein Computer, der das Programm ausführt, aber in der Zwischenzeit müssen auch andere Menschen mit dem Code arbeiten – sei es, weil er bewertet, reviewed, erweitert oder überarbeitet werden muss. Deswegen bezieht sich Lesbarkeit hier immer auf Lesbarkeit durch andere Menschen.

Die Code-Beispiele weiter unten sind teils sinnloser Pseudo-Code, teils Beispiele aus der Praxis. Was was ist, musst du entscheiden :-)

<center><img src="https://imgs.xkcd.com/comics/estimating_time_2x.png" style="height: 16em;" alt="XKCD: Estimating Time"/>[^2]</center><br/>

[^1]: Dazu ist [dieser Artikel](https://forschungsdaten.info/themen/ethik-und-gute-wissenschaftliche-praxis/softwareentwicklung-und-gute-wissenschaftliche-praxis/) bei [forschungsdaten.info](https://forschungsdaten.info/) sehr informativ und hilfreich!

[^2]: 'Estimating Time' by Randall Munroe available at https://xkcd.com/1658/ licensed under a Creative Commons Attribution-NonCommercial 2.5 License.

<div style="page-break-after: always;"></div>

### Englisch

In der Softwareentwicklung wird so gut wie immer auf Englisch kommuniziert: Dies gilt für Commit Messages, Benennung von Variablen oder Git-Branches wie auch für Kommentare. 

Unabhängig von den historischen Gründen arbeiten an einer Software häufig auch Personen, für die nicht Deutsch die Muttersprache ist. Dabei hat sich Englisch als *lingua franca* bewährt. Dies sollte bei allem beachtet werden, was Eingang in ein Repository findet.

### Plagiate

> ACM defines plagiarism as the misrepresentation of another's writings or other creative work (including unpublished and published documents, data, research proposals, computer code, or other forms of creative expression, including electronic versions) as one's own. […] Plagiarism manifests itself in a variety of forms, including:
>
> • verbatim copying, near-verbatim copying, or intentionally paraphrasing portions of another's work;
>
> • copying elements of another's work, such as equations, tables, charts, illustrations, presentation, or photographs that are not common knowledge, or copying or intentionally paraphrasing sentences without proper or complete source citation;
>
> • verbatim copying of portions of another's work with incorrect source citation
>
> \-- [ACM Policy on Plagiarism, Misrepresentation, and Falsification](https://www.acm.org/publications/policies/plagiarism-overview)

Abschlussarbeiten sollen eine eigenständige wissenschaftliche Leistung darstellen. Daher ist es nicht okay sein Projekt allein aus Stackoverflow-Snippets zusammen zu kopieren: Eine eigene Leistung muss erkennbar sein. 

Das heißt allerdings nicht, dass man gar keinen Code von anderen, bspw. aus Dokumentationen von Softwarebibliotheken, übernehmen darf! Wenn man Code übernimmt, muss dies jedoch deutlich kenntlich gemacht werden. Ein Kommentar im Code, der die Quelle angibt, zusammen mit einem Datum, genügt. 

Sollten Zweifel daran bestehen was wie auszuzeichnen ist und zu welchem Grad die übernahme von Fremd-Code in Ordnung ist, kontaktiert die betreuende Person für eine Klärung.

## git

In größeren Software-Projekten ist der Einsatz einer Versionsverwaltung Standard, da nur so eine reibungslose Zusammenarbeit mit mehreren Entwicklern gewährleistet werden kann. Die Versionsverwaltung "merkt" z. B. wenn zwei Entwickler an dieselbe Datei ins Repository[^1] einchecken wollen, und versucht, die Änderungen bestmöglich unter einen Hut zu bringen. Weiterhin speichert die Versionsverwaltung alle Änderungen auf eine nachvollziehbare Weise, so dass es problemlos möglich ist, zu einer früheren Version zurückzuspringen.

Aber auch bei kleineren Standalone-Projekten bringt der Einsatz einer Versionsverwaltung Vorteile. Zusätzlich zur Dokumentation der Arbeitsschritte und einfachem Rollback ist ein Remote Repository auch ein Backup, falls mal der Kaffee ins Laptop läuft. 

Weiterführende Informationen zur Funktionsweise von und Arbeit mit git sind [haufenweise im Internet](https://www.google.com/search?q=git+f%C3%BCr+anf%C3%A4nger) zu finden. Beispielsweise gibt es einen interaktiven Kurs, um git zu lernen, bei [Codecademy.com](https://www.codecademy.com/learn/learn-git).

<center><img src="https://imgs.xkcd.com/comics/git_commit_2x.png" style="height: 20em;" title="XKCD: Git Commit" />[^2]</center><br/>

[^1]: **Repository**, häufig auch kurz *Repo*, bezeichnet ein Verzeichnis oder Archiv, in dem Code und andere Dateien gespeichert werden. Ist das Repository auf dem eigenen Rechner, dann ist es das *lokale Repository*; bei der er auf einem Server abgelegten Spiegelung des lokalen Arbeitsstands, spricht man von einem *Remote Repository*.

[^2]: 'Git Commit' by Randall Munroe available at https://xkcd.com/1296/ licensed under a Creative Commons Attribution-NonCommercial 2.5 License. 

<div style="page-break-after: always;"></div>

### Commit Messages

Eine Commit Message (die bei Verwendung von `git commit` mit dem Parameter `-m` angegeben wird) kann aus einer einzelnen Zeile bestehen, sie kann aber auch eine mehrzeilige Nachricht (*Body*) mit weiterführenden Informationen sein.

Für Commit Messages gilt:

* Sie sollten so aussagekräftig wie möglich sein: Wenn eine Zeile nicht ausreicht, kann auch der Body verwendet werden.
* Wenn ein Ticketsystem verwendet wird, sollte die Ticketnummer in der Commit Message auftauchen.
* "Arghg, es ist alles so kaputt" oder "Next try" mögen die aktuelle Befindlichkeit gut widerspiegeln, sind aber keine guten Commit Messages.
* Gleiches gilt für "...", "cont'd" und ähnliche Nachrichten.

```bash
git commit -m "412 Fix email header"
```

### Branchnamen

Branchnamen sollten die Aufgabe widerspiegeln, die im Branch bearbeitet wird. Das Format hängt dabei stark vom Projekt bzw. vom Team ab, der Branchname sollte aber aber auf einen Blick ersichtlich machen, was das Thema des Branches ist.

**Beispielformat:** 

<category>/<author>\_<ticketno>\_<description>

**Beispiel:**

`feature/max_mustermann_129_simultaneous_editing`

`hotfix/382_mail_bug`

vs.

`bachelorarbeit` (<= nicht gut!)

Insbesondere der Benutzername ist nicht unwichtig, ansonsten kann es am Ende schwierig werden, wenn es heißt "Stell mal das Bachelorprojekt von Max Mustermann live".

Weiterführende Informationen zu (sinnvollen) Möglichkeiten Branches zu benennen, finden sich in diesem [lesenswerten Stackoverflow-Thread](https://stackoverflow.com/questions/273695/what-are-some-examples-of-commonly-used-practices-for-naming-git-branches). 

<div style="page-break-after: always;"></div>

### .gitignore

Die `.gitignore` ist eine gleichnamige Datei, die im Wurzelverzeichnis jedes Git-Projekts angelegt werden sollte. In der `.gitignore` werden Verzeichnisse/Dateien aufgeführt, die nicht ins Repository gehören. Dies sind z. B. alle Dateien, die während der Entwicklung entstehen, aber KEIN Bestandteil des Source Codes sind:

* Logfiles
* sqlite-Dateien oder Datenbank-Dumps
* installierte Pakete (z. B. `node-modules`)
* in der Develop-Umgebung kompilierte Assets

Eine gute `.gitignore` sorgt dafür, dass das Repository klein bleibt und unnötige Dateien nicht in der Versionsverwaltung sind. Dadurch wird die Arbeit mit dem Repository deutlich schneller und angenehmer für alle Beteiligten (bspw. diejenigen, die euer Projekt bewerten!).

Eine Sammlung von Beispiel-.gitignores für verschiedene Programmiersprachen und Projektarten gibt es bei [GitHub](https://github.com/github/gitignore).

### Abgabe von git-Repositories

Auch wenn die Prüfungsordnungen in der Informatik die Abgabe von git-Repos nach wie vor nicht vorsieht, hat es sich als gängige Praxis etabliert und ist vollkommen in Ordnung: Bitte kramt nicht eure DVD-Brenner für die Abgabe eurer Abschlussarbeit heraus. 

Am besten verwendet ihr von vornherein die Gitlab-Instanz des IfI. Dort habt ihr als Studierende der Informatik die Möglichkeit selbst Repositories anzulegen. Außerdem könnt ihr die Betreuer der Arbeit als Mitglieder hinzufügen, dadurch haben sie automatisch die Möglichkeit euren Code einzusehen. 

Eure (gedruckte) Arbeit sollte im Anhang zumindest einen Link auf das Repo enthalten. Ihr solltet sicherstellen, dass jede Person, die den Link besitzt, das Repository einsehen kann.

<div style="page-break-after: always;"></div>

## Dokumentation

<center><img src="https://imgs.xkcd.com/comics/manuals_2x.png" style="height: 10em;" title="XKCD: Manuals" />[^1]</center><br/>

Funktionen/Methoden sollten einen Header erhalten, in dem zumindest grob umrissen ist, was sie tun. Außerdem sollten die Parameter mit Typ und Beschreibung enthalten sein. Beispiel ([Quelle](https://www.programiz.com/python-programming/docstrings)):

```python
def add_binary(a, b):
    '''
    Returns the sum of two decimal numbers in binary digits.

            Parameters:
                    a (int): A decimal integer
                    b (int): Another decimal integer

            Returns:
                    binary_sum (str): Binary string of the sum of a and b
    '''
    binary_sum = bin(a+b)[2:]
    return binary_sum
``` 

Häufig kann aus solchen umfangreichen Kommentaren automatisch eine Dokumentation erstellt werden. Die Kommentare müssen dafür allerdings einem bestimmten Muster folgen. Eine Liste gängiger Generatoren findet sich bspw. bei der [Wikipedia](https://en.wikipedia.org/wiki/Comparison_of_documentation_generators).

Nicht sofort verständlicher Code sollte mit Inline-Kommentaren versehen werden. Dabei soll vor allem beschrieben werden, warum die betreffende Zeile an dieser Stelle notwendig ist, nicht, was sie tut – das sollte aus dem Code ersichtlich sein. Beispiel:

```python
# doppelte Leerzeichen erzeugen leere Listenelemente, diese werden herausgefiltert
g = [s for s in g if s != ""]
```

Ist eine Zeile so komplex und schwer lesbar, dass ein Kommentar zum Verständnis notwendig wäre, dann ist es in der Regel besser, den Ausdruck in mehrere Ausdrücke aufzuteilen. 

Außerdem ist darauf zu achten, dass wenn in einem Projekt gearbeitet wird, der bisherige Kommentarstil berücksichtigt und beibehalten werden sollte. 

[^1]: 'Manuals' by Randall Munroe available at https://xkcd.com/1343/ licensed under a Creative Commons Attribution-NonCommercial 2.5 License. 

## Deployment

Falls das Projekt auf einem Server deployed werden muss, darf eine Beschreibung der Infrastruktur und der notwendigen Schritte nicht fehlen. Diese sollte sowohl in einer `README.md` im Wurzelverzeichnis zu finden sein, als auch im Anhang der (gedruckten) Arbeit.

Die folgenden Dinge müssen dabei unbedingt berücksichtigt werden:

* benötigte Software und Programmiersprachen
* benötigte Softwarepakete; sollten diese nicht über die für die Programmiersprache typische Paketverwaltung verfügbar sein, dann ist auch eine Installationsanleitung für die jeweiligen Pakete mitzugeben (sofern diese nicht selbsterklärend ist)
* notwendige Umgebungsvariablen
* ggf. benötigte zusätzliche Infrastruktur (Datenbanken, VMs, Docker)
* ggf. benötigte Services (Mailserver, Reverse Proxy, Datenbank, Load Balancer etc.)

<div style="page-break-after: always;"></div>

## Code Quality

> Always code as if the guy who ends up maintaining your code will be a  
> violent psychopath who knows where you live.
>
> \-- [John F. Woods, 1991](https://groups.google.com/g/comp.lang.c++/c/rYCO5yn4lXw/m/oITtSkZOtoUJ)

"Guter" Code ist häufig etwas, auf das sich ein Team im Laufe der Zusammenarbeit verständigt hat; eine objektive Kennzahl für guten Code lässt sich schwer bilden. Eine Reihe von Empfehlungen, die in der Regel zu besserem Code führen, ist im Folgenden aufgelistet.

<center><img src="https://imgs.xkcd.com/comics/code_quality_2x.png" style="height: 12em;" title="XKCD: Code Quality" />[^1]</center><br/>

[^1]: 'Code Quality' by Randall Munroe available at https://xkcd.com/1513/ licensed under a Creative Commons Attribution-NonCommercial 2.5 License. 

### State of the Art

> ART. 1 FACHKOMPETENZ Das GI-Mitglied eignet sich den Stand von Wissenschaft und Technik in seinem Fachgebiet an, berücksichtigt ihn und kritisiert ihn konstruktiv. Das GI-Mitglied verbessert seine Fachkompetenz ständig.
>
> \-- [Die Ethischen Leitlinien der Gesellschaft für Informatik](https://gi.de/ueber-uns/organisation/unsere-ethischen-leitlinien)

Beschäftige dich mit der Sprache und der generellen Infrastuktur (Framework, Bibliotheken). Wenn du in einem bestehenden Projekt arbeitest, solltest du nicht blind Code kopieren, der eventuell schon Jahre alt ist und nicht mehr dem Stand der Technik entspricht. Im Zweifel sprich mit deinem Betreuenden.

### Linting und Prettying

Ein **Linter** ist ein statisches Analysetool, das den Entwickler dabei unterstützt, besseren Code zu schreiben. Insbesondere bei interpretierten Sprachen wie Javascript kann ein Linter vor Laufzeitfehlern schützen, da der Linter potentielle Fehlerquellen bereits beim Schreiben des Codes bemerkt und darüber informiert, bevor sie im Browser auftreten. Es ist auch möglich, eine Git-Pipeline einzurichten, die Commits nur erlaubt, wenn der Linter fehlerfrei gelaufen ist. Je nach verwendeter IDE kann der Linter auch so eingerichtet werden, dass er automatisch bei Texteingabe oder beim Speichern einer Datei ausgeführt wird.

Eine Liste von Lintern fürs vers. Programmiersprachen, findet sich bei [GitHub](https://github.com/caramelomartins/awesome-linters). Bei den jeweiligen Projektseiten finden sich in der Regel Hinweise dazu, wie man den Linter für seine bevorzugte IDE einrichtet. 

**Prettying** sorgt für eine einheitliche, automatische Formatierung des Codes, z. B. Einrückung, Verwendung von optionalen Leerzeichen oder Zeilenumbrüchen an bestimmten Stellen, die Verwendung von " vs ' etc. Die Grenzen zwischen Linting und Prettying sind etwas fließend, beispielsweise bei sprachspezifischen Konventionen wie der Schreibweise von Variablen- oder Funktionsnamen in `camelCase`, `snake_case` oder `PascalCase`.

Bei existierenden Projekten mit eingerichtetem Linting/Prettying sollte dieses verwendet, ansonsten mit Augenmaß selbst eingerichtet werden. Für die meisten Sprachen/Frameworks gibt es empfohlene Rulesets. Außerdem gibt es auch hier eine Liste von Prettiern für vers. Programmiersprachen bei [GitHub](https://github.com/rishirdua/awesome-code-formatters).

### Namen

> There are 2 hard problems in computer science: cache invalidation, naming things, and off-by-1 errors.
>
> \-- https://martinfowler.com/bliki/TwoHardThings.html

Variablen, Funktionen, Objekte, Methoden etc. sollten so benannt werden, dass im Kontext sofort klar ist, was sie beinhalten. 

Es hat sich als gute Praxis etabliert, dass Booleans mit `is`, `has` o. Ä. beginnen. Ebenso sollten Getter/Setter mit `get...`/`set...` anfangen.

Funktionen sollten so benannt werden, dass man beim Lesen eines Aufrufs weiß, was sie tun, ohne den Code selber anschauen zu müssen; es sollte nicht mehr passieren als sich aus dem Namen unmittelbar ergibt.

**Weitere Beispiele:**

```javascript
if (hasValidationError) {
	// render error message
}
```

```javascript
const currentUser = getUserById(currentId)

// vs

const current = user(id)
```

Eine anschauliche Erklärung findet sich dazu hier: 

<iframe width="560" height="315" src="https://www.youtube.com/embed/-J3wNP6u5YU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

### Länge von Funktionen, Methoden und Klassen

<center><img src="https://imgs.xkcd.com/comics/random_number.png" style="height: 10em;" title="XKCD: Random Number" />[^1]</center><br/>

Eine Funktion oder Methode sollte nach Möglichkeit nur eine einzelne Aufgabe ausführen und entsprechend benannt sein.

Bei mehr als sieben[^2] Zeilen Code sollte man sich Gedanken machen, ob es sinnvoll ist, eine Funktion oder Methode in mehrere, kleinere Funktionen/Methoden aufzuteilen. Je nach Kontext können das mal mehr, mal weniger Zeilen sein – in einem Controller, der einen Datensatz aus der Datenbank holt und ans Frontend liefert, werden das sehr wenige, in einem Javascript-Framework können das auch schon mal ein paar mehr Zeilen sein. 

Sieben Zeilen sind entsprechend keine harte Grenze: Ab da sollte man sich Gedanken machen, aber es kann (und wird) Fälle geben, in denen eine längere Funktion sinnvoll ist und eine Aufteilung unnötig. 

[^1]: 'Random Number' by Randall Munroe available at https://xkcd.com/221/ licensed under a Creative Commons Attribution-NonCommercial 2.5 License. 

[^2]: Warum sieben? Menschen können etwa fünf bis neun Gegenstände gleichzeitig in ihrem Arbeitsgedächtnis vorhalten. Da erscheint sieben doch eine ganz okayene Maßzahl...

<div style="page-break-after: always;"></div>

### Schachtelungstiefe

Je tiefer die Statements in einem Block geschachtelt sind, desto schwerer ist der Block zu lesen.

Im Beispiel sollten die einzelnen Statements in eigene Funktionen ausgelagert werden. Im Falle von `load()` `message()` scheint dies schon geschehen zu sein, kann aber noch weiter vorangetrieben werden.

```javascript
for (let i = 0; i < user.length; i++) {
  if (user[i] === 'admin') {
    for (let o = 0; 0 < user[i].capabilites.lengths; o++) {
      if (o > 20) {
        load(20)
      } else {
        switch (o) {
          case 0:
            if (i === 4)
              load(o + 4)
            break
          case 1:
            load(o + 3)
            break
          case 2:
            load(o + 2)
            break
          case 3:
            load(o + 1)
            break
        }
        if (example[o] !== 'admin') {
          // TODO
        } else {
          load(user[i].capabilites.length)
        }
      }
    }
  } else {
    message('not admin')
  }
}
```

Eine Schachtelungstiefe von 4 oder mehr ist in der Regel nicht sinnvoll und sollte vermieden werden. 

Das folgende Video veranschaulicht dies sehr schön mit einem Disgust-O-Meter und gibt konkrete Hilfestellungen, wie man die Schachtelungstiefe mit zwei einfachen Techniken reduzieren kann:  

<iframe width="560" height="315" src="https://www.youtube.com/embed/CFRhGnuXG-4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


### Komplexität von Ausdrücken

Einzelne Ausdrücke können je nach Sprache und Geschmack sehr komplex werden. Allerdings wird ein Ausdruck, je komplexer er wird, auch immer schwerer lesbar. Generell gilt: wenn man etwas von einer auf fünf Zeilen aufteilt, und es dafür hinterher besser lesbar ist, ist das besser. Wir sind hier nicht auf dem [Golfplatz](https://de.wikipedia.org/wiki/Codegolf).

**Beispiel:**

```python
# nicht gut: 
for val, count in counts.iteritems():
  entr += count / n * entropy(df.where(df[attribute_name] == val)[target_name].dropna())

# besser:
for val, count in counts.iteritems():
  # get correct column
  column = df.where(df[attribute_name] == val)[target_name]
  # drop NA values
  column_without_nas = column.dropna()
  # update summed entropy
  entr += count / n * entropy(column_without_nas)
```

<div style="page-break-after: always;"></div>

## Wartbarkeit

<center><img src="https://imgs.xkcd.com/comics/future_self_2x.png" style="height: 20em;" title="Future Self" />[^1]</center><br/>

Sollte der Code irgendwo live gestellt werden, ist die Wahrscheinlichkeit recht hoch, dass jemand anders ihn später noch anfassen muss. 

Wenn man seinen eigenen Code vier Wochen später wieder anguckt und nicht versteht, wie das jemals funktionieren konnte, ist es sehr wahrscheinlich, dass es anderen Personen auch so geht. Keine Sorge, das geht jedem Programmierer mal so :-)

[^1]: 'Future Self' by Randall Munroe available at https://xkcd.com/1421/ licensed under a Creative Commons Attribution-NonCommercial 2.5 License. 

### DRYness

"**D**on't **r**epeat **y**ourself."

Häufig wiederholt sich Code – spätestens beim zweiten Mal copy/paste eines Blocks sollte man überlegen, inwieweit man den Block sinnvoll in eine Funktion auslagern kann.

Zum Beispiel das Feststellen von Nutzerrollen:

```javascript
const canEditTests = capabilities?.includes('editTest') || capabilities?.includes('admin')
```

Dies lässt sich prima in eine Funktion auslagern:

```javascript
export const hasCapability = (capability, capabilities) => capabilities?.includes(capability) || capabilities?.includes('admin')
```

Der Aufruf erhöht zum einen die Lesbarkeit, zum anderen kann die Funktion auch mit anderen Nutzerrollen verwendet werden.

```javascript
const canEditTest = hasCapability("editTest")
const canViewTest = hasCapability("viewTest")
```

Auch hier muss man mit Augenmaß agieren: Manchmal kann es durchaus sinnvoll und lesbarer sein, wenn man Doppelungen im Code zulässt. Generell sollten diese aber durch sinnvolle Abstraktionen vermieden werden.

<div style="page-break-after: always;"></div>

## Weiteres

Die folgenden Punkte gehören zwar auch zur Softwareentwicklung, sind aber für Abschlussarbeiten bis auf die Code Review nur bedingt relevant und deshalb nur der Vollständigkeit aufgeführt.

### Code Review

Eine **Code Review** ist ein weiteres Instrument zur Sicherstellung der Code Quality. Meist findet diese im Rahmen eines Merge Requests statt, also bevor neuer oder überarbeiteter Code in die Codebasis aufgenommen wird.

Dabei wird der Code von einem zweiten Entwickler begutachtet, der ggf. Rückfragen stellt, die meist zu Überarbeitungen des Codes führen. Welchen Umfang eine solche Code Review hat, unterscheidet sich von Team zu Team sehr stark - von "Scheint zu funktionieren und es gibt keine console.logs" bis zu "Ich gehe den Merge Request Commit für Commit durch, und lese und verstehe jede Zeile" kann alles vorkommen. Dies sind natürlich die Extreme - hier sollte ein Weg gefunden werden, der die Codequalität sicherstellt und für das Team akzeptabel ist.

Eine andere Form der Code Review können auch wöchentliche Developer-Meetings sein, in denen ein Code-Abschnitt vorgestellt und diskutiert wird.

Wenn im Rahmen eines Abschlussprojektes an einem Produktivsystem gearbeitet wird, sollte nach Möglichkeit in Absprache mit dem Betreuenden eine Code Review stattfinden.

<center><img src="https://www.osnews.com/images/comics/wtfm.jpg" /></center><br/>

### Refactoring

Refactoring bezeichnet Umstrukturierungen des Codes, ohne die ursprüngliche Funktion zu verändern. Das Ziel dabei ist es den Code besser les- und wartbar zu machen, oder die Performance zu verbessern. Dinge, die im Rahmen eines Refactorings stattfinden können:

* Variablen/Funktionen sprechender benennen
* Code besser strukturieren
* Beseitigung von ungenutztem Code

Um sicherzustellen, dass die Software hinterher tatsächlich noch so funktioniert wie vorher, ist es sinnvoll, möglichst umfangreiche Tests einzurichten, und diese während des Refactorings regelmäßig laufen zu lassen.

### Tests

Hiermit ist nicht das händische Durchtesten einer Anwendung gemeint, sondern das automatische Testen von z. B. Schnittstellen, API-Endpunkten oder Rückgabewerten.

Unit-Tests werden dabei mit einem vordefinierten Satz an Eingabedaten (Fixtures) durchgeführt, zu denen jeweils das erwartete Ergebnis hinterlegt ist. Führt eine Code-Änderung dazu, dass das Ergebnis nicht mehr der Erwartung entspricht, schlägt der Test fehl.

Beispiel:

```javascript
Fixture: users = [
  {name: 'John', val1: 25, val2: 167}, 
  {name: 'Julia', val1: 27, val2: 187}, 
  {name: 'Jimmy', val1: 12, val2: 120}
]

// Zu testende Funktion:
function getOverallVal1() {
  return users.reduce((acc, user) => acc + user.val1, 0)
}

// Erwartung: 64 (alle val1 addiert)
```

Wird die Funktion verändert, z. B. so (-> user.val2 statt user.val1 im reduce)

```javascript
function getOverallVal1() {
  return users.reduce((acc, user) => acc + user.val2, 0)
}
```

würde der Test ein Ergebnis 64 erwarten, bekommt aber 474 von der Funktion zurück. Der Test schlägt dann fehl.

Im Optimalfall werden die Tests von einer Git-Pipeline ausgeführt, so dass es nur möglich ist, Code ins Repository zu pushen, wenn alle Tests vollständig fehlerfrei durchlaufen.
