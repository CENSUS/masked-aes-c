# Masked AES
This project is a masking implementation for AES in the C programming language, supporting CBC/CTR/ECB modes and 128/192/256-bit size keys 
based on Tiny-AES (3).

This is proof-of-concept code that is intended for use in glitching attacks
that aim to overcome proactive side-channel defenses. This was developed 
as part of the MELITY project (ΜΕΛΙΤΥ, Κωδικός Έργου: Τ1ΕΔΚ-01958, Δράση 
“Ερευνώ – Δημιουργώ – Καινοτομώ” του Επιχειρησιακού Προγράμματος ΕΠΑνΕΚ
2014-2020 “Ανταγωνιστικότητα – Επιχειρηματικότητα – Καινοτομία”).

![MELITY LOGO](doc/images/melity-logo-with-text.png?raw=true "MELITY Logo")
![EPANEK_LOGO](doc/images/epanek-logo.png?raw=true "EPANEK logo")


This is licensed as work in the public domain, for more details 
see unlicense.txt

## How to use 
Clone the repository and compile it using the following command:

```
make MASKED=1
```

This implementation is verified against the data in:

National Institute of Standards and Technology Special Publication 800-38A 2001 ED Appendix F: Example Vectors for Modes of Operation of the AES.

## Masking implementation
This is an implementation of the boolean masking tecnique described in _Stefan Mangard, Elisabeth Oswald, Thomas Popp - Power Analysis Attacks Revealing the Secrets of Smart Cards (Advances in Information Security) (2007)_ (2)

In our code we are using 10 masks:
* M', M are the input and the ouput masks for the masked _SubBytes_ operation
* M1, M2, M3, M4 are the input mask for the MixColumns operation
* M1', M2', M3', M4' are computed from M1,M2,M3,M4 and represent the output mask for the MixColumns operation.

All the revelant code can be found in the following functions (_aes.c_):

```C
static void CipherMasked(state_t *state, const uint8_t *RoundKey);
static void InvCipherMasked(state_t *state, const uint8_t *RoundKey);
```

### Encryption
![Encryption](doc/images/Encryption.png?raw=true "Masking implementation for encryption")
### Decryption
![Encryption](doc/images/Decryption.png?raw=true "Masking implementation for decryption")

## References
* Stefan Mangard, Elisabeth Oswald, Thomas Popp - Power Analysis Attacks Revealing the Secrets of Smart Cards (Advances in Information Security) (2007)
* Fault-assisted side-channel analysis of masked implementations. In 2018 IEEE International Symposium on Hardware Oriented Security and Trust (HOST), pp. 57-64. IEEE, 2018.
* https://github.com/kokke/tiny-AES-c
* https://github.com/ermin-sakic/smartcard-aes-fw
