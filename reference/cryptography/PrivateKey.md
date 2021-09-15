> class `PrivateKey` implements [`Key`](reference/cryptography/Key.md)

A private key on the Hedera™ network.

> [!TIP]
>  Use "" for an empty passphrase

<!-- tabs:start -->

#### ** Java **

```java
var key = PrivateKey.generate();
var key = PrivateKey.fromBytes(bytes);
var key = PrivateKey.fromString("key");
var key = PrivateKey.fromPem(pemString, passphrase);

var key = PrivateKey.fromMnemonic("word word2 word3", passphrase);
```

#### ** JavaScript **

```javascript
const key = PrivateKey.generate()
const key = PrivateKey.fromBytes(bytes);
const key = PrivateKey.fromString("key")
const key = await PrivateKey.fromPem(pemString, passphrase)
const key = await PrivateKey.fromKeystore(keystoreBytes, passphrase)

const mnemonic = await Mnemonic.fromString("word1 word2 word3...");
const key = PrivateKey.fromMnemonic(mnemonic, passphrase)
```

#### ** Go **

```go
newKey, err := GeneratePrivateKey()
newKey, err := PrivateKeyFromBytes(bytes)
newKey, err := PrivateKeyFromString("key")
newKey, err := PrivateKeyFromKeystore(bytes, passphrase)
newKey, err := PrivateKeyFromPem(bytes, passphrase)
if err != nil {
    println(err.Error())
}

// use "" for an empty passphrase
mnemonic, err := hedera.MnemonicFromString("word1 word2 word3...");
if err != nil {
    println(err.Error())
}

key, err := mnemonic.ToPrivateKey(passphrase)
if err != nil {
    println(err.Error())
}
```

<!-- tabs:end -->

### Static Methods

##### `generate` ( ): `PrivateKey`

Generates a new Ed25519 private key.

---

##### `fromBytes` ( `data`: `bytes` ): `PrivateKey`

Parses a private key from bytes.

---

##### `fromString` ( `text`: `String` ): `PrivateKey`

Recovers an PrivateKey from its text-encoded representation.

---

##### `fromPem` ( `pem`: `String` ): `PrivateKey`

Parse a private key from a PEM encoded string.

---

##### `fromKeystore` ( `data`: `bytes`, `passphrase`: `String` ): `PrivateKey`

Recovers an PrivateKey from an encrypted keystore encoded as a byte slice.

---

##### `fromMnemonic` ( `mnemonic`: `String`, `passphrase`: `String` ): `PrivateKey`

Recovers an ed25519 private key from a 24, 22, or 12 word mnemonic. 24 and
12 word mnemonics use a BIP-32 word list and SLIP-10 deriviation. 22 word
mnemonics use a legacy word list from the original Hedera mobile wallets.

###### Errors

- [`BadMnemonic`](reference/error/BadMnemonic.md) — when the mnemonic contains
  words not found in the word list; there is a checksum mismatch; or, an
  unexpected number of words.

### Methods

##### `isDerivable` ( ): `boolean`

Check if this private key supports derivation.

---

##### `derive` ( `index`: `Uint` ): `PrivateKey`

Given a wallet/account index, derive a child key compatible with the iOS and Android wallets.

---

##### `sign` ( `message`: `bytes` ): `bytes`

Sign a message with this private key.

---

##### `signTransaction` ( `transaction`: [`Transaction`](reference/core/Transaction.md) ): `bytes`

Sign a transaction with this private key.

---

##### `toBytes` ( ): `bytes`

Converts this key into bytes.

---

##### `toString` ( ): `String`

Serialiazes the private key into it's der encoded ASN1 string representation

---

##### `toKeystore` ( `passphrase`: `String` ): `bytes`

Converts the private key into a keystore which can be saved on disk

---

### Properties

##### `publicKey`: [`PublicKey`](reference/cryptography/PublicKey.md)

Derive a public key from this private key.

---