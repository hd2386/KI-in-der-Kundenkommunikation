# 🎯Aufgabenstellung
Gestaltet einen Prompt, der aus dem gegebenen Kontext eine Push-Nachricht und einen In-App-Banner erzeugt – respektvoll, klar und ohne künstliche Dringlichkeit.

## Kontext (fürs LLM)
> Lieblingskopfhörer sind wieder verfügbar. Begrenzte Menge, aber keine zeitliche Begrenzung. Kostenloser Versand ab 59 €. Warenkorb von letzter Sitzung ist gespeichert.

## Anforderungen

### Ausgabespezifikation

| **Element**        | **Limit**           | **Regeln**                              |
|--------------------|--------------------|-----------------------------------------|
| Push-Nachricht     | max. 50 Zeichen    | Keine Ausrufe, kein "Jetzt!"            |
| Banner-Headline    | max. 6 Wörter      | Klar und ruhig                          |
| Banner-Body        | max. 18 Wörter     | Informativ, nicht drängend              |
| CTA-Button         | max. 2 Wörter      | Handlungsauffordernd, aber neutral      |

### Tonalität
- ✅ Freundlich, informativ, du-Form
- ✅ Hilfsbereit und respektvoll
- ❌ Keine künstliche Verknappung ("nur heute", "letzte Chance")
- ❌ Keine Superlative ("beste", "einmalig")
- ❌ Keine Dringlichkeits-Trigger ("schnell", "sofort")

## Lösung
### Prompt Version 1 (Vorversion)
```
Erstelle aus folgendem Kontext eine Push-Nachricht und einen Banner:

Kontext: Lieblingskopfhörer sind wieder verfügbar. Begrenzte Menge, 
aber keine zeitliche Begrenzung. Kostenloser Versand ab 59 €. 
Warenkorb von letzter Sitzung ist gespeichert.

Push: maximal 50 Zeichen
Banner-Headline: maximal 6 Wörter
Banner-Body: maximal 18 Wörter
CTA: maximal 2 Wörter

Ton: freundlich und informativ
```
> Problem mit dieser Version: Zu vage, keine klaren Negativinstruktionen, Ton nicht präzise definiert! 

### Prompt Version 2 (Final) - Variante A

```
Du bist UX-Copywriter für eine E-Commerce-App. Erstelle aus 
folgendem Kontext Benachrichtigungstexte:

KONTEXT:
Lieblingskopfhörer sind wieder verfügbar. Begrenzte Menge, aber 
keine zeitliche Begrenzung. Kostenloser Versand ab 59 €. Warenkorb 
von letzter Sitzung ist gespeichert.

AUSGABEFORMAT:

Push-Nachricht:
- Exakt maximal 50 Zeichen (inkl. Leerzeichen)
- Du-Form verwenden
- Keine Ausrufezeichen
- Kein "Jetzt!"

Banner-Headline:
- Maximal 6 Wörter
- Klar und ruhig

Banner-Body:
- Maximal 18 Wörter
- Informativ, nicht drängend

CTA-Button:
- Maximal 2 Wörter
- Handlungsauffordernd, aber neutral

TONALITÄT:
Freundlich, hilfsbereit, respektvoll. Informiere statt zu drängen.

VERBOTEN:
- Künstliche Verknappung ("nur heute", "letzte Chance")
- Superlative ("beste", "einmalig")
- Dringlichkeits-Trigger ("schnell", "sofort", "beeil dich")
- Mehrere Ausrufezeichen

Gib die Texte strukturiert aus mit Zeichenzählung.
```
### Prompt Version 2 (Final) - Variante B für Tech-Fan
```
Du bist UX-Copywriter für eine E-Commerce-App. Erstelle aus 
folgendem Kontext Benachrichtigungstexte:

KONTEXT:
Lieblingskopfhörer sind wieder verfügbar. Begrenzte Menge, aber 
keine zeitliche Begrenzung. Kostenloser Versand ab 59 €. Warenkorb 
von letzter Sitzung ist gespeichert.

PERSONA: Tech-Enthusiast
- Zeige etwas mehr Begeisterung für das Produkt
- Bleibe dennoch respektvoll und ohne Druck
- Nutze leicht emotionalere Sprache ("endlich", "dein Favorit")
- Aber: keine Übertreibungen, keine falschen Versprechungen

AUSGABEFORMAT:

Push-Nachricht:
- Exakt maximal 50 Zeichen (inkl. Leerzeichen)
- Du-Form verwenden
- Keine Ausrufezeichen
- Kein "Jetzt!"

Banner-Headline:
- Maximal 6 Wörter
- Klar und ruhig

Banner-Body:
- Maximal 18 Wörter
- Informativ, nicht drängend

CTA-Button:
- Maximal 2 Wörter
- Handlungsauffordernd, aber neutral

TONALITÄT:
Freundlich, hilfsbereit, respektvoll. Informiere statt zu drängen.
Zeige Begeisterung für Tech, aber ohne Verkaufsdruck.

VERBOTEN:
- Künstliche Verknappung ("nur heute", "letzte Chance")
- Superlative ("beste", "einmalig")
- Dringlichkeits-Trigger ("schnell", "sofort", "beeil dich")
- Mehrere Ausrufezeichen

Gib die Texte strukturiert aus mit Zeichenzählung.
```
## 📤 Beispiel-Outputs
### Vorversion
*Push-Nachricht (42 Zeichen):*
```
🎧 Deine Lieblingskopfhörer sind wieder da!
```
*Banner:*
```
Headline: Lieblingskopfhörer jetzt wieder verfügbar

Body: Begrenzte Stückzahl! Dein Warenkorb ist gespeichert. Kostenloser Versand ab 59 €.

CTA: Jetzt shoppen
```
---

### Variante A (Neutral, informativ)
*Push-Nachricht (47 Zeichen):*
```
Deine Kopfhörer sind wieder verfügbar
```
*Banner:*
```
Headline: Kopfhörer wieder da

Body: Dein Modell ist zurück. Dein Warenkorb wartet. Ab 59€ versandkostenfrei.

CTA: Ansehen
```
---
### Variante B (Tech-Fan, etwas emotionaler)
*Push-Nachricht (49 Zeichen):*
```
Deine Kopfhörer sind endlich wieder da
```
*Banner:*
```
Headline: Dein Favorit ist zurück

Body: Das Modell aus deinem Warenkorb ist verfügbar. Sichere dir deins mit kostenlosem Versand.

CTA: Zum Produkt
```
## Erkenntnisse
### Was hat den größten Unterschied gemacht?
- **Vorher**: LLM nutzte "Jetzt shoppen" oder "Begrenzte Stückzahl"
- **Nachher**: Durch explizite Verbote (keine Ausrufezeichen, kein "Jetzt!") wurde der Ton sofort ruhiger
- **Persona-Effekt**: "Tech-Enthusiast" führte zu "endlich" und "dein Favorit" – mehr Emotion, aber immer noch respektvoll

## Diskussionsfragen

### 1. Welche konkreten Prompt-Zusätze haben den Ton sofort verändert?

- Die VERBOTEN-Sektion (Negativinstruktionen)
- "Informiere statt zu drängen" als Leitprinzip
- Explizite Zeichenzählung erzwang Prägnanz

### 2. Wo lag der Aha-Effekt: Ausgabespezifikation oder Negativinstruktionen?
- Ausgabespezifikation: Exakte Zeichenlimits zwangen zur Klarheit
- Negativinstruktionen: Verhinderten typische Marketing-Floskeln automatisch
- Beides zusammen war entscheidend

### 3. Wie balanciert ihr Information und Motivation ohne Druck?
- "Dein Warenkorb wartet" → sanfte Erinnerung statt Druck
- Versandkosten-Info gibt praktischen Mehrwert
- CTA bleibt neutral ("Ansehen" statt "Jetzt shoppen!")
- Fokus auf Verfügbarkeit, nicht auf Knappheit

## 🚀 Erfolgskriterien (erfüllt)
- Strukturtreue und Wortlimits eingehalten
- Klarheit und Lesbarkeit (keine Jargons, keine Dringlichkeits-Trigger)
- Ton passt zur definierten Persona
- A/B zeigt erkennbaren, aber professionellen Tonunterschied



