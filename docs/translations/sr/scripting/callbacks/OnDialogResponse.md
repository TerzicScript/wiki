---
id: OnDialogResponse
title: OnDialogResponse
description: Ovaj callback se poziva kada igrac odgovori na dialog prikazan pomocu ShowPlayerDialog klikom na dugme, pritiskom na ENTER/ESC ili klikne na neki od stvari sa liste ( ako se koristi tip dialoga koji je lista ).
tags: []
---

:::warning

Ovaj callback je dodana u SA-MP 0.3a i ne radi u nizim verzijama!

:::

## Opis

Ovaj callback se poziva kada igrac odgovori na dialog prikazan pomocu ShowPlayerDialog klikom na dugme, pritiskom na ENTER/ESC ili klikne na neki od stvari sa liste ( ako se koristi tip dialoga koji je lista ).

| Ime         | Opis                                                                                                                    |
| ----------- | ----------------------------------------------------------------------------------------------------------------------- |
| playerid    | ID igraca koji je odgovorio na dialog.                                                                                  |
| dialogid    | ID dialoga na koji je igrac odgovorio, dodeljen u ShowPlayerDialog.                                                     |
| response    | 1 za levo dugme i 0 za desno dugme ( ako je prikazano samo jedno, onda vraca 1 uvek )                                   |
| listitem    | ID stvari sa liste koju je igrac izabrao ( pocinje od 0 ) ( samo ako se koristi tip dialoga koji je lista, inace -1 ).  |
| inputtext[] | Tekst koji je igrac uneo u dialog.                                                                                      |

## Vracanje

Uvek se poziva prva u filterscript-ama tako da vracanjem vrednosti 1 blokira ostale filtlerscript-e da je vide.

## Primeri

```c
// Define the dialog ID so we can handle responses
#define DIALOG_RULES 1

// In some command
ShowPlayerDialog(playerid, DIALOG_RULES, DIALOG_STYLE_MSGBOX, "Server Rules", "- No Cheating\n- No Spamming\n- Respect Admins\n\nDo you agree to these rules?", "Yes", "No");

public OnDialogResponse(playerid, dialogid, response, listitem, inputtext[])
{
    if (dialogid == DIALOG_RULES)
    {
        if (response) // If they clicked 'Yes' or pressed enter
        {
            SendClientMessage(playerid, COLOR_GREEN, "Thank you for agreeing to the server rules!");
        }
        else // Pressed ESC or clicked cancel
        {
            Kick(playerid);
        }
        return 1; // We handled a dialog, so return 1. Just like OnPlayerCommandText.
    }

    return 0; // You MUST return 0 here! Just like OnPlayerCommandText.
}
#define DIALOG_LOGIN 2

// In some command
ShowPlayerDialog(playerid, DIALOG_LOGIN, DIALOG_STYLE_INPUT, "Login", "Please enter your password:", "Login", "Cancel");

public OnDialogResponse(playerid, dialogid, response, listitem, inputtext[])
{
    if (dialogid == DIALOG_LOGIN)
    {
        if (!response) // If they clicked 'Cancel' or pressed esc
        {
            Kick(playerid);
        }
        else // Pressed ENTER or clicked 'Login' button
        {
            if (CheckPassword(playerid, inputtext))
            {
                SendClientMessage(playerid, COLOR_RED, "You are now logged in!");
            }
            else
            {
                SendClientMessage(playerid, COLOR_RED, "LOGIN FAILED.");

                // Re-show the login dialog
                ShowPlayerDialog(playerid, DIALOG_LOGIN, DIALOG_STYLE_INPUT, "Login", "Please enter your password:", "Login", "Cancel");
            }
        }
        return 1; // We handled a dialog, so return 1. Just like OnPlayerCommandText.
    }

    return 0; // You MUST return 0 here! Just like OnPlayerCommandText.
}
#define DIALOG_WEAPONS 3

// In some command
ShowPlayerDialog(playerid, DIALOG_WEAPONS, DIALOG_STYLE_LIST, "Weapons", "Desert Eagle\nAK-47\nCombat Shotgun", "Select", "Close");

public OnDialogResponse(playerid, dialogid, response, listitem, inputtext[])
{
    if (dialogid == DIALOG_WEAPONS)
    {
        if (response) // If they clicked 'Select' or double-clicked a weapon
        {
            // Give them the weapon
            switch(listitem)
            {
                case 0: GivePlayerWeapon(playerid, WEAPON_DEAGLE, 14); // Give them a desert eagle
                case 1: GivePlayerWeapon(playerid, WEAPON_AK47, 120); // Give them an AK-47
                case 2: GivePlayerWeapon(playerid, WEAPON_SHOTGSPA, 28); // Give them a Combat Shotgun
            }
        }
        return 1; // We handled a dialog, so return 1. Just like OnPlayerCommandText.
    }

    return 0; // You MUST return 0 here! Just like OnPlayerCommandText.
}
#define DIALOG_WEAPONS 3

// In some command
ShowPlayerDialog(playerid, DIALOG_WEAPONS, DIALOG_STYLE_LIST, "Weapons",
"Weapon\tAmmo\tPrice\n\
M4\t120\t500\n\
MP5\t90\t350\n\
AK-47\t120\t400",
"Select", "Close");

public OnDialogResponse(playerid, dialogid, response, listitem, inputtext[])
{
    if (dialogid == DIALOG_WEAPONS)
    {
        if (response) // If they clicked 'Select' or double-clicked a weapon
        {
            // Give them the weapon
            switch(listitem)
            {
                case 0: GivePlayerWeapon(playerid, WEAPON_M4, 120); // Give them an M4
                case 1: GivePlayerWeapon(playerid, WEAPON_MP5, 90); // Give them an MP5
                case 2: GivePlayerWeapon(playerid, WEAPON_AK47, 120); // Give them an AK-47
            }
        }
        return 1; // We handled a dialog, so return 1. Just like OnPlayerCommandText.
    }

    return 0; // You MUST return 0 here! Just like OnPlayerCommandText.
}
```

## Belekse

:::tip

Parametri mogu da sadrze drugacije vrednosti, u zavisnosti od stila dialog-a ([klikni za vise primera](../resources/dialogstyles.md)).

:::

:::tip

Pozeljno je da se koristi switch kroz dialog-e, ako ih imate previse.

:::

:::warning

Igracev dialog se ne sakriva kada se mod restartuje, tako da ce u tom slucaju server ispisati "Warning: PlayerDialogResponse PlayerId: 0 dialog ID doesn't match last sent dialog ID" ako igrac odgovori na dialog nakon restarta.

:::

## Srodne Funkcije

- [ShowPlayerDialog](../functions/ShowPlayerDialog.md): Prikaze dialog igracu.
