

Eesmärk: kasutaja allkirjastab ja saadab akti; hiljem jõuab mõlemapoolselt allkirjastatud fail automaatselt akti alla.

## Kasutajavoog

1. Salvesta akt
2. Lae akt alla
3. Allkirjasta akt
4. Lae allkirjastatud akt üles
5. Saada akt teisele osapoo
>>>>
6. Vastus jõuab tagasi
7. Mõlemapoolselt allkirjastatud fail lisandub automaatselt akti alla
8. Soovi korral saada raamatupidamisele

## Taskid

### Task 1 — MVP: “Ava Outlook ja eeltäida kiri”
- Pärast üleslaadimist ava “Saada” dialoog (saaja, koopia endale, teema/tekst).
- Nupp “Ava e-maili klient (mailto)” + “Kopeeri tekst”.
- Märkus: manus lisatakse käsitsi.
- Done: e-kiri eeltäidetud, teemas dok/akti ID.

### Task 2 — Automaatsaatmine backendist
- Backend saadab e-kirja (SMTP/MS Graph vms) + manused (allkirjastatud akt, arve kui olemas).
- Salvesta meta (aeg, adressaadid, messageId).
- Done: UI näitab saatmist; vead käsitletud, saab retry.

### Task 3 — Allkirjastamine brauseris
- FE: “Allkirjasta brauseris” (ID-kaart/Mobiil-ID/Smart-ID), olek + retry.
- BE: eID integratsioon + API (start/status/finish), fail salvestub agregatsiooni alla.
- Done: “Allkirjastatud” olek + fail allalaetav; idempotentsus.

### Task 4 — Inbound/agent: vastuste sidumine
- Kuula inbound e-maile (IMAP/MS Graph webhook), seo thread/messageId või teema tokeniga.
- Salvesta manus “mõlemapoolselt allkirjastatud” failina, idempotentsus; vead → manual review.
- Done: õige akti all on uus fail ja auditjälg.

## Avatud küsimused
- Teenus + võtmed (dev/stage/prod)?
- Väljund (BDOC/ASiC-E vs PDF)?
- Mitu allkirjastajat?
- Auditlogi nõuded?
- Failiversioonid: hoia versioon, vana UI-s ei kuvata.
