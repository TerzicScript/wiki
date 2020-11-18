---
id: OnClientMessage
title: OnClientMessage
description: Ovaj callback se poziva kada god NPC vidi poruku u chatu.
tags: []
---

:::warning

Ovaj callback je dodana u SA-MP 0.3a i ne radi u nizim verzijama!

:::

## Opis

Ovaj callback se poziva kada god NPC vidi poruku u chatu. Ovo ce biti slucaj kada se SendClientMessageToAll posalje ili kada se SendClientMessage posalje NPC-u. Ovaj callback se nece pozvati kada neko nesto napise u chat-u. Za callback koji se poziva kada igrac ukuca nesto, pogledati OnPlayerText.

| Ime    | Opis                            |
| ------ | ------------------------------- |
| color  | Boja Client Poruke.             |
| text[] | Poruka                          |

## Vracanje

Ovaj callback ne vraca nikakve vrednosti.

## Primeri

```c
public OnClientMessage(color, text[])
{
    if (strfind(text,"Bank Balance: $0") != -1)
    {
        SendClientMessage(playerid, -1, "Ja sam siromasan :(");
    }
}
```

## Srodne Funkcije
