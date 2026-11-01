# Aspectus Lab certificate signing keys (public)

Aspectus Lab signs the certificate that comes with each piece. The certificate is **a record of our sale, not proof of ownership.** These are the public keys anyone can use to check that a certificate was issued by us. They are published here, on our website, and anchored in Bitcoin, so a swapped copy in one place shows up against the others.

## The two root keys

| Root | Short id | Public key (Ed25519, 32 bytes, hex) |
|---|---|---|
| A | `833c069d` | `5c1ca113b8dd1b16849075a25cc74aaa8db57635c567c912fa47d9e366abe0ba` |
| B | `3d5ae145` | `c3561aff4792570ed3ccefc0bedec5d8913a62b8488713d2f1e1a12b12abdef2` |

The short id is the first 8 hex characters of the SHA-256 of the 32-byte public key. Each root's private key was generated inside its own hardware key (a YubiKey) on 2026-10-31 and has never left it. Either root can sign a day-to-day signing key and either can revoke the other root or a signing key.

## How certificates are checked

Chain: certificate, signed by an online signing key, signed by root A or root B. A certificate stays valid after its signing key expires, as long as the sale date was inside the key's validity. Revocations are published in `revoke-lists.json`, signed by a root.

## Files

- `roots.json`: the two keys in machine-readable form.
- `aspectus-roots-2026-10-31.txt`: the exact text that was timestamped.
- `aspectus-roots-2026-10-31.txt.ots`: the OpenTimestamps proof for that text.
- `verify.html`: a single-page checker that runs entirely in your browser.

## Check the timestamp yourself

1. `sha256sum aspectus-roots-2026-10-31.txt` should print `b5f7ae21bc36b06b7184df79b3f79f196cceb9489115931430b63a6454de18ff`.
2. `ots info aspectus-roots-2026-10-31.txt.ots` lists Bitcoin attestations. The earliest is block **974077**, whose merkle root is `ae9abd922b02d14b4f693fb060c9c3ad1afdb9e42690b14ce8944ba67e936181`. Look the block up in any Bitcoin node or block explorer and compare the merkle root.
3. With a Bitcoin node of your own, `ots verify aspectus-roots-2026-10-31.txt.ots` checks the whole chain.

Later attestations are in blocks 974103 and 974104.
