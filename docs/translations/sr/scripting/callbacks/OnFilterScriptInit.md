---
id: OnFilterScriptInit
title: OnFilterScriptInit
description: Ovaj callback se poziva kada se filterscript-a ucita.
tags: []
---

## Opis

Ovaj callback se poziva kada se filterscript-a ucita. Poziva se samo u filterscript-i koja se pokrece.

## Primeri

```c
public OnFilterScriptInit()
{
    print("\n--------------------------------------");
    print("The filterscript is loaded.");
    print("--------------------------------------\n");
    return 1;
}
```

## Srodne Funkcije
