---
id: OnFilterScriptExit
title: OnFilterScriptExit
description: Ovaj callback se poziva kada se filterscript-a iskljuci.
tags: []
---

## Opis

Ovaj callback se poziva kada se filterscript-a iskljuci. Samo se poziva u filterscript-i koja se iskljucuje.

## Primeri

```c
public OnFilterScriptExit()
{
    print("\n--------------------------------------");
    print(" My filterscript unloaded");
    print("--------------------------------------\n");
    return 1;
}
```

## Srodne Funkcije
