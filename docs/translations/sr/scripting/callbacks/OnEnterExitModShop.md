---
id: OnEnterExitModShop
title: OnEnterExitModShop
description: Ovaj callback se poziva kada igrac udje ili izadje iz ModShop-a.
tags: []
---

:::warning

Ovaj callback je dodana u SA-MP 0.3a i ne radi u nizim verzijama!

:::

## Opis

Ovaj callback se poziva kada igrac udje ili izadje iz ModShop-a.

| Ime        | Opis                                                                         |
| ---------- | ---------------------------------------------------------------------------- |
| playerid   | ID igraca koji je usao ili izasao iz ModShop-a.                              |
| enterexit  | 1 ako je igrac usao, ili 0 ako je izasao.                                    |
| interiorid | ID interijera od ModShop-a u koji igrac ulazi ( ili 0 ako izlazi )           |

## Vracanja

Uvek se prvi poziva u filterscript-i.

## Primeri

```c
public OnEnterExitModShop(playerid, enterexit, interiorid)
{
    if (enterexit == 0) // If enterexit is 0, this means they are exiting
    {
        SendClientMessage(playerid, COLOR_WHITE, "Nice car! You have been taxed $100.");
        GivePlayerMoney(playerid, -100);
    }
    return 1;
}
```

## Belekse

:::warning

Poznati Bug-ovi: Igraci se sudaraju kada udju u isti ModShop.

:::

## Srodne Funkcije

- [AddVehicleComponent](../functions/AddVehicleComponent.md): Dodaje dodatak na vozilo.
