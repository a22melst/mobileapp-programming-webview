
# Rapport

Det första jag gjorde var att ändra appens namn, vilket görs i filen "res/values/strings.xml"
I brist på annat fick den heta "MelkersApp".

XML Kod för att byta namn på appen:
```
<string name="app_name">MelkersApp</string>
```

Efter det var det dags att möjliggöra internetanslutning i appen, då detta krävs för att visa
den externa webbsidan. För att göra detta gick jag in i filen "manifests/AndroidManifest.xml"
och lade till följande XML kod.
```
<uses-permission android:name="android.permission.INTERNET" />
```
Sedan var det dags att skapa min WebView, vilket man kan göra i filen "java/MainActivity.java".
Koden i den här filen skrivs i Java, och blev som följer.

```
// Inuti klassen
private WebView myWebView;

// Inuti onCreate()
myWebView = findViewById(R.id.my_webview);
myWebView.setWebViewClient(new WebViewClient());
myWebView.getSettings().setJavaScriptEnabled(true);
```
Först skapas ett privat objekt kallat myWebView av klassen WebView. Inuti metoden "onCreate()" 
instansierar jag objektet med hjälp av metoden findViewById() och fäster en ny WebClient på 
den. För att sidorna ska kunna visas måste även exekevering av JavaScript fungera. Detta möjliggörs genom
inställningen setJavaScriptEnabled(true) som åkallas via getSettings().

När man kommer in på appen finns det en meny med två alternativ, "External Web Page" och "Internal Web Page".
För att dessa alternativ ska vara väljbara fick jag ändra i metoden onOptionItemSelected() inuti MainActivity.
Där finns två if satser med kod som körs om respektive alternativ trycks. Under dessa if satser kallar jag
på metoderna showExternalWebPage() och showInternalWebPage(). 

```
    public boolean onOptionsItemSelected(MenuItem item) {
        // Handle action bar item clicks here. The action bar will
        // automatically handle clicks on the Home/Up button, so long
        // as you specify a parent activity in AndroidManifest.xml.
        int id = item.getItemId();

        //noinspection SimplifiableIfStatement
        if (id == R.id.action_external_web) {
            Log.d("==>","Will display external web page");
            showExternalWebPage();
            return true;
        }

        if (id == R.id.action_internal_web) {
            Log.d("==>","Will display internal web page");
            showInternalWebPage();
            return true;
        }

        return super.onOptionsItemSelected(item);
    }
```
För att något ska hända när man trycker måste man även implementera metoderna. Inuti respektive metod
använder jag metoden loadUrl(), som tar länken till hemsidan som argument. För den interna webbsidan skrev jag in
html-filens sökväg.

```
    public void showExternalWebPage(){
        myWebView.loadUrl("https://his.se");
    }

    public void showInternalWebPage(){
        myWebView.loadUrl("file:///android_asset/internalwebpage.html");
    }
```

(Fick det inte att fungera med att skriva ![](bildnamn.png) så jag la in bilderna direkt på github)

Min interna webbsida gör jag i notepad och lägger till lite simpel text.

![](InternalWebpage.png)![InternalWebpage](https://user-images.githubusercontent.com/129266288/231229567-b834817b-5f22-4340-aec2-769057a6e089.png)

För den externa webbsidan valde jag his.se.

![ExternalWebpage](https://user-images.githubusercontent.com/129266288/231229517-8b188f96-a1cd-4d03-803a-ff91132fe4bb.png)
