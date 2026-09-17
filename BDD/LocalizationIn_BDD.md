## Localization with Gherkin

Gherkin supports writing feature files in multiple natural languages, allowing teams to create BDD specifications in their native language.

### Step 1. Specify the Language

**Add a language header at the top of the .feature file**  

The # language: directive must be the first line of the feature file.

```text
# language: fr
Fonctionnalité: Connexion utilisateur
  Scénario: Connexion réussie
    Étant donné que l'utilisateur est sur la page de connexion
    Quand il saisit des informations valides
    Alors il doit être connecté
```


**Example: German Feature File**

```text
# language: de

Funktionalität: Benutzeranmeldung

  Szenario: Erfolgreiche Anmeldung

    Angenommen der Benutzer befindet sich auf der Login-Seite
    Wenn er gültige Anmeldedaten eingibt
    Dann sollte er angemeldet werden
```



### Step 2: Step Definitions Remain the Same

Even if feature files are written in another language, Java step definitions work normally.

```text
@Cuando("introduce credenciales válidas")
public void enterValidCredentials() {
    loginPage.login("user", "password");
}

@Alors("il doit être connecté")
public void userShouldBeLoggedIn() {
    Assert.assertTrue(homePage.isDisplayed());
}
```


### Supported Languages

Gherkin supports 70+ languages including:

```text
Language	Code
English	en
French	fr
German	de
Spanish	es
Italian	it
Portuguese	pt
Dutch	nl
Russian	ru
Chinese	zh-CN
Japanese	ja
Korean	ko
Hindi	hi
Arabic	ar
```

### Recommended Approach 

```text
@Given("user is on login page")
@Given("utilisateur est sur la page de connexion")
@Given("el usuario está en la página de inicio de sesión")
@Given("उपयोगकर्ता लॉगिन पृष्ठ पर है")
public void userIsOnLoginPage() {
    loginPage.open();
}
```


---

