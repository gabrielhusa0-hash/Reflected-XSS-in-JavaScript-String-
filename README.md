# Lab: Reflected XSS into a JavaScript string with angle brackets and double quotes HTML-encoded and single quotes escaped

Úspěšně vyřešená laboratoř zaměřená na Reflected XSS v rámci PortSwigger Web Security Academy.

## 📋 Popis zranitelnosti
Tato laboratoř obsahuje zranitelnost typu Reflected XSS uvnitř JavaScriptového řetězce. Aplikace ošetřuje speciální znaky (ostré závorky a dvojité uvozovky jsou HTML kódované, jednoduché uvozovky jsou escapované), což vyžaduje specifickou konstrukci payloadu pro únik z kontextu.

## 🛠️ Postup řešení (Walkthrough)

1. **Testovací vstup:**
   - Do vyhledávacího pole na stránce jsem zadal náhodný testovací řetězec (např. `abcd12345`).
2. **Zachycení provozu:**
   - Zapnul jsem intercept v proxy nástroji, odeslal požadavek a poslal ho do **Repeateru** k podrobnější analýze.
3. **Analýza odpovědi:**
   - V odpovědi (response) jsem dohledal, kde se můj zadaný text vkládá přímo do JavaScriptového kódu na stránce.
4. **Vytvoření payloadu a exploatace:**
   - Na základě kontextu jsem sestavil payload, který dokázal uzavřít řetězec a spustit JavaScript:
     ```text
     \'-alert(1)//
     ```
   - Po odeslání tohoto payloadu do vyhledávání se kód vykonal a laboratoř byla úspěšně vyřešena.

##  Technické vysvětlení 

Zpětné lomítko (\): Filtr ho zachytí a escapuje dalším lomítkem -> vznikne \\.

Jednoduchá uvozovka ('): Filtr ji zachytí a escapuje lomítkem -> vznikne \'.

Výsledný kód vyrenderovaný v HTML/JS pak vypadá takto:
var searchTerms = '\\'-alert(1)//';