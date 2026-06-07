# Wortell Browser Protect — threat-intel feed

Publieke blocklist voor de **[Wortell Browser Protect](https://github.com/wortell/browser-protect)** browser-extensie. De extensie haalt `blocklist.txt` elke ~15 minuten op en blokkeert pagina's waarvan de **hostname** op de lijst staat — een snelle manier om een bekende phishing-URL voor alle klanten te weren.

## Hoe het werkt

- De extensie fetcht:
  `https://raw.githubusercontent.com/wortell/browser-protect-feed/main/blocklist.txt`
- Matching is op **host/domein-niveau** (niet op pad). Verversen gebeurt elke ~15 minuten; bij een storing **fail-open** (de laatst opgehaalde lijst blijft gelden, de rest van de bescherming werkt door).
- De feed is bewust **publiek** (transparant; de extensie heeft geen auth).

## `blocklist.txt`-formaat

- Eén entry per regel: een bare hostname (`mfa-contoso.click`) of een volledige URL (`https://mfa-contoso.click/login`) — beide worden tot de hostname genormaliseerd.
- Regels die met `#` beginnen zijn commentaar.

## SOC-proces

- Voeg alleen **bevestigde** kwaadaardige hosts toe — een foute entry blokkeert een legitieme site voor élke client. Review vóór je commit.
- Commit naar `main` → clients pikken het binnen ~15 minuten op.

> De huidige `www.eicar.org` is een **veilige testentry** om de feed-werking te valideren; verwijder of vervang die voor productie.
