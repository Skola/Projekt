SKOLA

Skola is a MVC inspired framework. This document will show you how to install and how to configure runimentary functionality. This document will continue in swedish.

Installation/Setup

För att klona Skola från GitHub så behöver du först installera Git Bash eller Git GUI på din dator. Git Bash/ Git GUI nedladdningar går att hitta på följande länk: http://git-scm.com/downloads

För att sedan använda dig av Skola så behöver du ett filredigeringsprogram för webbfiler så som Dreamweaver eller jEdit. Där finns fler alternativ på internet.

När du har laddat ner Git Bash eller Git GUI och installerat klart så öppnar du programmet. Den här guiden kommer vidare att utgå från att du använder dig av Git Bash.

1. Välj mapp/skapa mapp

Skriv in koden nedanför i Git Bash för att öppna en mapp; utelämna dollar-tecknet då den endast utmärker Bash kod:

$ cd Your_desired_loaction  

Du kommer automatiskt hamna i C:/User/UserName om du installerat Git Bash på C:. För att gå upp ett eller flera steg så använder du två punkter, ett par för varje mapp, som i exemplet nedan där man gått från C:/User/Username till C:/wamp/www/Projekt:

$ cd ../../C/wamp/www/Projekt

Alternativt skapa en ny mapp på den önskade platsen...:

$ mkdir FolderName

Och öppnar den:

$ cd FolderName

2. Klona

Sedan så klonar du Skola till den valda mappen från GitHub med koden nedan:

$ git clone git://github.com/Skola/Projekt.git

Projekt kommer att läggas i en egen mapp, i mappen som du tidigare valt. Nu har du Skola inlagt på din dator!

3. RewriteBase

Öppna filen .htaccess i Projekt i ett webbfil-hanteringsprogram så som Dreamweaver eller jEdit. Ändra RewriteBase /~your/base/file/location/Projekt/ till där Projekt mappen ligger på din server eller i dina lokala filer.

4. Göra databasen skrivbar

Gör Skola databasen skrivbar genom att öppna Skola-Framework mappen i Git Bash, om den inte redan är öppen (du ser detta i den gula texten efter den gröna namntexten), och ändra chmod till 777 på site/data:

$ cd Projekt; chmod 777 site/data 

I vissa fall, om man har lokala filer och sedan drar över dessa till en extern server så kan man behöva ändra chmod på servern manuellt. För att dra över filer till en server så kan man använda programmet Filezilla. På dina serverfiler;gå in på Projekt/site/data och gör en chmod 777 på data-mappen.

5. Öppna i webbläsaren och initiera

Öppna ramverkets index-fil genom att peka på den i webbläsaren med adressändelsen: www.your.server.se/your/base/file/location/Projekt/

För att sedan installera Projekt initierar du databasen genom att klicka på länken längst ner under rubriken "Installation" som heter module/install.

Ramverket är installerat och klar för användning!
Konfiguration
Utseende CSS

För att ändra utseendet på Skola så öppnar du Projekt/site/themes/mytheme/style.css i en filredigerare, till exempel Dreamweaver eller jEdit. I style.css så ligger det ett antal tomma css referenser som exempel för vad som kan redigeras på ramverket. Du kan bland annat ändra färg på bakgrund och html, text storlek och färg, navigeringsmenyn, titel, sidhuvud, sidfot med mera. Ramverkets grund CSS hittar du på Projekt/themes/grid/style.css.
Layout

För att ändra webbsidans layout i mer drastiska drag så kan du gå in på filen index.tpl.php i Projekt/themes/grid/index.tpl.php - fast det är rekommenderat att hålla sig till att justera CSS-filen, som nämnt i ovanstående stycke, om man precis börjat bekanta sig med Skola ramverket.
Sidfot

För att ändra texten på sidfoten så öppnar du filen Projekt/themes/functions.php. För att ändra copyright texten så får du istället gå in på Projekt/site/config.php och ändra denna längst ner i config.php på rad 181.
Ändra fixerade delar av webbsidan så som titel och logotyp

För att byta logotyp eller favicon så behöver du öppna filen Projekt/site/config.php och ändra bilden. Här går det även att ändra webbsidans titel, slogan, logotypstorlek samt footer information.
Skapa en egen webbsida

Som standard så ligger det tre menyalternativ för skapandet av den egna webbsidan: About me, My work samt Guestbook. För att konfigurera dessa filer så kan du öppna en utav dessa template-filer i Projekt/site/src/CCMycontroller; blog.tpl.php, guestbook.tpl.php, page.tpl.php.

För att lägga till eller byta titel på någon utav menyalternativen för den egna webbsidan så behöver du öppna filen Projekt/site/config.php och ändra informationen, " 'my-navbar' => array( " . Här kan du ta bort menyalternativ eller lägga till för att justera antalet sidor på din webbsida. Hur du vidare lägger till en ny sida beskrivs mer ingående i nästa sektion.
Lägga till en ny sida

För att lägga till en ny sida så krävs det att man redigerar tre filer: CCMycontroller.php, config.php samt sidan du vill ha in.

Följ stegen nedan för att lära dig hur man lägger till en ny sida till din webbsida.
CCMycontroller.php

Om du vill lägga till en ny sida till din hemsida så börjar du med att öppna Projekt/site/src/CCMycontroller/CCMycontroller.php. I början av dokumentet, så finns tre rubriker som lyder "The page about me", "The blog" och "The guestbook". Under dessa rubriker så finns det var sin publik funktion som sköter presentationen av var och en av dem. Här lägger du till en ny publik funktion för att börja skapa en ny sida. Här nedan finns ett exempel på hur koden för "About me" sidan ser ut, under rubriken "The page about me":


/**
* The page about me
*/
 public function Index() {
    $content = new CMContent(5);
    $this->views->SetTitle('About me'.htmlEnt($content['title']))
                ->AddInclude(__DIR__ . '/page.tpl.php', array(
                  'content' => $content,
                ));
  }

Det som behöver ändras är alltså numret i $content = new CMContent(5), titlen 'About me' samt '/page.tpl.php'. Rubriken "The page about me" är inte nödvändig för att koden ska fungera utan för att hålla ordning på innehållet och dokumentationen. Säg att vi skapar en sida som visar upp allt vårt arbete, då tar man bort numret (numret hänvisar till en databastabell i CMContent, vilket håller i default texter för ramverket), titlen 'My work', sid-filen 'page2.tpl.php' och rubriken "The page about my work":


/**
* The page about my work
*/
  public function Index() {
    $content = new CMContent();
    $this->views->SetTitle('My work'.htmlEnt($content['title']))
                ->AddInclude(__DIR__ . '/mywork.php', array(
                  'content' => $content,
                ));
  }

config.php

Nästa fil som behöver ändras är Projekt/site/config.php. Öppna den så finns det en kodrad som lyder: $ly->config['menus']. För att ändra webbsidans meny så behöver du gå ner till: 'my-navbar' => array(, varav därunder redan finns tre alternativ: 'home', 'blog' samt 'guestbook':


     'my-navbar' => array(
         'home' => array('label'=>'About Me', 'url'=>'my'),
         'blog' => array('label'=>'My Blog', 'url'=>'my/blog'),
         'guestbook' => array('label'=>'Guestbook', 'url'=>'my/guestbook'),

Det sista som behöver göras är att skapa en ny php fil, med önskat namn. Du kan skapa den här filen antingen genom att kopiera page.tpl.php eller skapa en tom php fil och fylla med den html och php kod som än vill.

Det som är speciellt med page.tpl.php är koden som finns där gör det möjligt att redigera sidans innehåll på webben. Allt beror på vad som passar bäst för användarens behov. page.tpl.php ligger i PRojekt/site/src/CCMycontroller. Spara alla uppdateringar och öppna Skola ramverket online på adressen: www.your.server/Projekt/index.php. 
