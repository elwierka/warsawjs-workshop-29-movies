# warsawjs-workshop-29-movies
## Biblioteka z filmami

### <b>Features:</b>
- dodawanie/usuwanie/wyświetlanie filmów z pliku
- tworzenie komponentów zagnieżdżonych
- dowanie zewnętrznych bibliotek (Bootstrap, Angular Material)


## Przygotowanie środowiska

1. Utwórz konto na GitHubie. 
2. Zainstaluj node.js (current Version) - https://nodejs.org/en/.  
Razem z node.js, zainstaluje się npm (Node Package Manager)
3. Zainstaluj Angular CLI - https://cli.angular.io/.

W projekcie będziemy używać Angular CLI - Command Line interfejs dla Angulara. Jest wiele zalet używania Angular CLI:
* pomaga developerom aplikacji w ich budowaniu (zestaw poleceń pozwala szybko tworzyć aplikację)
* generuje pliki Angulara (moduły, komponenty, interfejsy, serwisy, routery itd.)
* wykonuje testy i pomaga w deployu aplikacji Angularowych
 
Samodzielne pisanie aplikacji wymaga więcej pracy, związanej z tworzeniem plików, importowaniem, nazewictwiem, bundlowaniem itp.

## Instalacja Angular CLI

* otwórz terminal lub okno poleceń i wpisz:

```JavaScript
npm install -g @angular/cli
```
Robimy to tylko raz. Komenda zainstaluje Angular CLI globalnie, dzięki czemu będziesz mógł go użyć z każdego folderu.

Używając Angular CLI, wykorzystujemy jego składnię, polecenia "ng" z nazwą taska, który chcemy wykonać.

## Lokalny server JSON-SERVER

W naszej aplikacji będziemy pracować z REST API, potrzebujemy więc czegoś, co działa jak serwer i pozwala dokonywać żądań HTTP.


### Instalacja JSON-SERVER

1. Otwórz terminal/command line i wpisz poniższą komendę:

```JavaScript
npm install -g json-server
```

Robimy to tylko raz. Polecenie zainstaluje json-server globalnie.


2. Gdy json-server się zainstaluje, możemy utworzyć testowy plik db.json. Ten plik będzie zawierał dane zapisane w formacie JSON, które powinny być wystawione przez REST API. Będzie to nasza lokalna baza danych.

Dla testu - utwórz w folderze aplikacji plik db.json a następnie wklej do niego zawartość:

```JavaScript

{
    "employees": [
    {
        "id": 1,
        "first_name": "Sebastian",
        "last_name": "Eschweiler",
        "email": "sebastian@codingthesmartway.com"
    },
    {
        "id": 2,
        "first_name": "Steve",
        "last_name": "Palmer",
        "email": "steve@codingthesmartway.com"
    },
    {
        "id": 3,
        "first_name": "Ann",
        "last_name": "Smith",
        "email": "ann@codingthesmartway.com"
    }
    ],
    "comments": [
        { "id": 1, "body": "some comment", "postId": 1 }
    ],
    "profile": { "name": "typicode" }
}

```

json-server uruchamiamy poleceniem:

```JavaScript
json-server db.json
```

lub 
```JavaScript
json-server --watch db.json
```
Jeśli nie użylibyśmy --watch, trzeba by po każdej zmianie danych ubijać serwer i uruchamiać na nowo, żeby je zauważyć.

API dostępne jest pod adresem: 
http://localhost:3000/ w resources:
* http://localhost:3000/employees
* http://localhost:3000/comments
* http://localhost:3000/profile


Jak uruchomicie sobie aplikację pod powyższym adresem, zobaczycie zwrotkę z serwera json.

Dzięki json-server będziemy mogli wykonywać operacje zapisywanie nowych rekordów, usuwanie, dodawanie, edycja.

Create	POST
Read (Retrieve)	GET	
Update	UPDATE	/ PUT / PATCH
Delete (Destroy)	DELETE	

Na przykładzie powyższego pliku db.json, nasze REST API udostępnia nam metody (m.in. na obj. employees):

	GET    /employees
	GET    /employees/{id}
	POST   /employees
	PUT    /employees/{id}
	PATCH  /employees/{id}
	DELETE /employees/{id}

Jeśli wykonamy requesty POST, PUT, PATCH lub DELETE, zmiany zostaną automatyczne zapisane do pliku db.json.

### Metody POST, PUT i PATCH powinny zawierać nagłówki:
```JavaScript
Content-Type: application/json header
```

żeby można było używać JSONa w body requestu. Jeśli nie dodamy nagłówka, zostanie nam zwrócony status 200, ale nie będzie widać żadnych zmian w danych.

URL zapytań można rozszerzać o parametry, np. można filtrować dane dołączając do adresu URL parametrów po znaku zapytania, w postaci klucz=wartość, np:

``` http://adresstrony.pl/?param=value```

```JavaScript
http://localhost:3000/employees?first_name=Sebastian
```


## B. Jak zacząć? (opcja 1 - pobranie gotowego repo)

1. Sklonuj repozytorium na swój komputer. Użyj do tego komendy `git clone adres_repozytorium`
Adres repozytorium możesz znaleźć na stronie repozytorium po naciśnięciu w guzik "Clone or download" 
2. Po sklonowaniu repozytorium, wejdź do folderu który się utworzył. W nim będzie folder z projektem "video-lib" - wejdź w niego (w tym folderze powinien znajdować się plik <i>package.json</i>). Teraz musisz zainstalować paczki za pomocą npm, w command line lub terminalu wpisz:

```JavaScript
npm install
```

Rozpocznie się instalacja dependencji. Bądź cierpliwy, trochę to może potrwać.

Po zainstalowaniu, jesteś gotów do uruchomienia aplikacji:

```JavaScript
ng serve -o
```

## Zapisywanie zmian w repo GIT
1. Zrób zadania "krok po kroku" i skomituj zmiany do swojego repozytorium. Użyj do tego komend `git add nazwa_pliku`.
Jeżeli chcesz dodać wszystkie zmienione pliki na raz, użyj `git add .` 
Pamiętaj że kropka na końcu jest ważna!
Następnie skommituj zmiany komendą `git commit -m "nazwa_commita"`
2. Wypchnij zmiany do swojego repozytorium na GitHubie.  Użyj do tego komendy `git push origin master`
3. Uruchom aplikację wpisując w terminalu/command line

```JavaScript
    ng serve
```
Musisz być w głównym folderze z aplikacją (tam, gdzie znajduje się plik package.json).

## B. Jak zacząć? - (opcja 2 - preferowana, od początku)

## 1 - Repo na GitHubie
1. Utwórz konto na GitHubie. 
2. Jeśli posiadasz konto, wejdź w zakładkę "Moje repozytoria" i wybierz "Nowe"
3. Wpisz nazwę nowego repozytorium
4. Utwórz repozytorium

## 2a Tworzenie nowego projektu - z konfiguracją domyślnego formatu stylów i prefixu

Można również utworzyć aplikację i od razu przy tworzeniu określić, jaki chcemy mieć np format plików ze stylami i np prefix selektorów:


```JavaScript
ng new my-project --style scss --prefix video
```


## 2b - Tworzenie nowego projektu - bez ustawienia domyślnego formatu stylów i prefixów

1. Otwórz okno terminala albo listy poleceń
2. Korzystając z Angular CLI utwórz nowy projekt


```JavaScript
ng new nazwa-projektu
```
Angular CLI wygeneruje aplikację w folderze o nazwie projektu, jaką wpisaliśmy. Utworzy też wszystkie potrzebne pliki i zależności. Jednym z utworzonych plików będzie package.json. Jest to bardzo ważny plik aplikacji, ponieważ zawiera listę zależności, które Angular CLI musi zainstalować oraz listę tasków (zadań), które można będzie wykonać. Instalując dodatkowe paczki, ten plik będzie nadpisywany nową wersją.

3. Teraz możemy przetestować, czy aplikacja działa. W terminalu/ konsoli należy wejść w folder z projektem 

```JavaScript
cd nazwa-projektu
```

a następnie uruchomić aplikację na serwerze wpisując polecenie Angular CLI do startu aplikacji:

```JavaScript
ng serve
```

Aplikacja wystartuje na serwerze lokalnym na domyślnym porcie 4300 i będzie dostępna pod adresem:
http://localhost:4300/


```JavaScript
ng serve -o
```
-o powoduje, że po uruchomieniu serwera aplikacja automatycznie wystartuje w nowym oknie.

Domyślnie Angular CLI generuje pliki ze stylami w formacie .css oraz selektory komponentów z prefixem "app-". Możemy to zmienić w aplikacji w późniejszym etapie - w pliku <i><b>angular.json</b></i> dostępnym w głównym folderze aplikacji:


* ustawiając domyślny format plików ze stylami np na .scss - dopisując w polu "schematics":

```JavaScript
    "schematics": {
	  "@schematics/angular:component": {
		"styleext": "scss"
	  }
	}
```
Możemy też zdefiniować, czy chcemy, aby domyślnie generowane komponenty zawierały inline template/ styles (czyli template pisany w tym samym pliku co klasa komponentu), lub czy chcemy żeby był oddzielnym plikiem:

```JavaScript
"schematics": {
     "@schematics/angular": {
       "component": {
         "inlineStyle": true,
         "inlineTemplate": true
       }
     }
   }
```

* ustawiając domyślny prefix dla aplikacji (np zamiast "app-", np "myprefix-")
```JavaScript
"app": [
  ...
  "prefix": "myprefix",
  ...
```

## 3 - dodanie grid-u Bootstrap ??

Bootstrap pozwala na tworzenie responsywnych projektów, Mobile First. W naszym projekcie użyjemy więc Grida Bootstrapowego do stworzenia responsywnego layoutu. Nie będziemy korzystać z innych komponentów Bootstrapowych, tj. buttony, nav itp., dlatego, że Angular doskonale wspiera Angular Material. Z niego skorzystamy do tworzenia elementów strony.

* Zainstaluj Bootstrap w oknie terminala, używając polecenia:

```JavaScript
npm i -S bootstrap
```
skrót "i"  - to skrót od "install", natomiast "-s" to skrót od "--save" - co oznacza, że NPM zainstaluje Bootstrap jako dependencję (oddzielną paczkę) w folderze node_modules i zapisze informację o zależności w pliku <i>package.json</i>  możesz mieć inną wersję na dzień instalacji.

```JavaScript
"dependencies": {
    ...
    "bootstrap": "^4.3.1",
}
```

* do pliku głównego <i>style.css</i> znajdującego się w głównym folderze aplikacji, zaimportuj style potrzebne do prawidłowego korzystania z grida:



```JavaScript
@import '~bootstrap/scss/bootstrap-reboot';
@import '~bootstrap/scss/bootstrap-grid';
```

Teraz możesz już korzystać z grida Bootstrapowego w swoim template.

W celu przetestowania Bootstrap, możesz wejść w główny plik z komponentem aplikacji (z CLI jest to src/app/app.component.html) i to, co się w nim znajduje, zastąpić:

src/app/app.component.html:
```HTML
<div class="container-fluid">
  <div class="row my__header">
    <div class="col">
      Hello world
    </div>
  </div>
  <div class="row">
    <div class="col">
      <div class="container content">
        <div class="row">
            <div class="col-3 nav">
                <nav>
                  <ul>
                    <li><a href="#">Link 1</a></li>
                    <li><a href="#">Link 2</a></li>
                  </ul>
                </nav>
              </div>
              <div class="col">
                Hello world.
              </div>
        </div>
      </div>
    </div>    
  </div> 
  <div class="row my__footer">
    <div class="col">
    Hello world
    </div>
  </div>
</div>
```


src/app/app.component.scss
```CSS
.my__footer, .my__header {
    color: white;
    padding: 24px;
    margin: 0;
}

.my__header {
    background-color: darkblue;    
}

.my__footer {
    background-color: lightslategray;
}

.content {
    background-color: #fff;
    color: black;
    font-size: 14px;
}

.nav {
    background-color: lightblue;
}

```

Powinieneś zobaczyć prostą strukturę strony.

To znaczy, że Bootstrap działa.

## 4 - dodanie Angular Material, Angular CDK i Angular Animations

W celu zainstalowania Angular Material należy w terminalu, będąc w projekcie, wpisać polecenie:

```JavaScript
npm install --save @angular/material @angular/cdk @angular/animations
```

Po zainstalowaniu Angular Material, musimy jeszcze zaimportować moduł z Animacjami do naszej aplikacji. Inaczej Angular, kiedy próbowalibyśmy użyć jakichś komponentów, krzyczałby, że nie rozpoznaje danego komponentu.

```JavaScript
import modułu import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
```

Zanim przejdziemy do następnego kroku, dodajmy jeszcze do pliku głównego ```style.scss``` (lub style.css) przykładowy theme Angular Material (gotowe style) do naszej aplikacji. Inaczej, korzystajac z Angular Material Components, komponenty nie będa nam się prawidłowo wyświetlać. Może w nich  zabraknać stylów, np. cieni dla elementów itp...

Gotowe skórki ze stylami znajdziesz tu: https://material.angular.io/guide/theming

Ja zaimportuję plik ```deeppurple-amber.css```

```SCSS
@import '@angular/material/prebuilt-themes/deeppurple-amber.css';
```

## 5 - instalacja Angularowych ikon

To ostatnia rzecz, która została nam do wykonania, żeby miec gotowe startowe repo. Ikony będą nam potrzebne, więc po prostu dodam je do projektu.

1. Zainstaluj ikony używając terminala/command line

```JavaScript
npm install material-design-icons
```

2. Dołącz ikony do styli - w pliku głównym style.css/ style.scss

```JavaScript
@import url("https://fonts.googleapis.com/icon?family=Material+Icons");
```

3. Po zainstalowaniu ikon Materiala, należy dodać moduł z ikonami do głównego modułu aplikacji:

```JavaScript
import { MatIconModule } from '@angular/material/icon';
```

4. Lista Icon dostępna jest pod adresem https://material.io/tools/icons/. Wybraną ikonę należy po prostu użyć:

```HTML
<i class="material-icons">
    account_circle
</i>
```

## 6 - dodanie obsługi typów dla plików .json

W folderze głównym aplikacji  ```src``` utwórz plik typings.d.ts i umieść w nim:

```JavaScript
declare module "*.json" {
    const value: any;
    export default value;
}
```

Dzięki temu będziemy mogli na początku korzystać z "bazy danych" z pliku JSON, importując ją lokalnie do aplikacji jak moduł, jeszcze zanim użyjemy HTTP.

# BIBLIOTEKA FILMÓW 
tworzenie aplikacji.


## 1. Struktura aplikacji

Główna aplikacja znajduje się w folderze 
```src```.

W folderze ```src``` znajdują się 3 foldery (app, assets, environments) oraz pliki konfiguracyjne i startowe aplikacji. 

Spójrzmy w plik ```index.html``` - wewnątrz niego znajduje się prosta struktura HTML oraz root aplikacji - komponent Angularowy (domyślnie jest to ```<app-root>```). Nie jest to element HTML, ale właśnie komponent Angularowy. Kiedy aplikacja jest gotowa do uruchomienia, zawartość komponentu zostaje wstrzyknięta do tego komponentu.

### Moduły Angulara - NgModule

Stanowią główny blok budujący aplikację. Są paczką powiązanych ze sobą funkcjonalności, zestawem komponentów, innych modułów powiązanych z danym modułem, wszelkich potrzebnych komponentom zależności. Organizuje kod naszej aplikacji, modularyzuje ją i pozwala na reużywanie zawartości.

Każdy komponent, który utworzymy, <b>jest zadeklarowany w i należy do jednego i tylko jednego modułu Angularowego</b>. Angular sam w sobie składa się z wielu modułów, np. 
* @angular/core
* @angular/animate
* @angular/http
* @angular/router

W Angularze musimy utworzyć główny moduł, który pozwoli nam uruchomić aplikację. Aplikacja Angularowa musi składać się minimum z jednego modułu.

Taki moduł Angularowy może zawierać:
* komponenty
* serwisy
* dyrektywy
* pipe'y
* inne angularowe moduły

W aplikacji posiadamy moduł główny, zwany ```root NgModule```, zdefiniowany w pliku app/app.module.ts.

Moduł Angularowy to zwykła klasa z dekoratorem @NgModule. 

```JavaScript
@NgModule({

})
export class AppModule{}
```

Jak Angular wie, że jest to nasz główny moduł, który ma uruchomić aplikację? 
Jest to zdefiniowane w pliku main.ts

```JavaScript
platformBrowserDynamic().bootstrapModule(AppModule)
  .catch(err => console.error(err));
```

platformBrowserDynamic - tworzy platformę - punkt wejścia dla Angulara do aplikacji webowej. 
Każda aplikacja musi być utworzona z metody bootstrapModule i właściwość bootstrap jest sprawdzana kiedy aplikacja jest tworzona. Root moduł musi mieć zdefiniowany bootstrap components i może być on tylko w jednym, głównym module aplikacji.
```JavaScript
@NgModule({
  imports: [BrowserModule],
  declarations: [AppComponent],
  bootstrap: [AppComponent]
})
export class AppModule {}
````


### Dekorator 
Dekorator to zwykła funkcja, poprzedzona znakiem @, która dodaje do klasy metadane. Angular dostarcza wbudowane dekoratory. 
Dekorator określa, jaką rolę pełni klasa w Angularze. Każdy obiekt angularowy jest dekorowany (moduł, dekorator, serwis, pipe, komponent).

Komponenty, które piszemy w Angularze, też są dekorowane z użyciem dekoratora @Component(). 

```JavaScript
@Component({

})
export class AppComponent{}
```

....


## 2. Budujemy aplikację - Step by Step

### 1. Sklonuj repo lub utwórz nowy projekt wg powyższych wskazówek
### 2. Wejdź w folder z projektem

```JavaScript
cd start-app
```

### 3. Zainstaluj paczki używając Node Package Manager

```JavaScript
npm install
```

Podstawowa struktura, od której zaczniemy pisanie aplikacji, znajduje się w folderze ```start-app```.

### 4. Uruchom aplikację - nasz etap startowy. 

```JavaScript
ng serve -o
```

## Działamy dalej...

### 5. Tworzymy pierwszy komponent

Komponent - view zdefiniowany z template, logika z klasą komponentu, a metadane z dekoratorem.
Komponenty w Angularze są to klasy, dekorowane z użyciem dekoratora @Component(), zawierający  informacje o komponencie. W metadanych definiujemy nazwę dyrektywy (selector), po którym będziemy identyfikować komponent w template, style, template itp. Każdy komponent posiada template, który zawiera syntax Angularowy z HTML i definiuje on widok komponentu.

```do poczytania:``` https://angular.io/guide/architecture-components

```lista wszystkich metadanych w dekoratorze @Component```: https://angular.io/api/core/Component


```JavaScript
@Component({
  // metadane:
})
export class AppComponent{}
```

Jako metadane do dekoratora @Component() możemy przekazać cała liste metadanych, w tym template i style inline:

```JavaScript
@Component({
  // metadane:
  selector: 'mov-films',
  template: `<div><h1>Tytuł</h1></div>`,
  styles: [`
    section {
      background-color: red;
      color: white;
    }

    h1 {color: blue; }
  `]
})
export class AppComponent{}
```

Albo template i style jako referencje do pliku:

```JavaScript
@Component({
  // metadane:
  selector: 'mov-films',
  templateUrl: './films.component.html',
  styleUrls: ['./films.component.scss']
})
export class AppComponent{}
```

W dekoratorze mamy metadana ```selector```. Służy on do nadania nazwy komponentowi. Dzięki tej nazwie będziemy mogli <b>korzystać z komponentu w template jako z dyrektywy</b>, wpisujac:

app.component.html
```html
 <mov-films></mov-films>
```

Klasy komponentu zawierają propertisy (właściwości) i metody, które możemy użyć w widoku.
Komponenty możemy łączyć razem w moduły. Każdy komponent, który utworzymy, jest zadeklarowany w, i należy do jednego i tylko jednego modułu Angularowego.
Jeśli chcemy z niego korzystać w innym module należy go z innego modułu wyeksportować.

Tworzymy komponent ```films``` oraz folder ```components``` w którym chcemy go umieścić.

```JavaScript
ng g c components/films
```
Po wygenerowaniu komponentu w konsoli dostaniemy informację o utworzeniu plików oraz o tym, że została dokonana zmiana w pliku ```app.module.ts``` - komponent ```FilmsComponent``` został zaimportowany.

W folderze ```src/app/components/films``` pojawiły się 4 pliki wygenerowane przez Angular CLI.
W pliku films.components.ts widzimy, że utworzył się komponent ```mov-films```.

W pliku ```app.component.html``` wstawiamy do template nasz komponent ```mov-films```. Widzimy w przeglądarce, że komponent działa, wyświetla się napis: ```films works!```.

Zobaczmy, jak przekazujemy  dane z komponentu do widoku. 
Zadeklarujmy wewnątrz klasy komponentu zmienną title i nadajmy jej wartość:

```JavaScript
    export class FilmsComponent implements OnInit {
        public title = "Biblioteka filmów"; 

        constructor() { }

        ngOnInit() {
    }
```
W szablonie możemy użyć tej właściwości stosując interpolację, czyli 
```{{ title }}```.

```html
<h1>{{ title }}</h1>
```

Interpolacja jest rodzajem one-way bindingu, gdzie dane idą w kierunku z komponentu do widoku. Zazwyczaj używamy jej gdy chcemy wyświetlić wartości właściwości lub metod klasy w template. Nie musimy się odwoływać do nich za pomocą <i>this</i>. Tekst między nawiasami ```{{}}``` jest nazywane "template expression", który Angular najpierw ewaluuje (oblicza), a potem konwertuje do stringa.
W interpolacji możemy dokonywać obliczeń. Mamy też kilka operatorów ułatwiających:
* |
* ?
* . 
* !

W interpolacji nie można używać:
* przypisania (=, +=, -=, ...)
* operacji, tj. new, typeof, instanceof itp
* łączonych wyrażeń z ; lub ,
* inkrementacji (++) i dekrementacji (--)
* wielu operatorów ES6+

Teraz możemy utworzyć w komponencie tablicę z danymi o filmach. Niech to na razie będzie przykładowa tablica, którą zamieścimy wewnątrz klasy ```FilmsComponent```, ale jeszcze przed konstruktorem. Mogę dodać modyfikator dostępu ```public```.

Plik films.component.ts powinien wyglądać tak:

```JavaScript
import { Component, OnInit } from '@angular/core';
import { Film } from './film';

@Component({
  selector: 'mov-films',
  templateUrl: './films.component.html',
  styleUrls: ['./films.component.scss']
})
export class FilmsComponent implements OnInit {
  public title = 'Biblioteka filmów';
  public films: Film[] = [
    {
        id: 0,
        title: 'Skazany na śmierć',
        actress: ['Wenthworth Miller', 'Dominic Purcell', 'Amaury Nolasco'],
        rating: 3,
        time: 270,
        types: ['Dramaty telewizyjne', 'Seriale i programy kryminalne', 'Amerykańskie programy i seriale'],
        categories: ['mroczne', 'trzymające w napięciu'],
        description: `Gliniarz z Las Vegas próbuje ukraść narkotyki należące do gangsterów, 
        ale jego plan nie wypala, a syn zostaje porwany.`,
        url: 'https://www.netflix.com/browse?jbv=80134513&jbp=1&jbr=7',
        imageUrl: 'http://img.liczniki.org/20151110/prison_break_skazany_na_smierc_sezon_4-1447173751.jpg'
      },
      {
        id: 1,
        title: 'Ciemniejsza strona Greya 1',
        actress: ['Jamie Fox', 'Scoot McNairy', 'T.I.'],
        rating: 3,
        time: 94,
        types: ['Akcja i przygoda', 'Thrillery akcji', 'Kryminalne filmy akcji'],
        categories: ['emocjonujące'],
        description: `1 - Anastasia rozpoczyna karierę w wydawnictwie, a Christian postanawia na nowo rozgrzać ich związek. 
        Na przeszkodzie ich szczęściu stają jednak pewne zewnętrzne siły.`,
        url: 'https://www.netflix.com/browse?jbv=80134513&jbp=1&jbr=7',
        imageUrl: 'https://ssl-gfx.filmweb.pl/po/58/60/735860/7774489.6.jpg'
      },
      {
        id: 1,
        title: 'Ciemniejsza strona Greya 2',
        actress: ['Jamie Fox', 'Scoot McNairy', 'T.I.'],
        rating: 3,
        time: 94,
        types: ['Akcja i przygoda', 'Thrillery akcji', 'Kryminalne filmy akcji'],
        categories: ['emocjonujące'],
        description: `2 - Anastasia rozpoczyna karierę w wydawnictwie, 
        a Christian postanawia na nowo rozgrzać ich związek. Na przeszkodzie ich szczęściu stają jednak pewne zewnętrzne siły.`,
        url: 'https://www.netflix.com/browse?jbv=80134513&jbp=1&jbr=7',
        imageUrl: 'https://ssl-gfx.filmweb.pl/po/58/60/735860/7774489.6.jpg'
      },
      {
        id: 1,
        title: 'Ciemniejsza strona Greya 3',
        actress: ['Jamie Fox', 'Scoot McNairy', 'T.I.'],
        rating: 3,
        time: 94,
        types: ['Akcja i przygoda', 'Thrillery akcji', 'Kryminalne filmy akcji'],
        categories: ['emocjonujące'],
        description: `3 - Anastasia rozpoczyna karierę w wydawnictwie,  
          a Christian postanawia na nowo rozgrzać ich związek. Na przeszkodzie ich szczęściu stają jednak pewne zewnętrzne siły.`,
        url: 'https://www.netflix.com/browse?jbv=80134513&jbp=1&jbr=7',
        imageUrl: 'https://ssl-gfx.filmweb.pl/po/58/60/735860/7774489.6.jpg'
      },
      {
        id: 1,
        title: 'Ciemniejsza strona Greya 4',
        actress: ['Jamie Fox', 'Scoot McNairy', 'T.I.'],
        rating: 3,
        time: 94,
        types: ['Akcja i przygoda', 'Thrillery akcji', 'Kryminalne filmy akcji'],
        categories: ['emocjonujące'],
        description: `4 - Anastasia rozpoczyna karierę w wydawnictwie, a Christian postanawia na 
        nowo rozgrzać ich związek. Na przeszkodzie ich szczęściu stają jednak pewne zewnętrzne siły.`,
        url: 'https://www.netflix.com/browse?jbv=80134513&jbp=1&jbr=7',
        imageUrl: 'https://ssl-gfx.filmweb.pl/po/58/60/735860/7774489.6.jpg'
      },
      {
        id: 1,
        title: 'Ciemniejsza strona Greya 5',
        actress: ['Jamie Fox', 'Scoot McNairy', 'T.I.'],
        rating: 3,
        time: 94,
        types: ['Akcja i przygoda', 'Thrillery akcji', 'Kryminalne filmy akcji'],
        categories: ['emocjonujące'],
        description: `5 - Anastasia rozpoczyna karierę w wydawnictwie, a Christian 
        postanawia na nowo rozgrzać ich związek. Na przeszkodzie ich szczęściu stają jednak pewne zewnętrzne siły.`,
        url: 'https://www.netflix.com/browse?jbv=80134513&jbp=1&jbr=7',
        imageUrl: 'https://ssl-gfx.filmweb.pl/po/58/60/735860/7774489.6.jpg'
      }
  ];

  constructor() {}

  ngOnInit() {
  }
}
```
Do wyświetlenia biblioteki filmów na stronie, utworzymy bloki z informacjami o danym filmie.
Do wyświetlenia danych o każdym filmie będę musiała użyć dyrektywy strukturalnej (*ngFor), która pozwoli mi przejść po każdym elemencie tablicy i wyświetlić go na stronie.

Z kolei do wyświetlenia kart użyję componentów Angular Material - ```mat-card```, który umieszczę w pliku ```films.component.html```.

Komponent mat-card jest kontenerem, w którym można umieszczać dowolną treść (tekst, obrazki oraz akcje, które chcemy wykonać w kontekście tego elementu (dokumentacja - https://material.angular.io/components/card/overview)). 

Do template films.component.html dodaję: 

```html
<mat-card>Simple card</mat-card>
```

Jak widać, Angular rzuca błędem, bo nie widzi jeszcze modułu mat-card.
Należy zaimportowac go w głównym module aplikacji - w pliku ```app.module.ts```
```JavaScript
import { MatCardModule } from '@angular/material/card';

@NgModule({
  ...
  imports: [
    ....,
     MatCardModule
  ]
})
```

Teraz powinniśmy móc wyświetlić Angularowy component mat-card.


## Wyświetlenie listy filmów
Kolejnym krokiem będzie wyświetlenie naszej testowej listy filmów. 
Lista filmów jest tablicą. Żeby ją wyświetlić, w komponencie films.component.html - muszę przeiterować po tablicy, odczytać wartość każdego elementu tablicy i wyrenderować widok dla każdego z nich. 

Wykorzystuję do tego dyrektywę strukturalna *ngFor, która w pętli wygeneruje nam fragment DOM dla elementów tablicy. Dodatkowo użyję  dyrektywy strukturalnej *ngIf, która spowoduje, że jeśli tablica filmów nie jest pusta (czyli films.length zwróci true), to filmy zostana wyświetlone, a jeśli jest pusta, to Angular nie wygeneruje tego elementu w strukturze DOM.

```HTML
<ul *ngIf="films.length">
   <li *ngFor="let film of films">
     <!-- film - to template input variable --->
      {{ film.title }}
   </li>
</ul>
```

Po tym, powinna nam się wyświetlić lista nieuporzadkowana tytulów filmów.


```JavaScript
Skazany na śmierć
Ciemniejsza strona Greya 1
Ciemniejsza strona Greya 2
Ciemniejsza strona Greya 3
Ciemniejsza strona Greya 4
Ciemniejsza strona Greya 5
```

Zauważcie, że ciężko jest "zapanować" nad danymi, jesli nie mamy sprawdzania poprawności danych, a przez to też nie mamy podpowiedzi, jakie właściwości czy metody posiada dany obiekt. Nie mamy też sprawdzania poprawności wprowadzanych danych. Utrudnia to debugowanie i wykrywanie błędów.

Dlatego wprowadzimy silne typowanie z użyciem TypeScript. TypeScript dostarcza nam interfejsy. Klasy mogą implementować interfejsy tzn. że klasa zawiera kod (metody i właściwości) określone w interfejsie. Interfejs to specyfikacja identyfikująca powiązany zestaw właściwości i metod. Możemy użyć tych interfejsów jako typy danych. ES5 i ES6 (ES 2015) nie wspierają interfejsów. Wspiera je TypeScript. Są usuwane w trakcie kompilacji i nie są widoczne w wynikowym JavaScripcie.

To oznacza, że sprawdzanie poprawności typów nie odbywa się w runtimie (w trakcie wykonywania kodu JavaScript), ale w trakcie kompilacji.


Przykładem interfejsu jest:
```JavaScript
export interface Person {
    name: string;
    surname: string;
    age: number;
    obliczBMI(height:number, weight: number): number;
}
```

Powyższy interfejs definiuje properties (właściwości obiektu - name, surname, age) - określa ich typy, oraz definiuje metodę obliczBMI która jako argument przyjmuje 2 wartości typu number i zwraca wynik typu number.

Interfejs możemy później zaimportować do np. komponentu i użyć jako typ danych, np jako tablicę obiektów typu Person:

```Javascript 
import { Person } from './osoba';

export class SomeComponent {
    public people: Person[];
}
```

Interfejsy możemy tworzyć ręcznie albo automatycznie dzięki Angular CLI.

```JavaScript
ng generate interface [name] <type> generates an interface

// lub alias g = generate, i = interface
// --dry-run pozwala nam "podejrzeć" gdzie Angular wygeneruje pliki bez nanoszenia zmian.

ng g i [nazwa_interfejsu]
```

Wygeneruj interfejs albo utwórz samodzielnie plik film.ts:

```JavaScript
ng g i components/films/films
```

Zostanie wygenerowany plik ```film.ts```, w którym znajduje się definicja interfejsu dla filmów - na razie pusty obiekt. 
Inteferjs ma konstrukcję:

```JavaScript
export interface Film {
}
```

Tworzymy interfejs dla obiektu Film - zauważ, że opisuję go w liczbie pojedynczej; Opisujemy interfejs dla obiektu Film, nie Films. Później w kodzie będziemy tworzyć tablicę filmów i wtedy będziemy mogli nadać jej typ tablicy filmów: Films[]. 

Eksportujemy interfejs, żebyśmy mogli zaimportować go w innych miejscach w aplikacji.

```JavaScript
export interface Film {
    id: number;
    title: string;
    actress: string[];
    rating: number;
    time: number;
    types: string[];
    categories: string[];
    description: string;
    url: string;
    imageUrl: string;
}
```

Określ typ tabeli film, którą zadeklarowałeś w komponencie FilmsComponent:

```JavaScript
 public films: Film[] = [
     ...
```

Jeśli w użytym przez Ciebie kodzie wystąpi niezgodność typów, kompilator podkreśli Ci na czerwono tę informację.

2. Listę filmów w pliku films.component.html zamieniamy na komponent angularowy mat-cards, w którym umieścimy dane.

Zamieniamy

```html
<ul *ngIf="films.length">
    <li *ngFor="let film of films">
       {{ film.description }}
    </li>
 </ul>
```

na 


```html
 <section class="films__list" *ngIf="films.length">
   <h1>Films</h1>
   <mat-card class="films__item" *ngFor="let film of films">
      <mat-card-header>
        <mat-card-title>{{ film.title }}</mat-card-title>
        <mat-card-subtitle>{{ film.types}}</mat-card-subtitle>
      </mat-card-header>
      <mat-card-content>
        <img 
          class="films__item films__item_image" 
          mat-card-image 
          src="{{film.imageUrl}}">
        <mat-card-subtitle>{{ film.description }}</mat-card-subtitle>
      </mat-card-content>
  </mat-card>
 </section>
```

Da się zauważyć, że po zdefiniowaniu typu dla tablicy filmów, edytor podpowiada nam dostępne pola dla obiektu films (w momencie postawienia kropki za zmienną film).


## Binding

Zarzadza komunikacja między klasa komponentu a jego template i często angażuja dołaczone dane.
<b>Syntax bindingu jest zawsze zdefiniowany w template.</b>

## Angular dostarcza kilka typów bindingu:
### Grupowane w zależności od kierunku przepływu danych
1. ```ONE-WAY``` - przepływ danych ze źródła danych do widoku i sa to typy:  
- Interpolation
- Property binding
- Attribute binding
- Class binding
- Style binding

Syntax:
```html
{{expression}}
[target]="expression"
bind-target="expression"
```

2. ```ONE-WAY``` - przepływ danych z widoku do źródła danych 
- event binding

Syntax:
```html
(target)="statement"
on-target="statement"
```

3. ```TWO-WAY``` - przepływ w obie strony

Syntax:
```html
[(target)]="expression"
bindon-target="expression"
```

To, co jest po lewej stronie przypisania, w nawiasach [] lub () [()] (lub prefixowane bind-, on-, bindon-), nazywamy ```nazwa targetu```. Nazwa targetu jest nazwa ```property```. To, co jest po lewej stronie - wartość. W zależności od typu bindingu, targetem może być: 
* (property binding) element, component lub dyrektywa, 
* (event binging) element, component, dyrektywa, event, lub 
* (attribute binding) - atrybut.

```html
 <button [attr.aria-label]="help">help</button> 
 ```

Więcej na ten temat: https://angular.io/guide/template-syntax#binding-targets


###  <b>PROPERTY BINDING</b> - one-way binding  
```html
<img [src]="film.imageUrl">
```

W powyższym przykładzie: ```[src]``` to właśnie element property (właściwość elementu), a ```film.imageUrl``` to template expression - przekazujemy do src wartość imageUrl.

## Podpięcie pliku .json z bazą danych filmów 

Za chwilę zaczniemy pracę na bardziej "realnych" danych. W komponencie FilmsComponent (w pliku films.component.ts), zamienimy obecną tablicę z danymi na dane z pliku ```db.json```, który znajduje się w folderze głównym aplikacji.
W pliku znajduje się baza filmów.

Podepniemy ją do naszej aplikacji i na podstawie tych danych zbudujemy widok strony z filmami. 

W późniejszej części workshopów ten plik .json posłuży nam jako baza danych do naszego REST API.

1. Zaimportuj do pliku ```films.component.ts``` bazę danych z pliku db.json, podając lokalizację pliku.

```JavaScript
import * as data from 'src/db.json';
```
ES6 pozwala nam importować wystkie dane z pliku za pomocą gwiazdki (*) i pozwala nadawać alias tym danym czyli nazwę, po której będziemy mogli się do tych danych odwołać w projekcie do którego importujemy.
Ponieważ dane nie zostały przypisane do żadnej zmiennej, są tylko luźną tablicą z danymi w formacie JSON, to nie mamy też nazwy zmiennej, którą moglibyśmy zaimportować. Alias pozwala nam opakować te luźne dane i odnosić się do nich po tej nazwie, w tym przypadku: ```data```.

2. Utwórz properties w klasie komponentu i określ jego typ jako tablicę obiektów typu ```Film```. 

W konstruktorze przypisz do właściwości ```films``` zawartość pliku .json. Po zaimportowaniu pliku .json - zostanie on zaimportowany jako moduł. Nie mamy od razu dostępu do zawartości, ale dopiero po kropce, w property ```default```:

films.component.ts
```JavaScript
export class FilmsComponent implements OnInit {
  public title = 'Biblioteka filmów';
  public films: Films[];

  constructor() {
    this.films =  data.default;
  }
  ....
```

3. W pliku films.ts (plik, w którym przechowujesz interfejs tablicy filmów) - zmień definicję interfejsu. Interfejs powinien definiować typ danych, jakich spodziewamy się w naszej bazie danych filmów.

films.ts

```JavaScript
export interface Films {
    title: string;
    year: string;
    genres: string[];
    duration: string;
    ratings: number[];
    releaseDate: string;
    averageRating: number;
    originalTitle: string;
    storyline: string;
    actors: string[];
    imdbRating: number;
    posterurl: string;
}
```
4. Zobaczcie, jak wygląda plik db.json - jest to obiekt JSON zawierający tytuł filmu, rating, aktorów, rok produkcji, gatunki, czas trwania itp.

Możemy przerobić sobie pierwszy widok, który wyrenderowaliśmy na przykładzie poprzedniej "bazy danych":

```films.component.html```
```html
<h1>
   {{ title }}
</h1>
 <section class="films__list" *ngIf="films.length">
   <h1>Films</h1>
   <mat-card class="films__item" *ngFor="let film of films">
      <mat-card-header>
        <mat-card-title>{{ film.title }}</mat-card-title>
        <mat-card-subtitle>{{ film.types}}</mat-card-subtitle>
      </mat-card-header>
      <mat-card-content>
        <img 
          class="films__item films__item_image" 
          mat-card-image 
          src="{{film.imageUrl}}">
        <mat-card-subtitle>{{ film.description }}</mat-card-subtitle>
      </mat-card-content>
  </mat-card>
 </section>

```

na nowy widok, pobierający dane zgodnie z nowym źródłem informacji o filmach. Póki co, linter będzie nam podpowiadał o błędach w template spowodowane tym, że próbujemy odwoływać się do właściwości obiektu, które nie zostały zdefiniowane. 
Dzieje się tak dlatego, że obecnie nasze filmy mają inne pola nich wcześniejsze.

5. Zanim utworzę nowy widok, zaimportuję component Angularowy - button. Buttony Angular Material to natywne elemety ```<button>``` i ```<a>``` ulepszone o stylowanie Material Design i ripple. 

Jak mówi dokumentacja:

<i>The ```<button>``` element should be used for any interaction that performs an action on the current page.</i>

<i>The ```<a>``` element should be used for any interaction that navigates to another view.</i>

Zgodnie z powyższym, ja w moim widoku później użyję linku ```<a>```, ponieważ będę chciała, żeby przycisk nawigował mnie do strony filmu, gdzie przeczytam detale. Póki nie mam obsłużonej nawigacji, umieszczę po prostu ```<button>```.

Najpierw jednak, muszę zaimportować ```MatButtonModule```.

```app.module.ts```

```html
import { MatButtonModule } from '@angular/material/button';

....
// oraz do tablicy import  

imports: [
    ...
    MatButtonModule
]
```

Następnie możemy przerobić template. 
W templacie wyświetlę podstawowe informacje o obrazku, tj. tytuł, plakat (obrazek), opis, gatunek, czas trwania i gwiazki oraz wstawię przycisk do wejścia w szczegóły o filmie, gdzie można będzie przeczytać wszystkie informacje, jakie się o nim znajdują.

```films.component.ts``` - cała zawartość:

```html
<h1>
   {{ title }}
</h1>
 <section class="films__list" *ngIf="films.length">
   <h1>Films</h1>
   <mat-card class="films__item" *ngFor="let film of films; let i = index">
      <mat-card-header>
        <mat-card-title>{{ film.title }}</mat-card-title>
        <mat-card-subtitle>{{ film.genres}}</mat-card-subtitle>
      </mat-card-header>
      <mat-card-content>
        <div class="rating">
          <i class="material-icons">star_rate</i>
          <i class="material-icons">star_rate</i>
          <i class="material-icons">star_rate</i>
          <i class="material-icons">star_rate</i>
          <i class="material-icons">star_rate</i>
          <i class="material-icons">star_rate</i>
          <i class="material-icons">star_rate</i>
          <i class="material-icons">star_rate</i>
          <i class="material-icons">star_rate</i>
          <i class="material-icons">star_rate</i>
        </div>
        <img 
          class="films__item films__item_image" 
          mat-card-image 
          src="{{ film.posterurl }}">
        <mat-card-subtitle>{{ film.storyline }}</mat-card-subtitle>
      </mat-card-content>
      <mat-card-actions>
        <button mat-icon-button>Details</button>
      </mat-card-actions>
  </mat-card>
 </section>

```

Obecnie aplikacja powinna nam wyświetlać stronę z listą filmów i głównymi informacjami.

W template zahardkodowałam gwiazki, które będą oznaczały wynik ratingu. Będzie to średnia skala od 0 do 10 liczona na podstawie średniej arytmetycznej wszystkich ocen uzyskanych przez film.

W detalach filmu można będzie również zobaczyć "składowe" rankingu.

Zanim przejdziemy do szczegółów o filmie, zobaczcie, co Angular pozwala Wam zrobić z widokiem.

6. Nadawanie klasy, dodawanie klas

Pierwsza rzecz, jaką chciałabym zrobić, to nadanie parzystym kartom z filmami innego koloru tła, żeby łatwiej było odróżnić, gdzie się kończy a gdzie zaczyna nowy opis filmu.

Można to zrobić na kilka sposobów, na przykład dodać w widoku ```films.component.html``` zmienną lokalną w pętli *ngFor (pętla która generuje karty z filmami), a tam umieścić zmienną lokalną index. Będzie ona odpowiadała indeksowi elementu w tablicy. Na podstawie indeksu elementu tablicy, można dodawać/usuwać klasę elementowi.

```html
<mat-card class="films__item" *ngFor="let film of films; let i = index">
```

Następnie do pliku ```films.component.scss``` dodaj klasę .even, która będzie zawierała regułę CSS z kolorem tła dla elementu nieparzystego.

```css
.even {
    background-color: #f3f3f3;
}
```

Następnie wróć do pliku komponentu filmu ```films.component.html``` i do komponentu ```<mat-card>``` dodaj klasę ```even``` tylko wtedy, gdy element jest nieparzysty: ```[class.even]="i%2 !== 0"```
Tak powinien wyglądać template dla ```<mat-card>``` dla filmów.

```html
<h1>{{ title }}</h1>
 <section class="films__list" *ngIf="films.length">
   <h1>Films</h1>
   <mat-card class="films__item" [class.even]="i%2 !== 0"  *ngFor="let film of films; let i = index">
      <mat-card-header>
        <mat-card-title>{{ film.title }}</mat-card-title>
        <mat-card-subtitle>{{ film.genres}}</mat-card-subtitle>
      </mat-card-header>
      <mat-card-content>
        <div class="rating">
          <i class="material-icons">star_rate</i>
          <i class="material-icons">star_rate</i>
          <i class="material-icons">star_rate</i>
          <i class="material-icons">star_rate</i>
          <i class="material-icons">star_rate</i>
          <i class="material-icons">star_rate</i>
          <i class="material-icons">star_rate</i>
          <i class="material-icons">star_rate</i>
          <i class="material-icons">star_rate</i>
          <i class="material-icons">star_rate</i>
        </div>
        <img 
          class="films__item films__item_image" 
          mat-card-image 
          src="{{ film.posterurl }}">
        <mat-card-subtitle>{{ film.storyline }}</mat-card-subtitle>
      </mat-card-content>
      <mat-card-actions>
        <button mat-icon-button>Details</button>
      </mat-card-actions>
  </mat-card>
 </section>
```

Powyższy przykład służył tylko i wyłącznie, żeby pokazać, jak można dodawać inne klasy do elementów template, zmeniając ich style wyświetlania. 

Oczywiście na zaznaczanie elementów parzystych jest znacznie lepszy sposób - w stylach komponentu ```films.component.scss```, korzystając z pseudo-klasy CSS ```nth-child(even)``` - która pobiera element dziecko, nieparzyste i jego możemy ostylować. Dla przeciwieństwa - parzyste pobieramy za pomocą "odd".

```css
.films__item:nth-child(even) {
    background-color: #f3f3f3;
}
```

Dla czystości kodu, usuń klasę .even ze stylów komponentu i dodawanie klasy even ```[class.even]``` w widoku komponentu. Deklarację zmiennej lokalnej, do której przypisujemy indeks elementu tablicy, możesz zostawić.

Do klasy komponentu dodaj metodę, która obliczy średnią ocenę filmu i zwróci wynik w postaci stringa. Metoda korzysta z metody JS "reduce" a następnie średnią (z nieskończoną ilością liczb po przecinku), zaokrągla za pomocą metody "toFixed" do ilości miejsc (w tym przypadku 2) podanych w argumencie.

```films.component.ts```
```JavaScript
public avarageRating(ratings: number[]): string {
    return (ratings.reduce((prev, curr) => prev + curr, 0) / ratings.length).toFixed(2);
}
```

a następnie za pomocą interpolacji (podwójne wąsy {{}}) - osadź wynik w widoku komponentu:

```films.component.html```
```html
<mat-card-content>
    <!-- osadź średni ratin w widoku -->
    <div class="rating__label">
        Średni rating: {{ avarageRating(film.ratings) }}
    </div>
    <div class="rating">
        <i class="material-icons">star_rate</i>
          
```
Zmienię jeszcze trochę strukturę template dla listy filmów. Obecnie karta z opisem zajmuje zbyt dużo miejsca.


1. W films.component.ts wyedytuje template listy z filmami

```html
<h1>
   {{ title }}
</h1>
<section class="films__list" *ngIf="films.length">
    <h1>Films</h1>
    <mat-card class="films__item" *ngFor="let film of films; let i = index">
        <img 
        class="films__item_image" 
        mat-card-image 
        src="{{ film.posterurl }}">  
        <mat-card-content>
          <mat-card-header>
            <mat-card-title>{{ film.title }}</mat-card-title>
            <mat-card-subtitle>{{ film.genres}}</mat-card-subtitle>
          </mat-card-header>
          <div class="films__item_content rating__label">Średni rating: {{ avarageRating(film.ratings) }}</div>
          <div class="films__item_content rating">
            <i class="material-icons">star_rate</i>
            <i class="material-icons">star_rate</i>
            <i class="material-icons">star_rate</i>
            <i class="material-icons">star_rate</i>
            <i class="material-icons">star_rate</i>
            <i class="material-icons">star_rate</i>
            <i class="material-icons">star_rate</i>
            <i class="material-icons">star_rate</i>
            <i class="material-icons">star_rate</i>
            <i class="material-icons">star_rate</i>
          </div>          
          <div class="films__item_content">{{ film.storyline }}</div>
        </mat-card-content>
        <mat-card-actions>
            <button mat-flat-button color="primary">Details</button>
        </mat-card-actions>
    </mat-card>
</section>
```

2. W pliku films.components.scss wyedytuj style:

```css
.films__item {
    // margin-bottom: 20px;
    // padding: 24px;
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    margin-bottom: 24px;
}

.films__item_content {
    padding-left: 16px;
}

.films__item_image {
    width: 100px;
    height: 100%;
}

.mat-card-image {
    margin: 0;
}

.mat-card-image:first-child {
    margin: 0;
}

.films__item_content {
    margin-left: 12px;
}

div.rating {
    i.material-icons {
        color: darkorange;
        width: 22px;
    }
}
```

Usunę też niebieskie tło z sidebar, czyli cała klasę .nav {} w pliku  app.components.scss.

## Event Binding

Jak już pisałam, event binding pozwala nam na przesyłanie informacji z template do źródła danych (do klasy komponentu). Event binding jest potrzebny do tego, by np wykonać jakies akcje w odpowiedzi na zachowanie użytkownika, np. naciśnięcie przycisku.

Obecnie w liście filmów, dla każdej pozycji mamy przycisk: "Detale". 
Sprawmy, by po kliknięciu w niego, pokazały nam się wszystkie informacje o danym filmie.

### 1. Dodajmy sekcję, w której umieścimy pełna zawartość o filmie - utwórzmy nowy komponent.

Możemy samodzielnie utworzyć nowy folder w aplikacji  a w nim plik o nazwie film-details.component.html lub za pomoca CLI wygenerować pliki w folderze films w /components (ten komponent jest powiazany z komponentem films, więc powinien znaleźć się wewnatrz niego):

```JavaScript
ng g c components/films/film-details
```

Jak Angular CLI zakończy generowanie komponentu, w konsoli powinien się wyświetlić komunikat:

```JavaScript
CREATE src/app/components/films/film-details/film-details.component.html (31 bytes)
CREATE src/app/components/films/film-details/film-details.component.spec.ts (664 bytes)
CREATE src/app/components/films/film-details/film-details.component.ts (293 bytes)
CREATE src/app/components/films/film-details/film-details.component.scss (0 bytes)
UPDATE src/app/app.module.ts (891 bytes)
```

Jak widać w ostatniej linijce, zostały naniesione zmiany do pliku app.module.ts. Angular CLI, tworzac komponent, od razu importuje go do głównego modułu aplikacji i my nie musimy już o tym pamiętać.

Otwieramy plik ```film-details.component.ts``` i sprawdzamy, jak nazywa się selektor, po którym będziemy mogli odnieść sie do komponentu jako dyrektywy w template.
W moim przypadku jest to selector ```mov-film-details```.

Umieszczam komponent w template ```films.component.html``` zaraz za komponentem 
```<mat-card-actions>``` - będzie to dodatkowa część widoku wyświetlana tylko po kliknięciu przycisku "Detale".

```html
<mat-card-actions>
    <button mat-flat-button color="primary">Details</button>
</mat-card-actions>
<mov-film-details></mov-film-details>
```

Powinniście zobaczyć w aplikacji tekst: "film-details works!".

Wizualnie jednak nie wyglada to dobrze, bo wcześniej w stylach opisałam, żeby wszystkie elementy w mat-card układały się obok siebie, więc nasz opis się nie mieści. Musimy go przenieść na dół, pod opis filmu, dlatego przebuduję trochę strukturę template componentu ```films.component.html```. Cała zawartość ```<mat-card>``` opakowałam w div i zmieniłam klasy - mat-card jest wrapperem dla wszystkich danych  o filmie i wszystkie "dzieci" tego elementu będa układały się w kolumnie, czyli jeden pod drugim. 
Tak właśnie mamy poszczególne elementy zagnieżdżone:  ```<div class="films__item" >```, oraz nasz ``` <mov-film-details></mov-film-details>```. Póki co, jest on widoczny, ale za chwilę go ukryjemy i pokażemy tylko na kliknięcie.

 ```films.component.html``` - cały plik films.component.html
 ```html
<h1>
   {{ title }}
</h1>
<section class="films__list" *ngIf="films.length">
    <h1>Films</h1>
    <mat-card class="films__wrapper" *ngFor="let film of films; let i = index">
        <div class="films__item">
            <img 
            class="films__item_image" 
            mat-card-image 
            src="{{ film.posterurl }}">  
            <mat-card-content>
              <mat-card-header>
                <mat-card-title>{{ film.title }}</mat-card-title>
                <mat-card-subtitle>{{ film.genres}}</mat-card-subtitle>
              </mat-card-header>
              <div class="films__item_content rating__label">Średni rating: {{ avarageRating(film.ratings) }}</div>
              <div class="films__item_content rating">
                <i class="material-icons">star_rate</i>
                <i class="material-icons">star_rate</i>
                <i class="material-icons">star_rate</i>
                <i class="material-icons">star_rate</i>
                <i class="material-icons">star_rate</i>
                <i class="material-icons">star_rate</i>
                <i class="material-icons">star_rate</i>
                <i class="material-icons">star_rate</i>
                <i class="material-icons">star_rate</i>
                <i class="material-icons">star_rate</i>
              </div>          
              <div class="films__item_content">{{ film.storyline }}</div>
            </mat-card-content>
            <mat-card-actions>
                <button mat-flat-button color="primary">Details</button>
            </mat-card-actions>
          </div>        
        <mov-film-details></mov-film-details>
      </mat-card>
    
</section>

 ```
Zmieniłam również stylowanie komponentu oraz zastosowałam "możliwości" składniowe SASS:
```films.component.scss```

```css
.films__wrapper {
    display: flex;
    flex-direction: column;
    justify-content: center;    
    margin-bottom: 24px;
}

.films__item {
    // margin-bottom: 20px;
    // padding: 24px;
    display: flex;
    flex-direction: row;
    justify-content: flex-start;

    &_content {
        padding-left: 16px;
        margin-left: 12px;
    }

    &_image {
        width: 100px;
        height: 100%;
    }
}

.mat-card-image {
    margin: 0;

    &:first-child {
        margin: 0;
    }
}

div.rating {
    i.material-icons {
        color: darkorange;
        width: 22px;
    }
}
```
Jak uruchomimy aplikację widzimy, ze pod opisem filmu pojawił się domyślny tekst z template komponentu film-details.component.html, utworzony przez Angular CLI - "film-details works!"

Teraz czas na pokazywanie/ ukrywanie komponentu.

W pliku ```films.component.ts``` dodaj do klasy właściwość (property) o nazwie 
```detailsVisible``` i ustaw jej wartość na false. Oznacza to, że domyślnie ukryjemy blok z detalami.

```JavaScript
export class FilmsComponent implements OnInit {
  public title = 'Biblioteka filmów';
  public films: Films[];
  public detailsVisible = false;

  constructor() {
    this.films =  data.default;
  }
```

Tak, nadal go widzimy, ponieważ nie nanieśliśmy jeszcze zmian do templateu z filmami.

Wejdź do pliku ```films.component.html``` i odszukaj komponent ```<mov-film-details></mov-film-details>```. Dzięki dyrektywie strukturalnej *ngIf możemy manipulować drzewem DOM i w zależności od potrzeby, dodawać lub usuwać elementy struktury DOM. Dyrektywa strukturalna charakteryzuje się tym, że zapisujemy przed nia gwiazdkę (asterix *), co oznacza, że ona zmieni strukturę DOM. Nie dodajemy nawiasów ani cudzysłowiów.

Sama gwiazdka (* - asterix) - to taki "syntactic sugar" dla bardziej złożonej składni. Wewnętrznie, Angular tłumaczy atrybut *ngIf do elementu ```<ng-template>```, którym opakowuje hostujacy element, mniej więcej to wyglada tak:

```html
<ng-template [ngIf]="detailsVisible">
  <div class="details">{{film.details}}</div>
</ng-template>
```

Dyrektywa *ngIf jest przenoszona do elementu ```<ng-template>``` a tam następuje bindowanie property [ngIf].
W środku template znajduje się reszta struktury (template). Jesli warunek zostanie spełniony, ta właśnie reszta struktury strony zostanie wyświetlona.

### Templates
Tak też działaja template w Angular.

Za pomoca 'ng-template' możemy zdefiniować kawałek struktury HTML. Nie zostanie ona bezpośrednio wyświetlona, a dopiero to, co znajduje się wewnatrz niej.

Angular dostarcza trzech wbudowanych dyrektyw strukturalnych (build-in directives) - *ngIf, *ngFor, *ngSwitch

Dyrektywę dodajemy do elementu hostujacego, czyli do elementu, na którym chcemy manipulować, w naszym przpadku - mov-film-details.

Jeśli property klasy ```detailsVisible``` jest ustawione na false - usuwamy detale filmu ze struktury, zaś jeśli jest ustawione na true - dodajemy do struktury:

```html
<mov-film-details *ngIf="detailsVisible"></mov-film-details>
```

Teraz napiszemy funkcję, która pozwoli nam wyświetlić detale filmu na kliknięcie a na ponowne kliknięcie - ukryć. Nazwę tę metodę ```toggleDetails()```, ponieważ będzie ona nam zmieniała ustawieni widoczności z true na false lub z false na true, w zależności, jak jest ustawione.

```JavaScript
  public toggleDetails(): void {
    this.detailsVisible = !this.detailsVisible;
  }
```
Metoda musi być publiczna, ponieważ będziemy wykorzystywać ja w template komponentu. Nic nam nie zwraca, a jedynie zmienia wartość property.

Aby użyć naszej metody, musimy obsłużyć w template kliknięcie przycisku "Details" - tu wykorzystamy ```Event Binding```.

Event Bindign identyfikujemy w template po zapisie:
(click) = "wartosc"

W naszym przypadku - komponent nasłuchuje na kliknięcie (event click) na przycisku. Nazwa zboudnowanego eventu jest umieszczona w nawiasach okraglych, określa cel zdarzenia. Po prawej stronie przypisania mamy wyrażenie będace metoda komponentu wraz z nawiasami () które wywołuja metodę -  umieszczone w ciapkach. Oznacza to, że jak wystapi zdarzenie kliknięcia w przycisk, zostanie uruchomiona metoda przekazana w ciapkach.

```films.component.html```
```html
 <mat-card-actions>
      <button 
      (click)="toggleDetails()"
      mat-flat-button color="primary">Details</button>
  </mat-card-actions>
```

Teraz ukrywanie i pokazywanie detali komponentu w karcie działa, natomiast zauważ, że ukrywanie i pokazywanie odbywa się dla wszystkich filmów. Obsłużymy to w kolejnych krokach - przy tworzeniu komponentów zagnieżdżonych.

Ciekawostka: lista eventów: https://developer.mozilla.org/pl/docs/Web/Events


Zostawmy na chwilę komponent detali. Jak jestśmy przy bindingu, przejdźmy do ```two-way``` data binding.

## TWO-WAY BINDING

Zwykle, gdy pracujemy z elementami HTML, w których użytkownik może wpisywać dane (np pole input), zwykle chcemy żeby dane, które modyfikuje użytkownik, od razu zmieniały się też na stronie, tzn.
One-way binding pozwala nam tylko wyświetlać dane na widoku, ale jak użytkownik np zmieniłby te dane za pomoca pola ```<input>``` to ta zmiana nie miałaby żadnego wpływu na wartość przechowywana w komponencie.

Aby to uzyskać, potrzebujemy two-way bindinig, czyli przekazywanie danych z klasy do template i template do klasy.

W Angularze 2-way binding zapisujemy za pomoca dyrektywy ngModel opakowana w nawiasy [()] - tzw. "Banana in a Box", która musimy zaimportować do komponentu. Umieszczamy ngModel w nawiasach kwadratowych [], aby wskazać powiazanie property z property klasy do input element oraz w nawiasach okragłych () - by wskazać powiazanie zdarzenia, żeby wysłać powiadomienia o wprowadzonych przez użytkownika zmianach, z powrotem do property klasy. () - bindowanie z widoku do źródła danych, [] - bindowanie ze źródła danych do widoku.

Dodaj do pliku ```films.component.html``` pole tekstowe do wprowadzania nazwy w filtrze:

```<input [(ngModel)]='listFilter'>```

listFilter - może być lista filtrów, po których chcemy filtrować np. tytuły.
Dodajmy taki input do pliku ```films.component.html``` oraz property do klasy komponentu ```films.component.ts```:

```JavaScript
export class FilmsComponent implements OnInit {
  public title = 'Biblioteka filmów';
  public films: Films[];
  public detailsVisible = false;
  public listFilter = 'lab';
```

Póki co, w konsoli rzuca błędem. Musimy powiazać dyrektywę ngModel z komponentem. Za każdym razem kiedy chcemy użyć angularowej dyrektywy w template, musimy zastanowić się, jak sprawić, zeby była ona widoczna dla komponentu, z którym ten template jest powiazany.

Przypomnijmy, że moduł Angulara definiuje granicę lub kontekst, w którym komponent rozwiązuje swoje dyrektywy i zależności.

Chcemy użyć dyrektywy ngModel dla komponentu ```films.component.ts```, który należy do modułu AppModule w pliku app.module.ts. W zwiazku z czym musimy tu zaimportować system modułów, który będzie eksponował dyrektywę ngModel. 
Dyrektywa ngModel jest najczęściej używana przy budowie formularzy, stad też znajdziemy ja w module ```FormsModule```.  Należy zaimportować go do modułu aplikacji:

```app.module.ts```
```JavaScript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
```

oraz to tablicy importów:

```JavaScript
 imports: [
    ...
    FormsModule,
    ....
```

Odtad wszystkie dyrektywy Angularowe dotyczace formularza będa dostępne dla wszystkich komponentów, należacych do AppModule.

Teraz możemy wykorzystać two-way binding do wyświetlenia tego, co użytkownik wpisał w polu "input" jako tekst do filtrowania. 
Dopiszmy do pliku ```<h4>Filtered by: {{ listFilter }}</h4>``` i niech nasz  plik ```films.component.html``` wyglada następujaco:

```html
<h1>Films</h1>
    <input [(ngModel)]='listFilter'>
    <h4>Filtered by: {{ listFilter }}</h4>
          .....
```

Two-way binding właśnie zaczał działać. Przetestuj.
Uruchom aplikację, wpisz do pola "input" dowolny znak i zobaczysz, że to co wpiszesz, wyświetli sie po tekście: "Filtered by:".

Oczywiście filtrowanie wyników nie jest jeszcze obsłużone, zajmiemy się tym za chwilę. 
Jako ciekawostkę warto dodać, że Angular nie oferuje żadnych Pipes do filtrowania czy sortowania danych tłumacząc, że takie rozwiązanie byłoby zbyt kosztowne performanceowo. Angular zostawia nam obsługę filtrowania/sortowania w samym komponencie.

## Pipes

Pipes to klasy udekorowane dekoratorem @Pipe, które pobieraja dane i przekształcaja je. Angular posiada kilka wbudowanych @Pipe, ale można też pisać własne. 
Pipe używamy ich w template w iterpolacji, po znaku |
Możemy łaczyć pipe'y ( value | pipe1 | pipe2 | pipe3 )
Możemy przekazywać do pipe'ów argumenty ( value | pipe1: argument : argument)


Pipe pozwalaja np. przekształcić tekst na wielkie litery, albo do kwoty dopisać walutę i wyświetlić w template przekształcona wartość.

W naszej aplikacji - w bazie danych, filmy posiadaja property ```genres```, którymi jest tablica stringów. Użyjemy wbudowanego Pipe ```uppercase``` do przekształcenia wartości na wielkie litery.

Uppercase działa tylko na stringi i zwraca string. Tablicę stringów połaczę więc w jeden łańcuch za pomoca separatora (przecinek) i użyję do tego metodę ```join(',')```.

```JavaScript
film.genres.join(',') | uppercase
```
Gatunki filmów powinny wyświetlić się pisane wielka litera.

Lista dostępnych wbudowanych Pipe'ów:

https://angular.io/guide/pipes#pipes

Nie wyglada jednak zbyt estetycznie łaczenie w template elementów tablicy.
Dodatkowo, chcę zmienić formatowanie tekstu i zamiast całego tekstu wielka litera chce napisać pierwsza literę wielka a resztę małymi.
Angular nie dostarcza nam takiego wbudowanego pipe. Mamy dostępne tylko transformacje do małych lub wielkich liter.
Możemy więc napisać taki pipe samodzielnie a potem użyć w dowolnym innym miejscu w aplikacji (oczywiście importujac custom pipe).

Utwórz w folderze ```src/app/components``` folder ```shared/pipes``` a w nim plik ```first-upper.pipe.ts``` lub wykonaj polecenie Angular CLI:
```JavaScript
ng generate pipe components/shared/pipes/first-upper
```

Zostana wygenerowane pliki z pipe.
Angular automatycznie doda import do AppModule.

Pipe należy importować do modułu, w którym znajduje się komponent, który potrzebuje do działania tego Pipe. W naszym przypadku, potrzebujemy pipe w komponencie FilmsComponent, który należy obecnie do modułu AppModule. W związku z tym, Pipe importujemy w AppModule.

```JavaScript
import { FirstUpperPipe } from './shared/pipes/first-upper.pipe';
```
oraz do tablicy ```declarations```
```JavaScript

@NgModule({
  declarations: [
    AppComponent,
    ...
    FirstUpperPipe
  ],

```
Jak już dołaczyliśmy nasz customowy Pipe, zobacz, co jest w środku.
Otwórz plik
```first-upper.pipe.ts```.

W nim znajduje się definicja klasy udekorowana dekoratorem @Pipe. Każdy Pipe musi implementować metodę ```transform```, która przyjmuje dwa argumenty 
- wartość, która będziemy przekształcać
- argumenty, które możemy przekazać do pipe (opcjonalnie)

Domyślnie wygenerowany pipe zwraca nam null, ale chcemy, żeby zwrócił przetworzona wartość - każdy string w tablicy ma być napisany pierwsza wielka liter.

```JavaScript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'firstUpper'
})
export class FirstUpperPipe implements PipeTransform {

  transform(value: any, args?: any): any {
    return null;
  }

}
```
Zauważ, że dekorator @Pipe() przyjmuje obiekt z metadanymi. Każdy pipe musi mieć nazwę, po którym wywołamy pipe w template. Tutaj nazwa jest ```firstUpper```.

Żeby sprawdzić samo działanie nowo utworzonego Pipe, zwrócmy dowolna wartość, np string "test".

```JavaScript
transform(value: any, args?: any): any {
    return 'test';
  }
```

i użyjmy naszego customowego Pipe w template filmów, dla opisu
```films.component.html```
```html
<div class="films__item_content">{{ film.storyline | firstUpper }}</div>
```
Zobacz, że zamiast opisu, zostanie zwrócony tekst "test".

Napiszmy kod, który pobierze wszystkie elementy tablicy i zwróci przetransformowane string w postaci pierwszej wielkich liter.

Jednocześnie zauważ, że w metodzie transform definiuję typy argumentów:
- value jest tablicą stringów
- args - jest opcjonalne (na razie nie używamy), równie dobrze, możemy go usunąć z deklaracji funkcji
- zwracany typ - string


```JavaScript
export class FirstUpperPipe implements PipeTransform {
  transform(value: string[]): string {
    let temp = ''; 
    for (const item of value ) {
      temp += item.toUpperCase().charAt(0) + item.toLowerCase().substr(1) + ',';
    }
    return temp;
  }

}
```

lub krócej...Metoda reduce działa na tablicach i przyjmuje dwa argumenty - funkcję tzw. callback oraz wartość początkową (w naszym przypadku pusty string). W callbacku mamy też mamy dwa argumenty, gdzie prev - jest wartością poprzednich elementów tablicy, zaś curr - wartością aktualną.

```JavaScript
export class FirstUpperPipe implements PipeTransform {
  transform(value: string[]): string {
    return value.reduce((prev, curr) => `${prev}, ${curr}`, '' );
  }
}
```

I zmieńmy w template ```films.component.html``` z 
```JavaScript
<mat-card-subtitle>{{ film.genres.join(',') | uppercase }}</mat-card-subtitle>
 ```

na 

```html
 <mat-card-subtitle>{{ film.genres | firstUpper }}</mat-card-subtitle>
```

Jednocześnie usuńmy pipe | firstUpper i zostawmy tylko:
```html
<div class="films__item_content">{{ film.storyline }}</div>
```

No dobrze. Dodałam do Pipe jeszcze możliwość dodawania argumentu. Oznacza to, że jeśli przekażemy do pipe argument (a zakładam że jest on opcjonalny, stąd w definicji funkcji typ argumentu ma znak zapytania), to lista elementów z tablicy zostanie połączona w jeden string za pomocą tego separatora. Jeśli nie przekażemy żadnego argumentu, domyślnie zostanie użyty jako separator przecinek.

```JavaScript
export class FirstUpperPipe implements PipeTransform {

  transform(value: string[], separator: string): string {
    return value.reduce((prev, curr) => `${prev}${separator ? separator : ','} ${curr}`, '' );
  }

}
```

Wypróbujmy nasz kod
```films.component.html```
```html
<mat-card-subtitle>{{ film.genres | firstUpper: '-'}}</mat-card-subtitle>
```
Użyłam naszego pipe i przekazałam argument - separator: '-'.

Oczywiście do Pipe możemy przekazać kilka argumentów wypisując je podwukropkach, a następnie wykorzystać je w pipe. Tego nie musicie pisać, ale możecie przetestować sobie działanie:

```NIE ZOSTAWIAJ TEGO W KODZIE```
```JavaScript
  transform(value: string[], separator = ',', sep2?: string): string {
    return value.reduce((prev, curr) => `${prev}${sep2 ? sep2 : separator} ${curr}`, '' );
  }
```
Przekształciłam funkcję transform tak, że jako drugi parametr otrzymuje separator (jeśli ktoś nie przekaże argumentu to domyślnie separator zostanie ustawiony na przecinek). Dodałam też drugi argument, który jest opcjonalny. To, co się dzieje wewnątrz funkcji to jeśli zmienna ```sep2``` została podana to zaaplikujemy ją jako separator, a jeśli nie, to użyjemy wartości pod zmienną ```separator```. Oznacza to, że jeśli ktoś użył samego pipe bez argumentów, to domyślnie zmienna ```separator``` zostanie ustawiona na przecinek. Z kolei zmiennej ```sep2``` nie będzie więc jako separator zostanie użyty przecinek - domyślny.
Jeśli ktoś użyje pipe z jednym argumentem, ale nie poda drugiego, to do transformacji, jako separator zostanie użyty separator podany w argumencie.
Jeśli ktoś poda wszystkie wartości, zgodnie z definicją funkci, jako separator zostanie użyta wartość drugiego argumentu:

```NIE ZOSTAWIAJ TEGO W KODZIE```
```html
<mat-card-subtitle>{{ film.genres | firstUpper: '-' : '*'}}</mat-card-subtitle>
```

Ostatecznie nasz Pipe powinien wyglądać tak:

```JavaScript
export class FirstUpperPipe implements PipeTransform {

  transform(value: string[], separator?: string): string {
    return value.reduce((prev, curr) => `${prev}${separator ? separator : ','} ${curr}`, '' );
  }

}

```

a w template ```films.component.html```:
```html
<mat-card-subtitle>{{ film.genres | firstUpper }}</mat-card-subtitle>
```

Jeszcze jeden mały szlif. Przy obecnej implementacji custom Pipe, pierwszym znakiem, jaki się pojawia w przekształconej wartości, jest przecinek (",Drama, Mystery, Thriller"). Nie chcemy, żeby przecinek się wyświetlał, jeśli nie było w tablicy pierwszego tekstu. 

Przeróbmy trochę funkcję tak, by dla elementu o indeksie 0 dołączyła do wynikowej wartości tylko bieżącą wartość, a gdy element tablicy nie jest pierwszym elementem, żeby dodała separator.

```JavaScript
return value.reduce((prev, curr, ind) => {
      if (ind !== 0 ) {
        return `${prev}${separator ? separator : ','} ${curr}`;
      } else {
        return curr;
      }
    }, '' );
```

Możemy zapis skrócić do jednej linii, posługując się operatorem trynarnym. Operator trynarny to operator o konstrukcji:

```JavaScript
warunek === true ? zrobA : zrobB
```

Oznaczający, że jeśli warunek jest spełniony, należy wykonać 'zrobA', a jeśli nie jest spełniony, 'zrobB'.

```JavaScript
  transform(value: string[], separator?: string): string {
    return value.reduce((prev, curr, ind) => ind !== 0 ? `${prev}${separator ? separator : ','} ${curr}` : curr, '');
  }
```

Oto mamy gotowy działający Pipe, który przekształca tablicę stringów w jeden string połączonych ze sobą elementów za pomocą separatora, gdzie każdy string z tablicy pisany jest pierwszą wielką literą i resztą małych.

### 2. Lifecycle Hooks - cyli cykle życia komponentu

Komponent ma cykl życia zarządzany przez Angular.
Angular tworzy komponent, renderuje go, tworzy i renderuje jego dzieci, sprawdza, kiedy zmieniają się powiązane z nim propertiesy, niszczy go zanim wyrzuci go z DOM.

Dyrektywy mają te same cykle życia.
Dzięki tym kluczowym momentom z cyklu życia możemy uruchamiać pewne działania. 
Komponenty mogą implementować jeden lub wiele interfejsów cyklu życia,ale jak już zaimplementujemy interfejsy (np. ```export class SomeComponent implements OnInit```), to musimy do komponentu dodać pojedyncze metody które je obsłużą. Metody te są prefiksowane ```ng```. Jednym z takich lifecycle hooks jest OnInit interfejs, który wymaga metody ngOnInit(); 

```JavaScript
export class SomeComponent implements OnInit {
    constructor() {}

    ngOnInit() { }
}
```

Lifecycle hook ngOnInit jest on automatycznie dodawany do klasy komponentu, kiedy generujemy komponent z Angular CLI.
Oczywiście, jeśli metodę pozostawiamy pustą, czyli jej nie potrzebujemy, możemy usunąć ją, jak i implementację interfejsu.

W ```ngOnInit()``` powinniśmy inicjalizować komponent po tym, jak Angular zainicjuje właściwości powiązane z danymi.
Nie należy zamieszczać tu kodu, który jest potrzebny do utworzenia instancji komponentu. Jest to dobre miejsce do uzyskiwania danych z serwisów backendowych.
Kod niezbędny do utworzenia instancji komponentu powinien znajdować się w konstruktorze.

<b>Konstruktor</b> klasy to funkcja, która jest wykonywana kiedy komponent jest inicjalizowany po raz pierwszy.

```ngOnChanges``` lifecycle hook wykonuje akcje po tym, jak Angular ustawi dane związane z input propertisami (@Input() - o tym za chwilę).

```ngOnDestroy``` - czyści komponent zanim go zniszczy.

```Lista dostępnych lifecycle hooks:```
https://angular.io/guide/lifecycle-hooks



### Obsługa filtrowania

Wróćmy do filtrowania filmów po tytule.
W pliku films.component.ts zadeklarowaliśmy property, któremu na sztywno przypisaliśmy wartość 'lab' - czyli już na wstępie ustawiliśmy na liście filtrów filtrowanie po "lab".

```JavaScript
public listFilter = 'lab'; 
```

Jeśli chcemy przefiltrować filmy po tytułach, musimy:
- mieć przefiltrowaną listę filmów, którą będziemy chcieli powiązać. Zdefiniujmy dla niej property w komponencie - będzie to lista (tablica) z filmami - użyjemy typowania i typu danych Film.

```JavaScript
public filteredFilms: Film[];
```

    Nie możemy po prostu przefiltrować po tablicy filmów bez użycia pomocniczego property, ponieważ kiedy przefiltrowalibyśmy tablicę filmów, stracilibyśmy oryginalne dane. Mamy tu 2-way data binding - przekazywanie danych z komponentu do widoku i nadpisywanie z widoku do komponentu. Musielibyśmy ponownie pobrać dane ze źródła, żeby je odzyskać.

- Jako dalszy step w tworzeniu filtra, musimy wiedzieć, kiedy użytkownik zmieni kryteria filtrowania. Moglibyśmy użyć event bindingu i nasłuchiwać na wciśnięty klawisz lub zmianę wartości pola input, ale jest łatwiejsze rozwiązanie - zmiana property przechowującej wyszukiwany filtr - property listFilter.
Ustawienie gettera i settera na property zamiast 
```   public listFilter = 'lab'; ```

możemy ustawić getter i setter:

```JavaScript
  public _listFilter: string;

  get listFilter(): string {
      return this._listFilter;
  }

  set listFilter(value: string) {
      this._listFilter = value;
  }
```

Getter i setter działają jak zwykłe property. Kiedy powiązanie danych potrzebuje wartości, zostanie zawołany getter i pobierze wartość.

Wykorzystując getter (get listFilter()), pobieramy ją jak zmienną, czyli po prostu this.listFilter;

Za każdym razem kiedy użytkownik zmieni wartość, powiązanie danych zawoła setter, dołączając zmienioną wartość.
Jeśli chcemy dołączyć jakąś logikę za każdym razem, gdy wartość się zmienia, robimy to w setterze. Np. sortowanie danych.

My chcemy ustawić przefiltrowaną tablicę filmów do przefiltrowanej listy filmów. Jeśli w liście filtrów nic nie ma, to po prostu do przefiltrowanych filmów przypisujemy listę wszystkich filmów. Jeśli jakieś filtry znajdują się na liście filtrów, aplikujemy te filtry wykorzystując metodę setFilters();

```JavaScript
this.filteredFilms = this.listFilter ? this.setFilters(this.listFilter) : this.films;
```

Funkcja this.setFilters przyjmuje jako argument string, którym jest filtr, a jako wynik funkcji zwracamy tablicę filmów.
Nie chcemy robić porównywania nazw case sensitive, więc zmienię tekst filtru na małe litery. Następnie przefiltruję tablicę filmów zwracając nową tablicę tylko z tymi filmami, które w tytule posiadaja słowo kluczowe, po którym filtrujemy. 
Metoda indexOf() zwraca pozycję w ciągu znaków, w której znajduje się pierwsze wystąpienie szukanego znaku/ciągu. Metoda zwróci -1, gdy nic nie zostanie znalezione.

```JavaScript
  setFilters(filteredBy: string): Film[] {
    filteredBy = filteredBy.toLocaleLowerCase();
    return this.films.filter((film: Film) => film.title.toLocaleLowerCase().indexOf(filteredBy) !== -1);
  }
```

Mamy ustawiony getter i setter, musimy jeszcze ustawić domyślną wartość dla tablicy przefiltrowanych filmów.
Listę tę ustawiamy w konstruktorze, ponieważ powinniśmy ją zdefiniować w momencie tworzenia komponentu, a to najlepiej robić właśnie w konstruktorze. Domyślnie, jako listFilter wpisałam pusty string, domyślnie - brak kryteriów filtrowania.

```JavaScript
 constructor() {
    this.films =  data.default;
    this.filteredFilms = this.films;
    this.listFilter = '';
  }
```

Ostatnim krokiem jest zmiana w template films.component.html.

Obecnie wyświetlamy filmy polegając na pełnej tablicy dostępnych filmów. Musimy zmienić to na tablicę przefiltrowanych filmów.
Gdy nie będziemy filtrować, wyświetli się pełna lista filmów.

zamiast: 
```html
<mat-card class="films__wrapper" *ngFor="let film of films; let i = index">
```

wpisz:
```html
<mat-card class="films__wrapper" *ngFor="let film of filteredFilms; let i = index">
```

### 3. Zagnieżdżanie komponentów, komunikacja z kontenerem

Czas na zagnieżdżanie komponentów i komunikację komponentu rodzica z kompnoentem zagnieżdżonym.

## 3.1. 
Wróćmy do filmów, w których mamy rating. W obecnym kodzie mamy rating (10 gwiazdek) ustawiony na sztywno. Napiszmy oddzielny komponent, który wyświetli ten rating.

Rating umieścimy w oddzielnym komponencie z kilku powodów:
- będzie można go reużyć w innym miejscu aplikacji
- zachowana zostanie enkapsulacja logiki i template (co to oznacza? Pamiętasz, jak klikanie na przycisk "Detale" pokazywało i chowało detale filmu dla wszysktich pozycji?? No właśnie, tam nie robiliśmy oddzielnego komponentu na kartę z danymi o filmie)

Komponent z ratingiem może być reużywalny i będzie to 'dummy' komponent, służący tylko do wyświetlania gwiazdek. Nie będzie zawierał żadnej logiki, natomiasat możemy mu przekazać property z informacją, ile gwiazdek ma wyświetlić lub pokolorować.

Do utworzenia komponentu użyję Angular CLI, który od razu utworzy mi pozostałe pliki dla komponentu - css, testy i zaimportuje komponent do modułu.

```JavaScript
ng g c components/shared/components/star
```
Angular CLI utworzył mi komponent, którym mogę posługiwać się w template za pomocą dyrektywy 'mov-star'.

Zobaczmy, czy działa.

Wejdź w plik ```films.component.ts``` i dodaj gdzieś w karcie filmu utworzony komponent.

```html
<mov-star></mov-star>
```
Teraz przeniosę całą zawartość o ratingu do template star.component.html.

Zawartość pliku ```films.component.html```
```html
<h1>{{ title }}</h1>
  <section class="films__list" *ngIf="films.length">
    <h1>Films</h1>
    <input [(ngModel)]='listFilter'>
    <h4>Filtered by: {{ listFilter }}</h4>
    <mat-card class="films__wrapper" *ngFor="let film of filteredFilms; let i = index">
      <div class="films__item">
        <img 
        class="films__item_image" 
        mat-card-image 
        src="{{ film.posterurl }}">  
        <mat-card-content>
          <mat-card-header>
            <mat-card-title>{{ film.title }}</mat-card-title>
            <mat-card-subtitle>{{ film.genres | firstUpper }}</mat-card-subtitle>
          </mat-card-header>
          <div class="films__item_content rating__label">Średni rating: {{ avarageRating(film.ratings) }}</div>
          <mov-star></mov-star>
          <div class="films__item_content">{{ film.storyline }}</div>
        </mat-card-content>
        <mat-card-actions>
          <button 
          (click)="toggleDetails()"
          mat-flat-button color="primary">Details</button>
        </mat-card-actions>
        </div>        
        <mov-film-details *ngIf="detailsVisible"></mov-film-details>
      </mat-card>     
  </section>
```
oraz zawartość pliku ```star.component.html```

```html
<div class="films__item_content rating">
  <i class="material-icons">star_rate</i>
  <i class="material-icons">star_rate</i>
  <i class="material-icons">star_rate</i>
  <i class="material-icons">star_rate</i>
  <i class="material-icons">star_rate</i>
  <i class="material-icons">star_rate</i>
  <i class="material-icons">star_rate</i>
  <i class="material-icons">star_rate</i>
  <i class="material-icons">star_rate</i>
  <i class="material-icons">star_rate</i>
</div>          
```

Musimy też przenieść style odpowiedzialne za wyświetlanie gwiazdek. Usuwamy style z ```films.component.scss```
```css
/* usuwamy te style */
div.rating {
    i.material-icons {
        color: darkorange;
        width: 22px;
    }
}
```

i przenosimy je do pliku ```star.component.scss```

Ok. Kolejnym krokiem jest ustawienie ilości gwiazdek (ratingu) oraz szerokość gwiazdki. 

W komponencie star.component.ts dodaj do klasy komponentu poniższe właściwości:

```JavaScript
public rating = 10;
public starVisibleWidth: number;
```
Chcemy, żeby szerokość była przeliczana ponownie za każdym razem, kiedy kontener zmieni liczbę ratingu.
Aby wykryć taką zmianę, musimy wykorzystać lifecycle hook OnChanges. Musimy zaimplementować jego interfejs do klasy komponentu:

```star.component.ts```
```JavaScript
import { Component, OnChanges } from '@angular/core';

@Component({
  selector: 'mov-star',
  templateUrl: './star.component.html',
  styleUrls: ['./star.component.scss']
})
export class StarComponent implements OnChanges {
  public rating = 10;
  public starVisibleWidth: number;
  constructor() { }

  ngOnChanges() {
      this.starVisibleWidth = this.rating * 75 / 10;
  }

}
```
Nic się jeszcze nie dzieje, ponieważ event OnChanges nie zachodzi dla naszego komponentu. Lifecycle hood event OnChanges tylko obserwuje na zmiany inputów (@Input() property) a my ich jeszcze nie zadeklarowaliśmy. NgOnchanges się nie odpala.

Musimy zmienić dwa property w klasie StarComponent: ```rating``` i ```starWidth``` i udekorować je dekoratorem @Input(). Następnie do komponentu z ratingiem musimy przekazać rating filmu, z kontenera. W kontenerze (FilmsComponent) znajdują się informacje o wszystkich filmach, czyli o ratingu także. Musimy tę informację przekazać do komponentu StarComponent za pomocą property o nazwie, jaką ustaliliśmy w komponencie StarComponent przy dekoratorze @Input().

Jeśli zagnieżdżony komponent chce otrzymywać dane z jego kontenera, musi wyeksponować property do tego kontenera. Za pomocą tego property kontener przekaże wartość do kontenera zagnieżdżonego. Komponent zagnieżdżony te property może użyć do otrzymania danych z kontenera, używając @Input() dekoratora. 
Domyślnie, property dekorowane dekoratorem @Input() mą propertisami publicznymi i cel jest taki, by takimi pozostały.

W komponencie musimy też zaimportować dekorator. Musimy też usunąć domyślną wartość przypisaną do ratingu.

```star.component.ts```
```JavaScript
import { Component, OnChanges, Input } from '@angular/core';

export class StarComponent implements OnChanges {
  @Input() public rating: number;
  public starVisibleWidth: number;
  constructor() { }
```
Ponieważ mamy już @Input property, lifecycle hood onChanges odpali się za każdym razem, kiedy wartość Inputu z kontenera się zmieni.


## 3.2.
Następnie umieśmimy komponent z ratingiem w template filmu i do każdego z nich przekażemy dane (skalę ratingu) za pomocą propsów @Input().

Za pomoca dekoratora @Input() wyeksponowaliśmy property dla kontenera. Teraz musimy użyć tego property, by przekazać dane z kontenera do komponentu zagnieżdżonego (StarComponent).

```films.component.html```
```html
<mov-star [rating]="avarageRating(film.ratings)"></mov-star>
<!-- możesz usunąć poniższą linijkę z tego pliku:-->
<div class="films__item_content rating__label">Średni rating: {{ avarageRating(film.ratings) }}</div>
         
```

## 3.3.
Następnie obsłużymy kliknięcie użytkownika na gwiazdki. Kiedy użytkownik kliknie na nie, wywołamy event, który poinformuje o tym kontener.
Jeśli zagnieżdzony komponent chce wysłać dane z powrotem do kontenera, musi odpalić event (zdarzenie). Zagnieżdżony komponent (StarComponent) eksponuje event, który może użyć, żeby przekazać wynik do jego kontenera, używajac dekoratora @Output().

Dekoratora @Output() możemy użyć do dekorowania dowolnej property zagnieżdżonego komponentu klasy. Typem property musi być EVENT. Event jest jedynym sposobem, w jaki możemy przekazać dane z komponentu zagnieżdżonego do parenta. Dane, które przekażemy, staja sie payloadem eventu. W Angularze, event jest zdefiniowany jako obiekt EventEmitter, który posiada metodę ```emit()``` do emisji wartości.  Angular dostarcza klasę EventEmitter, która jest używana, kiedy publikowane sa wartości z komponentu, poprzez dekorator @Output().

Generatory TypeScript pozwala identyfikować specyficzny typ, z którym instancja klasy będzie współpracować. Nie musimy określać w momencie definiowana, ale w momencie użycia. Kiedy tworzymy instancję obiektu EventEmitter, generyczny argument identyfikuje typ event payloadu.

W klasie komponentu ```star.components.ts``` tworzymy nowa instancję EventEmittera:

```JavaScript
@Output() public choosedRatingNotify: EventEmitter<string> = new EventEmitter<string>();
```
Oczywiście, musimy zaimportować Output dekorator i EventEmitter (do użycia w dyrektywach i komponentach).

```JavaScript
import { Component, OnChanges, Input, Output, EventEmitter } from '@angular/core';

```

Kiedy użytkownik kliknie na gwiazdki, komponent otrzyma informację o kliknięciu. Użyjemy event binding w komponencie StarComponent do zawołania metody onStarsClick. Metoda wykorzysta property Obiektu EventEmitter, notify i zawoła metodę emit(), by podnieść event notify do kontenera. Jesli chcemy dołaczyć dane do event payloadu, dołaczamy te dane jako argument do metody .emit().

```star.component.ts```
```JavaScript
onStarClick() {
  this.choosedRatingNotify.emit('Clicked');
}
```

Żeby jeszcze komponent nam zadziałał, musimy dodać do template event binding.
```star.component.html```
```html
<div class="films__item_content star__rating"
  ...
  (click)="onStarClick()"
  ...
```

Następnie, uzyjemy property udekoraowanego dekoratorem @Output() w kontenerze, czyli w FilmsComponent. 

```films.component.html```
```html
  <mov-star 
  [rating]="avarageRating(film.ratings)"
  (choosedRatingNotify)=""
  ></mov-star>
```
i musimy przypisać metodę, która chcemy uruchomić, gdy event wyemituje wartość. Jeśli wyemitowaliśmy wartość przez EventEmitter, payload jest dostępny pod zmienna ```$event``` - w naszym przypadku - jest to string;

```html
  <mov-star 
  [rating]="avarageRating(film.ratings)"
  (choosedRatingNotify)="onRatingChanged($event)"
  ></mov-star>
```

### 5. Zacznijmy od wydzielenia modułów. 
Obecnie, w pliku <i>app.component.html</i> znajduje się html aplikacji w jednym miejscu. Potencjalnie możemy wydzielić część layoutu do zupełnie innego modułu. Ten moduł będzie mógł być reużywany w innych modułach. 

Korzystając z Angular CLI, tworzymy nowy moduł:

```JavaScript
ng g m layout
```


## SERWISY

Serwis to zwykła klasa uderokowana dekoratorem @Injectable(). 

Serwisy to świetny sposób na dzielenie się informacjami między klasami, które się nie znają. Komponenty nie powinny pobierać ani zapisywać danych bezpośrednio i na pewno nie powinny przedstawiać zahardkodowanych danych. Powinny koncentrować się na prezentacji danych i delegowaniu dostępu do danych do usługi. Serwis można wstrzyknąć w różnych komponentach jako dependencję.

```JavaScript

@Injectable({

})
export class TemplateService {

}
```

## HTTP SERWIS

Obecnie odczytujemy dane do naszej aplikacji z pliku db.json.
Przeróbmy nasz skrypt, aby pobieranie danych odbywało sie poprzez żadanie HTTP.

Większość Angularowych aplikacji używa protokołu HTTP do pozyskiwania danych z backendu. Nowoczesne przegladarki wspieraja dwa rodzaje API do robienia HTTP requestów: XMLHttpRequest Interfejs i fetch() API.  
GET Request idzie przez Web Serwisy, web serwis otrzymuje dane z bazy danych, zwykle używajac bazy danych i zwraca je do aplikacji w postaci HTTP response - odp. serwera.

W Angularze do komunikacji frontu z backendem za pomoca HTTP wykorzystujemy moduł HttpClient dostępny w @angular/common/http. Moduł jest mechanizmem do komunikacji ze zdalnym serwerem poprzez HTTP. Oferuje proste HTTP API dla Angularowych aplikacji, które opieraja się na interfejsie XMLHttpRequest oraz dostarcza funkcje testowania, typowane obiekty żadań i odpowiedzi serwera, API Observable i usprawniona obsługę błędów.

Obecnie pobieramy dane z pliku db.json.
Zmieńmy to i pobierzmy dane z requestem HTTP.

Na poczatku workshopów, mieliście zainstalować json-serwer, który posłuży nam jako API do pierania/zmiany danych.

Requesty POST, PUT, PATCH lub DELETE będa automatycznie zapisane do pliku db.json.


Z serwera możemy otrzymywać różne typy danych.

Serwis HTTP musimy zaimportować tylko raz w root AppModule.

1. Zaimportuj HttpClientModule

```JavaScript
import { HttpClientModule }    from '@angular/common/http';
```

2. Dodaj moduł do tablicy importów AppModule

```JavaScript
  imports: [
    ....
    HttpClientModule,
    ...
```

Angularowy moduł HttpClient zwraca Observable z wołanych metod HTTP, np. http.get('/api') zwraca Observable. Observable nie zmieniaja odpowiedzi z serwera (jak to jest możliwe w przypadku Promise i chainowaniu za pomoca metody .then()). Zamiast tego na Observable można użyć operatorów, które zmienia wartości response w miarę potrzeby.

Http requesty można anulować poprzez odsubskrybowanie (Observable emituje wartości po zasubskrybowaniu do niego. Observable można odsubskrybować, tzn. przestać nasłuchiwać - zaś Promise nie). Żądania można skonfigurować, aby uzyskać aktualizacje zdarzeń postępu.
Nieudane żądania można łatwo ponowić.


Obserwable pomagaja zarzadzać asynchronicznymi danymi przychodzacymi w czasie, tj. dane przychodzace z backendu. Observable traktuje takie dane jako kolekcję.
Można myśleć o Observableach jako o kolekcji, która przychodzi asynchronicznie w czasie.

Angular używa Observable jako interfejs do obsługi różnych, wspólnych asynchronicznych operacji.
- klasa EventEmitter rozszerza Observable
- HTTP moduł używa Observable do obsługi AJAX requestów i resposeów
- Router i Form Moduły używaja Observable do nasłuchiwania i odpowiadania na eventy wprowadzone przez użytkownika
Router.events dostarcza eventy jako Observable.

Observable pozwalaja manipulować zestawem eventów z operatorami.
Operatory to metody na Observableach, które tworza nowe Observable.
Każdy operator przekształca źródło Observable na swój sposób.
Operatory nie czekaja na wszystkie wartości i przetwarzaja je osobno w czasie, kiedy sa emitowane. Operatory: map, filter, take, merge ... 

Angular umożliwia subskrybowanie do Observable na dwa sposoby:
- ręcznie, używajac metody .subscribe() na Observable
- za pomoca pipe ```async``` - przewaga tego rozwiazania jest to, że async sam też odsubksrybowuje nasłuchiwanie, dzięki czemu nie ma wycieku pamięci. Przy ręcznej subskrypcji trzeba zawsze pamiętać, aby przed zniszczeniem komponentu odsubsrybować do Observable.

Dodawanie Operatorów rxjs (Reactive Extensions) i Observable

```JavaScript
import { Observable } from 'rxjs';
import { map, filter } from 'rxjs/operators';
```

Ok. przejdźmy do aplikacji.
Chcemy pobierać dane już nie z pliku db.json, ale z API. 
Aby to osiagnac, potrzebujemy wykonać request HTTP, żeby pobrać listę filmów z serwera.
Angular dostarcza HTTP Serwis, który pozwala komunikować się z backend web-serwerem używajac przyjaznego protokołu HTTP dla request i response. Returned response is an Observable.

Aby utworzyć serwis, musimy stworzyć plik films.service.ts. Możemy utworzyć go ręcznie lub wygenerować bazę z użyciem Angular CLI.

Serwisy sa dostawcami danych, więc zgodnie z zaleceniami architektury Angulara, powinny znajdować się w module Core. Później go utworzymy. Na razie po prostu utwrórzmy plik z serwisem w folderze core/services/api/films.


```JavaScript
ng g service core/services/api/films
```

Angular CLI utworzy plik serwisu oraz równolegle do niego plik z testami do serwisu.

Serwis powinien mieć strukturę:

```JavaScript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class FilmsService {

  constructor() { }
}

```

Aby móc pobierać dane z serwera, musimy zdefiniować url do API, za pomoca którego będziemy mogli pobrać dane. Musimy wykonać żadanie HTTP z użyciem metody GET pod podany URL.
Utwórzmy go.

W między czasie, poprawmy plik db.json, obecnie mamy w nim tablicę obiektów typu Film.
Aby plik był poprawnym plikiem dla naszego API, musimy opakować go w obiekt, wrzućmy więc:

```JavaScript
{
  "films": [
    // to już zawartość która była
  ]
}
```
Jednocześnie danym z pliku zmienia się ścieżka dostępu, więc musimy tę zmianę uwzględnić w miejscu, w którym odczytujemy plik w celu pobrania danych. Zmieniamy:

```films.component.ts```
```JavaScript
constructor() {
    this.films =  data.default;
```
na :

```JavaScript
constructor() {
    this.films =  data.default.films;
```

Wracajac do serwisu....

definiujemy url. Korzystamy z json-serwer do serwowania API, po uruchomieniu, jest on dostępny na porcie 3000. W zwiazku z tym, lokalnie URL do serwisu to:
'http://localhost:3000/films'.

Instancję HttpClientModule musimy zainjectować do kompnonentu/serwisu, w którym zamierzamy użyć sewisu. Importujemy HttpClient znajdujacy się w @angular/common/http

Więcej o http: https://angular.io/guide/http

```films.service.ts```

```JavaScript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';

@Injectable({
  providedIn: 'root'
})
export class FilmsService {
  private filmsUrl = 'http://localhost:3000/films';
  constructor(private http: HttpClient) { }
}
```

Zaimportowałam HttpClienta oraz zdefiniowałam właściwość klasy filmsUrl z linkiem do bazy danych filmów. Jest to informacja dla HttpClienta, gdzie wysyłamy request HTTP.

Aby móc skorzystać z HttpClienta w moim serwisie, muszę wstrzyknac go za pomoca Dependency Injection do konstruktora komponentu. Argumentowi http nadajemy modyfikator dostępu ```private``` oraz określamy jego typ jako HttpClient. Przy instancjonowaniu komponentu, HttpClient będzie skojarzony i dostępny w serwisie pod nazwa ```http```. Musimy też zarejestrować dostawcę serwisu za pomoca Angular Injectora (zrobiliśmy to w kroku 1)

Majac instancję serwisu, jesteśmy w stanie go użyć. Tworzymy metodę ```getFilms()```, która pobierze filmy z serwera za pomoca metody GET.

```films.service.ts```
```JavaScript

export class FilmsService {
  private filmsUrl = 'http://localhost:3000/films';
  constructor(private http: HttpClient) { }

  getFilms() {
    return this.http.get(this.filmsUrl);
  }
}
```

Na razie nie określamy typu zwracanych danych, zostawmy to na później.
Zazwyczaj jak zwracane sa dane z sewera backendowego, maja one format JSON. 
W przypadku Angulara, metody HttpClient pozwala na łatwe pobranie danych w formacie JSON.
Wystarczy, że napiszemy, jakiego typu danych chcemy zwrócic (używajac TypeScript generatora) i ustawiajac typ danych w generycznym parametrze metody ```.get<typ>()```, w naszym przypadku, będzie to tablica Filmów.

```JavaScript
getFilms() {
    return this.http.get<Films[]>(this.filmsUrl);
  }
```

Metoda get jest w stanie automatycznie zmapować objekt odpowiedzi zwrócony z backend sewera do zdefiniowanego typu (w tym przypadku typu tablica Filmów).
Ponieważ używamy silnego typowania powinniśmy też określić typ danych, zwracanych przez metodę http.get. Jak pisałam wcześniej, HTTP calle sa operacjami asynchronicznymi, pojedynczymi i HttpClient jako wynik requestów zwraca tylko jeden element, Observable, dlatego wynikiem zwróconym z requestu będzie Observable typu Films[]

```JavaScript
import { Film } from './../../../components/films/films';
import { Observable } from 'rxjs';

  getFilms(): Observable<Film[]> {
    return this.http.get<Film[]>(this.filmsUrl);
  }
```

Oczywiście ```Film``` i ```Observable``` musimy zaimportować.
Nie można jeszcze podejrzeć zwróconych danych, ponieważ musimy zasubskrybować do Observable, aby odtrzymać wyemitowana wartość.

Żeby móc odczytać wartość zwracana przez serwis, musimy do komponentu films.component.ts wstrzyknac nasz film.serwis.ts i wywołac metodę getFilms();

Przy requestach HTTP powinniśmy zawsze dodawać obsługę błędów. W trakcie wysyłania żądania lub odbierania odpowiedzi może wystąpić wiele problemów, np. błąd połączenia, brak dostępu do danych, itp.
Obsługę błędów możemy zapisać w pipe'able operatorze, catchError(). 
tap() operator jest z kolei dobrym sposobem na debugowanie Observable, patrzenie, co jest w ich środku w momencie, kiedy są emitowane. Działa jak console.log.

```films.service.ts```
```JavaScript
import { catchError } from 'rxjs/operators';

 getFilms(): Observable<Film[]> {
    return this.http.get<Film[]>(this.filmsUrl).pipe(
      catchError(this.handleError)
    );
  }
```

oraz obsługa błędów - metoda handleError:

```JavaScript
private handleError(err: HttpErrorResponse) {
    let errorMessage = '';

    if (err.error instanceof ErrorEvent) {
      errorMessage = `An error occured: ${err.error.message}`;
    } else {
      errorMessage = `Server returned code: ${err.status}, error message is: ${err.message}`;
    }
    console.log(errorMessage);
    return throwError(errorMessage);
  }
  ```

Ok. Jednak dane nadal pobieramy z pliku, a nie z URLa.

Zanim zaczniemy przerabiać sposób pobierania danych trzeba wiedzieć, że Observable są leniwe i nie wyemitują wartości dopóki do nich nie zasubskrybujemy, czyli wykonamy na nich funkcję ```subscribe```.

Metoda ```subscribe``` przyjmuje jako argument od zera do trzech argumentów, z czego
1. funkcja emitująca następną wartość
2. funkcja obsługująca błędy
3. funkcja wywoływana, gdy Observable zakończy emitowanie wartości.

Metoda subscribe() zwraca Subskrypcję. Możemy powołać się na nią, by przestać nasłuchiwać na Observable czyli anulować subskrypcję metodą ```unsubscribe()```.

Wróćmy do pliku ```films.component.ts``` gdzie mamy przypisanie filmów z pliku db.json do property klasy ```this.films```.

Mamy już serwis, który łączy się z serwerem backendowym (w pliku films.service.ts) i za pomocą metody get HttpClienta pobiera z URLa dane o dostępnych filmach.

Teraz trzeba podpiąć metodę naszego serwisu do komponentu films.component.ts tak, żeby pobierać dane nie z pliku, a poprzez serwis, z backendu.

Na początek do konstruktora komponentu films.component.ts musimy wstrzyknąć serwis filmów jako dependencję.  Nie musimy podawać tablicy providerów serwisu w dekoratorze komponentu, bo FilmService jest już zarejestrowany i przypisany do modułu głównego AppModule (w pliku films.service.ts);

```films.component.ts```
```JavaScript
import { FilmsService } from './../../core/services/api/films.service';
...
constructor(private filmsService: FilmsService) {
...
}
```

Teraz możemy usunąć przypisanie zawartości pliku do property ```films``` w pliku films.component.ts.

Usuwamy 
```     this.films =  data.default.films;```.


Zamiast tego zawołamy metodę ```getFilms()``` z serwisu ```films.service.ts```.

Gdzie należałoby wołać serwis?
W konstruktorze?
A może w lifecycle hood, np ngOnInit?

Konstruktor jest nam potrzebny, by stworzyć instancję klasy. 
Wołając http nie tylko wykona się żądanie http, ale też zostanie zawołany serwer backendowy, więc nasza usługa wyjdzie do serwera cackendowego i ostatecznie zwróci dane itp...
Nie ma sensu tego całego procesu wywoływać w konstruktorze. Bez tego też jesteśmy w stanie utworzyć komponent. Wołanie serwisu nie powinno więc znajdować się w konstruktorze, jest na to lepsze miejsce. ngOnInit lifecycle hook dostarcza miejsca, w którym można wykonywać wszelkie inicjalizacje komponentu i jest to doskonałe miejsce na uzyskiwanie danych które potrzebne nam są do template.

Wykonajmy zapytanie do serwera o dane:
```JavaScript
  ngOnInit() {
    this.films = this.filmsService.getFilms();
  }
```

Tu trzeba pamiętać o jednej ważnej rzeczy - konstruktor (constructor) zawsze wykonuje się przed ngOnInit, dlatego kod, który jest w konstruktorze wykona się pierwszy.
Obecnie w konstruktorze mamy:

```JavaScript
 constructor(private filmsService: FilmsService) {
    this.filteredFilms = this.films;
    this.listFilter = '';
  }
```

To oznacza, że to property ```filteredFilms``` staramy się przypisać wartość property ```films```, ale ta nie jest jeszcze ustawiona - czyli jest undefined. Jakbyśmy w konstruktorze próbowali wyrzucić na konsolę przeglądarki zawartość  ```this.films``` - otrzymalibyśmy undefined.
Dlaczego? 
Ponieważ jak już wspomniałam, konstruktor wykonuje się przed ngOnInit więc w jeszcze w konstruktorze, this.films jest puste. Ustawiamy mu wartość dopiero w ngOnInit na to, co zwróci nam serwer.
W związku z tym, nie widzimy wyników, bo ich nie ma.

Aby to zafixować, należy przenieść przypisanie 
```  this.filteredFilms = this.films;``` z konstruktora do ngOnInit.

```JavaScript
  ngOnInit() {
    this.films = this.filmsService.getFilms();
    this.filteredFilms = this.films;
  }
```

Jak pewnie zauważysz, w pliku ```films.component.ts``` edytor zaczął podkreślać nam property this.films jako że jej wartość jest niezgodna z zadeklarowanym typem (Film[]). Zauważ, że obecnie do property ```films``` przypisujemy odpowiedź z zapytania serwera, korzystając z metody getFilms() z films.service.ts, a metoda zwraca Observable typu Film[]. Ponieważ zmieniliśmy pobieranie danych na pobieranie z serwera, który zwraca Observable, nie możemy bezpośrednio przypisać wartości do property ```films```.

Możemy natomiast zasubskrybować do zwróconego Observable i kiedy wyemituje dane, ustawimy property ```films``` do zwróconej tablicy filmów.

```JavaScript

  ...
```

Czasem jednak pojawiają się błędy. Możemy dodać property ```errorMessages``` i jak pojawi się jakikolwiek błąd, do tej zmiennej zostanie przypisany komunikat błędu.

```JavaScript
  public errorMessages: string;
  ```

```JavaScript
  ngOnInit() {
    this.filmsService.getFilms().subscribe(
      films => this.films = films,
      error => this.errorMessages = error as any
    );
    this.filteredFilms = this.films;
  }
  ```

  Ok. Nie ma żadnych danych. Nie pojawia się żadna lista filmów.
  Wiesz dlaczego?

Ten kod:
```JavaScript
 this.filmsService.getFilms().subscribe(
      films => this.films = films,
      error => this.errorMessages = error as any
    );
```
wykonuje asynchroniczną operację co oznacza, że odpowiedź zostanie do użytkownika zwrócona, jak będzie gotowa.

Ten kod:
```JavaScript
 this.filteredFilms = this.films;
```
wykonuje się synchronicznie, czyli po kolei zgodnie z kolejką i może się wykonać zanim jeszcze zostaną zwrócone dane ze wcześniejszego zapytania asynchronicznego. Mamy tu właśnie taką sytuację, w której do przefiltrowanej listy filmów staramy się przypisać filmy, które jeszcze nie zostały zwrócone z backendu, dlatego też na stronie nic się nie wyświetla. Bo tablica ```filteredFilms``` po której iterujemy w template, by wyświetlić dane o filmach, jest pusta. 

Rozwiązaniem jest poczekanie, aż Observable wyemituje wartość jak subskrybujemy, to wtedy przypisujemy filmy do filmów przefiltrowanych, np:

```JavaScript
  ngOnInit() {
    this.filmsService.getFilms().subscribe(
      films => {
        this.films = films;
        this.filteredFilms = this.films;
      },
      error => this.errorMessages = error as any
    );
  }
```

## ROUTING i nawigacja

Do routingu będziemy potrzebować jeszcze kilka komponentów. 
Jakiś czas temu utworzyliśmy komponent zawierający detale dotyczące filmu. Suchy komponent, bez żadnych szczegółowych informacji. 
Pora, by go uzupełnić.

W pliku ```film-details.component.html``` usuwamy domyślnie wygenerowaną zawartość i wpisujemy dane o filmach:

Gdy chodzimy po obiektach w template, które nie zostały zdefiniowane lub mają wartość null, pojawi się błąd mówiący o tym, że próbujemy się dostać do zmiennej, która nie została zdefiniowana. Aby uniknąć pojawiania się takich komunikatów, możemy użyć tzw. "safe navigation operator", dzięki któremu, jeśli obiekt, do któregoo właściwości się próbujemy dostać nie jest zdefiniowany lub ma wartość null, po prostu nic się nie wyśweitli, zwróci null i nie rzuci błędem. Nie działa on jednak z ```[(ng-Model)]``` i 2-way data binding. Jest to też uciążliwe pisać wiele razy, jeśli w template chcemy zamieścić odwołania do wielu pól obiektu, któy nie istnieje.
Zamiast pisać wszędzie safe navigator operator można użyć *ngIf i sprawdzić czy obiekt istnieje.


Routing

Zakładamy, że mamy aplikację z nawigacją. Kliknięcie w jakiś z linków nawigacji ma nas przekierować na pożądaną stronę. Każda taka menu opcja używa wbudowanej dyrektywy routera, tzw. routerLink. Kiedy użytkownik klika na link, zostaje przekierowany pod konkretny adres przekazany w routerLinku, np:

```html
<a routerLink="/films">Filmy</a>
```

URL zmieniają się korzystając ze stylów url HTML5, nie zawierają symbolu #.  
``` http://strona.pl/films```

Angular wspiera również routing z haszami.
Kiedy adres przeglądarki się zmieni, Angular poszukuje definicji routów pasujących do ścieżki URL.

```JavaScript
{ path: 'films', component: FilmsComponent }
```

Angular Router ładuje template komponentu, który ma się uruchomić, kiedy ścieżka zostanie dopasowana.

Template ten zostanie wyrenderowany tam gdzie zadeklarujemy 

```<router-outlet></router-outlet>```

Aplikacja Angularowa ma jeden router, który jest zarządzany przez angularowy router service. Zanim takiego serwisu użyjemy, musimy go zarejestrować w providerach danych w module głównym Angulara.

```app.module.ts```

```JavaScript
import { RouterModule } from '@angular/router';

@NgModule({
  imoprts: [
    ...
    RouterModule
  ]
})
```

Razem z importem RouterModule importujemy dyrektywy routera, które mogą używać templatey:
- routerLink
- router-outlet

Zanim nawigujemy do routea, musimy mieć pewność, że te routy są dostępne dla aplikacji. Musimy dołączyć routey do RouterModule jako .forRoot()

```JavaScript
@NgModule({
  imoprts: [
    ...
    RouterModule.forRoot([])
  ]
})
```

Wołamy metodę forRoot(), do której przekazujemy tablicę z routami do naszej aplikacji.
Taką tablicę musimy sobie utworzyć.
Jeśli chcemy używać URLi z haszem 3, w .forRoot(), jako drugi argument musimy przekazać obiekt z property useHash ustawionym na true;

```JavaScript
RouterModule.forRoot([], {useHash: true})
```

Routey wymagają dwóch właściwości: path oraz component.

W AppModule deklarujemy tablicę z routeami:

```JavaScript
const routes = [
  {
    path: 'films',
    component: FilmsComponent
  },
  {
    path: 'film/:id', // 'films/:id/:year'
    component: FilmDetailsComponent
  },
  // default route
  {
    path: '',
    redirectTo: 'films', 
    pathMatch: 'full' // dopasowanie
  },
  {
    path: '**',
    component: PageNotFoundComponent;
  }
  }
];
```

Definicja 
```JavaScript
{
  path: '',
  redirectTo: 'films',
  pathMatch: 'full'
}
``` 
to definicja domyślnych routeów, tzn, gdzie użytkownik ma być przekierowany gdy route jest pusty.
ostatnia definicja jest definicja "dzikich" routeów, czyli urli do części aplikacji, które nie istnieja. Za pomoca tego można ustawić np przekierowanie do strony PAGE NOT FOUND.

Routy pozwalaja na poruszanie się w przegladarce z użyciem przycisku "Wstecz" i "Dalej", bo pamięta routing.

Trzeci zestaw z redirectTo wymaga, aby podać pathMatch. PathMatch wartość mówi routerowi jak dopasować segment ścieżki URL do ścieżki route. Potrzebujemy tego domyślnego routa tylko wtedy gdy cała część ścieżki URL po stronie klienta jest pusta więc ustawiamy pathMatch na "full".
Ostatnia definicja routea z gwiazdkami dotyczy takich URLi, które nie spełniają żadnych powyższych dopasowań i można jej doskonale użyć do obsługi strony błędu.

Kolejność definicji routeów ma znaczenie, bo wygrywa ten, który się pierwszy dopasuje. Bardziej szczegółowe routy powinny być przed tymi mniej szczegółowymi.

Wrzucam listę routeów do 
```JavaScript 
RouterModule.forRoots(routes)
```
Zanim zaczniemy używać Routeów, należy zastanowić się, jak chcemy pokazać opcje routingu użytkownikowi. Czy ma to być link, czy klikalny obrazek, czy może przycisk.

Utwórz główne menu. Dodaj menu do route głównej aplikacji.

Gdy wskazujemy komopnent, do którego chcemy nawigować po kliknięciu w menu, nie potrzebujemy więcej selectora dla tego komponnetu.



## routign - sposoby

Do URL strony mozna mieć dostęp na dwa sposoby:
- za pomoca hasz # (hasz style routing) "http://strona.pl/#/films"
- rewriting url by nie zawierały hasza "http://strona.pl/films"

Do widoku możemy się dostać na kilka sposobów: np, wpisujac adres URL bezpośrednio w pasku adresu przegladarki, albo poprzez linki.
RouterModule dostarcza kilka wbudowanych dyrektyw, w tym routerLink. Pozwala ona zdefiniować, na jaka stronę chcemy się dostać  i że Angular ma sprawdzać poprawność linków.

```html
<a routerLink="/films">Lista filmów</a>
```
a potem Kiedy adres URL w przegladarce się zmienia, Angular route szuka definicji route który pasuje do segmentu ścieżki url - w tym przypadku "films".

```JavaScript
{ 
  path: 'films',
  component: 'FilmsComponent' 
}
```

Powyższa definicja route składa się z dwóch właściwości
- path (ścieżka dopasowania)
Definiuje segment ścieżki URL dla route. Kiedy ten route jest aktywowany, ten fragment ścieżki jest doklejany do URL aplikacji. Można pisać lub zapisywać do zakładek taki link. W wielu przypadkach określamy też, jaki widok ma sie załadować pod ta ścieżka, a robimy to przez parametr ```component```

- component (ma się załadować, jeśli dopasuje w definicji ścieżkę i route zostanie aktywowany). Angular router ładuje template komponentu. Ładuje go do miejsca określonego przez ```<router-outlet></router-outlet>```


Routing bazuje na komponentach. Identyfikujemy zestaw komponentów, które chcemy dostarczyć jako cel routingu i definiujemy route dla każdego z nich.

Ok, poprawmy nasza boczna nawigacje i dodajmy kilka linków z dyrektywa [routerLink].
RouterLink jest dyrektywa atrybutu, więc dodajemy ja do takich elementów, jak ```<a>``` i umieszczamy w nawiasach kwadratowych.
Dyrektywa atrybutu zmienia wyglad lub zachowanie elementu DOM.

## DYREKTYWY 
W Angularze mamy 3 rodzaje dyrektyw:
- komponentowe - dyrektywy z templatem (czyli komponenty, którymi poslugujemy sie w template jak dyrektywamy, używajac okreslonej w dekoratorze, w polu selector: nazwie)
- strukturalne - zmieniaja layout DOM poprzez dodawanie lub usuwanie elementów (*ngIf, *ngFor, *ngSwitch)
- dyrektywy atrybutów - zmieniaja wyglad lub zachowanie elementu, komponentu lub innej dyrektywy. Używane sa jak atrybuty elementów.

Możemy tworzyć własne dyrektywy, należy je zadeklarować w Module Angularowym, w taki sam sposób, co komponenty. Dodajemy atrybut routerLink NA ELEMENTACH KLIKALNYCH, otaczamyy nawiasami kwadratowymi i bindujemy do tablicy z parametrami linku, gdzie pierwszy element to ścieżka, a pozostałe - to inne parametry route.

Przykład własnej dyrektywy:

```JavaScript
import { Directive } from '@angular/core';

@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
  constructor() { }
}
```

W pliku 
```app.component.html``` zamieńmy:
```html
 <div class="col-3 nav">
  <nav>
    <ul>
      <li><a href="#">Link 1</a></li>
      <li><a href="#">Link 2</a></li>
    </ul>
  </nav>
</div>
```
na:

```html
 <div class="col-3 nav">
  <nav>
    <ul>
      <li><a [routerLink]="['/films']">Lista filmów</a></li>
      <li><a [routerLink]="['/add']">Dodaj film</a></li>
      <li><a [routerLink]="[/search']">Wyszukiwarka na YT</a></li>
    </ul>
  </nav>
</div>
```

Możemy też użyć skrótowego zapisu, bez bindowania i użycia tablicy, jeśli nie mamy zamiaru podawać innych parametrów:
```html
<a routerLink="/films">Lista filmów</a>
```

Bindujemy (wiazemy) routerLink z template expression i zwracamy tablicę z parametrami linku.
Pierwszym elementem tablicy (tego co jest po prawej stronie [routerLink]) jest string ścieżki dla routea. Można dodać dodatkowe elementy do tablicy żeby określić opcjonalne parametry.
Router używa tej tablicy do ulokowania powiazanych routeów i utworzenia pożadanego URL bazujac na dostarczonych parametrach. Kiedy użytkownik wybierze opcję, powiazany link jest aktywowany.
Aktywowanie route komponentu wyświetla widok tego komponentu.

Zanim załadujemy główny komponent do aplikacji za pomoca routingu, wydzielmy zawartość template app.component.html do oddzielnego komponentu, a nawet kilku.

Stworzymy w ten sposób reużywalne moduły i komponenty, które będzie można użyć w różnych częściach aplikacji.

Utwórzmy komponent LayoutComponent ( w nim będziemy trzymać layout).

```JavaScript
ng g components/layout
```

a następnie usuńmy cała zawartość z pliku ```app.component.html``` i wklejmy ja do 
```layout.component.html```

```html
<div class="container-fluid">
  <div class="row my__header">
    <div class="col">
      Hello world
    </div>
  </div>
  <div class="row">
    <div class="col">
      <div class="container content">
        <div class="row">
          <!-- nawigacja boczna -->
          <div class="col-3 nav">
              <nav>
                <ul>
                    <li><a [routerLink]="['/films']">Lista filmów</a></li>
                    <li><a [routerLink]="['/add']">Dodaj film</a></li>
                    <li><a [routerLink]="['/search']">Wyszukiwarka na YT</a></li>
                </ul>
              </nav>
            </div>
            <div class="col">
              <mov-films></mov-films>
            </div>
        </div>
      </div>
    </div>    
  </div> 
  <div class="row my__footer">
    <div class="col">
    Hello world
    </div>
  </div>
</div>
```

Póki co, nic nam się nie wyświetla, dlatego że usunęliśmy cały widok z komponentu ```app.component.ts```.
Musimy wstawić komponent jako dyrektywę do template dla ```app.component.html```, żeby aplikacja otrzymała widok z komponentu.

```html
<mov-layout></mov-layout>
```

Ok, działa. Nie ma styli, więc musimy przenieść też całe style z ```app.component.scss``` do ```layout.component.scss```

```scss
.my__footer, .my__header {
    color: white;
    padding: 24px;
    margin: 0;
}

.my__header {
    background-color: darkblue;    
}

.my__footer {
    background-color: lightslategray;
}

.content {
    background-color: #fff;
    color: black;
    font-size: 14px;
}

.nav {
    background-color: lightblue;
}
```

Ale załóżmy, że nie chcemy pokazywać strony komuś, kto nie ma odpowiednich uprawnień lub chcemy mieć możliwość przekierowania pod odpowiedni URL i wygenerowanie odpowiedniego widoku komuś, kto porusza się po aplikacji nie tak, jak byśmy chcieli.
Po to nam routy. Możemy wyswietlać użytkwonikowi odpowiedni widok w zależności od tego, pod jaki adres próbuje sie dostać. Możemy też przekierowywać do innego widoku lub, zablokować dostęp do widoku, ustawiajac guardy (bramki), chroniace np. przed nieautoryzowanym wejściem.
Np. do panelu zarzadzania zalogowanego użytkownika może dostać się tylko ten użytkownik, ktory zna dane logowania.

Ok.

Obecnie w app.module.ts, gdzie zadeklarowalismy routing, zadeklarowaliśmy, by pod routerm ```films``` ładował się widok komponentu FilmsComponent.
W zwiazku z tym, nie musimy już w ```layout.component.html``` wczytywać do layoutu bezpośrednio 
```<mov-films></mov-films>```, tylko możemy użyć dyrektywy ```<router-outlet></router-outlet>```, aby wyświetlić w tym miejscu zawartość komponentu. Daje nam do jeszcze inna dodatkowa zaletę.
Przy poprzednim rozwiazaniu i wstawianiu dyrektyw komponentu do widoku, kiedy chcielibyśmy w tym samym miejscu renderować różne widoki, nie bardzo mielibyśmy jak to zrobić.
Korzystajac z ```<router-outlet>``` dajemy tylko placeholder dla wyświetlenia się komponentu.
Ponieważ do nawigacji wykorzystamy routing, możemy usunac również selector z samego komponentu FilmsComponent.

```app.module.ts```
```JavaScript
const routes = [
  {
    path: 'films',
    component: FilmsComponent
  },
  {
    path: 'film/:id', // 'film/:id/:year'
    component: FilmDetailsComponent
  },
  {
    path: '',
    redirectTo: 'films', 
    pathMatch: 'full' // dopasowanie
  },
  {
    path: '**',
    component: PageNotFoundComponent;
  }
  }
];
  ```

 ```layout.component.html``` - częśc nawigacji i placeholder do wstawienia widoku routea
 ```html
  <div class="container content">
    <div class="row">
      <!-- nawigacja boczna -->
      <div class="col-3 nav">
          <nav>
            <ul>
                <li><a [routerLink]="['/films']">Lista filmów</a></li>
                <li><a [routerLink]="['/add']">Dodaj film</a></li>
                <li><a [routerLink]="['/search']">Wyszukiwarka na YT</a></li>
            </ul>
          </nav>
        </div>
        <div class="col">
          <router-outlet></router-outlet>
        </div>
    </div>
  </div>
 ```

 W efekcie nadal widać listę filmów. 
 Dla testu, podmień komponent FilmsComponent dla path: 'films' na FilmDetailsComponent i zobaczysz template z tego właśnie komponentu.


 Ok. Już wiesz, jak działaja routy i jak napisać je samemmu.

 ## Dolaczanie parametrów do routea

 ```JavaScript
{
    path: 'films/:id', // 'films/:id/:year'
    component: FilmDetailsComponent
  },
  ...
 ```

 Do route przekazujemy parametry oddzielajac je ":/". Gdy użytkownik aktywuje dany URL z parametrem, powinien załadować się widok kompnentu FilmDetailsComponent.

 Aby dostać sie do URLa, możemy albo z paska url, albo udostępnić element HTML, który nas przeniesie (pomijamy na razie redirecty, gdzie samodzielnie manipulujemy i budujemy link, poczym przekierowujemy pod niego. Zróbmy zwykłe menu klikalne).

 Możemy użyć np opcji menu albo zwykłego linka.
 Jeśli do URLa mamy przekazać parametr, musimy ten parametr przekazać do tablicy parametrów route, jako drugi parametr:

 ```html
<a [routerLink]="['/film', film.id]">Details</a>
 ```

 // dodawanie nowego/ usuwanie

Ok, zróbmy tę zmianę pod naszym przycikiem "Details" w pliku ```films.component.ts```.
Dodajmy link i klikajac na niego, będziemy chcieli przenosić się do strony z detalami o filmie.

Jeszcze tylko małe czyszczenie. Ponieważ nie będziemy się więcej odnosić do detali filmu za pomoca dyrektywy komponentu, a będziemy go ładować po klieknięciu w link, usuńmy selector definiujacy komponent.

```film-details.component.ts``` - usuń ```selector: 'mov-film-details'``` i jego użycie z template ```films.component.html```
```html
    <mov-film-details *ngIf="detailsVisible"></mov-film-details>
```

Ok. W komponencie możemy wyświetlić informacje o filmie oraz je edytować..


## Utwórzmy formularz do edycji danych o filmie.

Będąc na stronie "Szczegóły o filmie", wyświetlmy informacje, jakie udało nam sie uzyskać.

Ok. Jak już jesteśmy na stronie widoku filmu, chcielibyśmy w jakiś sposób wyświetlić o tym filmie informacje, które mamy w bazie.
Zauważ, że dostaliśmy się na widok "Szczegółów" filmu po adresie URL, w którym przekazaliśmy id filmu.

Jedynym sposobem, żeby pobrać dane o filmie i je wyświetlić w template, jest pobranie parametru id z URLa i wtedy, pobranie informacji o filmie z bazy korzystając z tego id.

Do odczytania parametrów z aktywnego routea, potrzebujemy serwisu ActivatedRoute, dostarczonego przez '@angular/router'.
Potrzebujemy instancji tego serwisu, więc musimy za pomocą Dependecy Injection wstrzyknąć go do konstruktora kompnentu.
Następnie używamy instancji Activated Route (this.route) do pobrania parametrów. Parametry dostarczone w URLu możemy odczytać na dwa sposoby:
1. używając snapshot 'route.snapshot.paramMap' i korzystając z metody ```get()``` pobrać konkretny jeden parametr, wyświetlmy go w konsoli:

```JavaScript
import { ActivatedRoute } from '@angular/router';

constructor(private route: ActivatedRoute) { }

ngOnInit() {
   console.log(this.route.snapshot.paramMap.get('id'));
}

```

```film-details.component.ts```
```JavaScript
export class FilmDetailsComponent implements OnInit {
  private id: number;
  constructor(private route: ActivatedRoute) {
  }

  ngOnInit() {
    this.id = +this.route.snapshot.paramMap.get('id');
  }
}

```
Plus (+) przed postawiony przed liczbą w postaci tekstowej, konwertuje string na liczbę.
Ok. Możemy też utworzyć przycisk, który pozwoli nam się np. przemieścic na inną część naszej aplikacji. Często tak robimy, gdy np. użytkownik próbuje wejść w jakąś część aplikacji a nie ma do niej dostępu i zostanie przekierowany na inną stronę.

My zróbmy sobie przycisk "Powrót do filmów", który przekieruje nas z powrotem do strony z filmami.

Przycisk potrzebujemy w template ```film-details.component.html```
```html
<button (click)="onBack()">Powrót do filmów</button>
```
Następnie musimy do komponentu zaimportować instancję Routera i dostarczyć go w konstruktorze.
Pozwoli nam on użyć metody .navigate(), dzieki niej przekierujemy użytkonika na inną stronę.

```film-details.component.ts```
```JavaScript
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute, Router } from '@angular/router';

@Component({
  templateUrl: './film-details.component.html',
  styleUrls: ['./film-details.component.scss']
})
export class FilmDetailsComponent implements OnInit {
  private id: number;
  constructor(
    private route: ActivatedRoute,
    private router: Router
  ) {}

  ngOnInit() {
    this.id = +this.route.snapshot.paramMap.get('id');
  }

  onBack(): void {
    this.router.navigate(['/films']);
  }
}

```

## DODAWANIE FILMU DO BIBLIOTEKI

Ta część aplikacji ma nam służyć do dodawania nowych filmów do naszej bazy danych.
Najpierw, utwórzmy więc komponent, który nam posłuży do dodawania informacji o nowym filmie:

```JavaScript
ng g c components/films/film-add
```

Po utworzeniu komponentu, ustawiamy route dla ścieżki ['/add'], który wyświetli komponent ```FilmAddComponent```.

 ```app.module.ts```
```JavaScript
  {
    path: 'add',
    component: FilmAddComponent
  },
``` 

Ok, nasz nowy komponent z widokiem do dodawania nowych filmów, jest już połaczony i dostępny pod adresem z linkiem "/add'. Z klasy komponentu, z dekoratora @Component() możemy też usunac selector z nazwą, bo nie będziemy go używali w aplikacji, a będziemy ładować komponent w route.

Zamockujmy dane i zróbmy serwis, który wyśle request POST do serwera celem dodania nowego filmu. 

Mockujemy dane o filmie, dla jednego rekordu. 
Jak mówiłam wcześniej, HttpClient służy do komunikacji z serwerem, a działania wykonuje na Observable które sa określonego typu. Musimy więc zamockować nowy obiekt o interfejsie Films.

```films.ts``` - interfejs
```JavaScript
    id: number;
    title: string;
    year: string;
    genres: string[];
    duration: string;
    ratings: number[];
    releaseDate: string;
    averageRating: number;
    originalTitle: string;
    storyline: string;
    actors: string[];
    imdbRating: number;
    posterurl: string;
```


```film-details.component.ts```
```JavaScript
import { Component, OnInit } from '@angular/core';
import { FilmsService } from 'src/app/core/services/api/films.service';
import { Film } from './../films';

@Component({
  templateUrl: './film-details.component.html',
  styleUrls: ['./film-details.component.scss']
})
export class FilmDetailsComponent implements OnInit {
  public added: Film;
  public film: Film = {
    "id": 32,
    "title": "The Imitation Game",
    "year": "2014",
    "genres": [
        "Biography",
        "Drama",
        "Thriller"
    ],
    "ratings": [
        4,
        3,
        9,
        2,
        3,
        7,
        9,
        6,
        5,
        4,
        3,
        10,
        8,
        4,
        6,
        6,
        4,
        4,
        6,
        5,
        2,
        9,
        2,
        2,
        1,
        2,
        2,
        8,
        10,
        2
    ],
    "duration": "PT114M",
    "releaseDate": "2015-01-16",
    "averageRating": 0,
    "originalTitle": "",
    "storyline": "Based on the real life story of legendary cryptanalyst Alan Turing, the film portrays the nail-biting race against time by Turing and his brilliant team of code-breakers at Britain's top-secret Government Code and Cypher School at Bletchley Park, during the darkest days of World War II.                Written by\nStudio Canal",
    "actors": [
        "Benedict Cumberbatch",
        "Keira Knightley",
        "Matthew Goode"
    ],
    "imdbRating": 8.1,
    "posterurl": "https://images-na.ssl-images-amazon.com/images/M/MV5BNjI3NjY1Mjg3MV5BMl5BanBnXkFtZTgwMzk5MDQ3MjE@._V1_SY500_CR0,0,340,500_AL_.jpg"
};
  constructor(private filmsService: FilmsService) { }

  ngOnInit() {
  }

  addFilm(): void {
    this.filmsService.addFilm();
  }
}


```

```films-details.component.html```
```html
<h1>Szczegóły filmu</h1>
<button (click)="addFilm()">Dodaj film</button>
```

Ok. Do naszej funkcji ```addFilm()``` w jakiś cudowny sposób musimy przekazać obiekt filmu, który chcemy dodać. 

Narazie wykorzystajmy zamockowany obiekt z filmami o nazwie ```film``` i wyślijmy jego do zapisania w bazie, za pomocą requestu http, który napisaliśmy w pliku films.service.ts. Później dorobimy edytor:

```film-details.component.ts```
```JavaScript
addFilm(): void {
    this.filmsService.addFilm(this.film);
  }
```
Do wysłania żądania zapisu wykorzystamy HttpClienta i metody POST. Przy wysyłaniu żądań zapisu wiele aplikacji wymaga wysłania ekstra nagłówków. Wiele z nich wymaga np. "Content-Type", żeby jawnie zadeklarować, jakiego typu MIME jest request.
Innym przypadkiem jest przesłanie authorization tokena.
Do zadeklarowania tych opcji potrzeba użyć obiektu httpOptions, który dostarczamy do każdego HttpClient requestu, dotyczącego zapisywania danych. 
Więcej o dodawaniu nagłówków: https://angular.io/guide/http#adding-headers


Przy requestach obsługiwanych przez HttpClienta bazujemy zawsze na Observable.

```films.service.ts```

```JavaScript
import { HttpHeaders } from '@angular/common/http';

const httpOptions = {
  headers: new HttpHeaders({
    'Content-Type':  'application/json'
  })
};

 addFilm(film: Film):Observable<Film> {
    return this.http.post<Film>(this.filmsUrl, film, this.httpOptions).pipe(
      catchError(this.handleError)
    );
  }
```