====================================
Encryption Configuration Quick Guide
====================================
 
Encryption Types
----------------

ownCloud provides two encryption types:

- **User-specific Key:** every user has their own private/public key pairs; the private key is protected by the user's password.

- **Master Key:** there is only one key (or key pair) and all files are encrypted using that key pair.
  
How To Enable Encryption
------------------------

How to enable **Master Key** encryption:

::

  occ app:enable encryption
  occ encryption:enable
  occ encryption:select-encryption-type masterkey
  occ encryption:encrypt-all

How to enable **User-specific Key** encryption:

::

  occ app:enable encryption
  occ encryption:enable
  occ encryption:select-encryption-type user-keys
  occ encryption:encrypt-all 


After User-specific encryption is enabled, users must log out and log back in to trigger the automatic personal encryption key genaration process. 

How To Enable Users File **Recovery Keys**
------------------------------------------

Go to the "Encryption" section of your Admin page and set a recovery key password. You then need to ask the users to opt-in to the Recovery Key. If a user decides not to opt-in to the recovery key and forgets about his password, all of the users data can not be decrypted anymore.

They need to:

- go to the "**Personal**" page 
- enable the recovery key
 
View Current Encryption **Status**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Get the current encryption status and the loaded encryption module::

 occ encryption:status 

**Decrypt** Files For All Users
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
How to decrypt **Master Key** encryption::

 occ maintenance:singleuser --on
 occ encryption:decrypt-all
 occ maintenance:singleuser --off

How to decrypt **User-specific Key** encryption::

 occ maintenance:singleuser --on
 occ encryption:decrypt-all
 #enter **Recovery Key** for **each user**
 occ maintenance:singleuser --off

Disabling Encryption
--------------------

When you have decrypted all the files, encryption will be turned off.
