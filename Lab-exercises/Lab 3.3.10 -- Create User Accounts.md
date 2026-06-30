# Lab 3.3.10 -- Create User Accounts

> **Course:** Cisco CyberOps Associate
> **Module:** 3 — Windows Operating System
> **Platform:** Windows 10
> **Lab Type:** Hands-On
> **Completed:** June 2026
> **Author:** Christos Panopoulos — University of Peloponnese, CS & Telecommunications

---

## Overview

The lab demonstrated the security measures an operating system implements even to a simple task such as
user account creation to reduce the attack surface by using the principle of least privilege. By using the 
GUI of Windows, an account can be created in the Standard group, which later can be modified through the command
prompt.

---

## Background

Implementing security measures to protect as many access points for an attacker as possible is a fundamental requirement for operating systems.
This is why Windows OS applies NTFS permissions. Creating a new Windows account on a system is set to have restricted access by default
over the system, implementing the principle of least privilege, which limits each account to only accessing what is needed.

---

## Environment & Tools

| Component       | Details |
|-----------------|---------|
| Operating System | Windows 10 Home |
| Primary Tool(s) | Control Panel, Command Prompt |
| Key Concepts    | NTFS permissions, least privilege |

---

## Procedure Summary

### Part 1

To examine how Windows enforces NTFS permissions on accounts, a new local account User1 was created alongside the
Administrator account already existing on the system. Windows by default sets the User1 account type to a Standard account, 
logging in to the account demonstrates that every account with Administrator privileges has full control of the User1 folder.
SYSTEM, Administrator and the "christos christos" account, my personal Administrator account, all have full permissions
over the User1 folder. In contrast, the User1 account cannot access the admin account's user files.

![Account Creation](../Lab-screenshots/User%20Creation%20Windows/local%20account%20creation.jpg)
![Security Tab](../Lab-screenshots/User%20Creation%20Windows/User1%20permissions.png)
![Access denied Tab](../Lab-screenshots/User%20Creation%20Windows/accessing%20admin%20account.png)


### Part 2

Locating group information for the User1 account and "christos christos" account could not be done using the GUI tool, 
as Local Users and Groups is not available on Windows 10 Home. The group information needed was retrieved from the command prompt by 
executing the `net user User1` command and `net user Χρηστος` command for the admin account information. The output of those 
commands shows User1 being a part of the Users group and Χρηστος being part of the Administrators and Performance Log Users groups.

![net user User1 Tab](../Lab-screenshots/User%20Creation%20Windows/net%20user%20user1.jpg)
![net user Christos Tab](../Lab-screenshots/User%20Creation%20Windows/christos%20christos%20command%20prompt.jpg)

### Part 3

Initially, trying to add User1 to the Administrators group was met with an access denied, as the command prompt was not run as an Administrator.
Changing User1 to the Administrators group through the command prompt was done with `net localgroup Administrators User1 /add`, after verifying 
the changes with `net user User1`, where the User1 account was added to the Administrators group, it was later removed with `net localgroup Administrators User1 /delete` command.
The User1 account is subsequently deleted with `net user User1 /delete`.

![add user1 admin Tab](../Lab-screenshots/User%20Creation%20Windows/Add%20User1%20as%20admin.jpg)
![Security Tab](../Lab-screenshots/User%20Creation%20Windows/delete%20user1%20admin.jpg)
![Security Tab](../Lab-screenshots/User%20Creation%20Windows/delete%20User1%20from%20system.jpg)

---

## Key Findings

The Windows operating system sets any new accounts to a Standard account by default, not giving away any unnecessary access. Modifying User1's group membership 
through the Command Prompt confirmed that account privileges in Windows are not fixed at creation, with User1 successfully elevated to the Administrators group 
and later returned to Standard privileges before deletion. The new account User1 has full access over its local system to perform any work necessary,
but cannot access important files like the Administrator's user folder due to the NTFS permissions Windows forces. Even logged in as an 
administrator account, many actions cannot be performed in the command prompt without running it as administrator.

---

## References

- Cisco NetAcad — CyberOps Associate, Lab 3.3.10: Create User Accounts
