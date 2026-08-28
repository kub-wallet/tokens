# KUB Wallet Token Registry

Name, symbol, logo, contract address, and decimals for community tokens shown in KUB Wallet. Officially listed assets such as KKUB and THBK are managed elsewhere and are not submitted here. They take precedence on any collision, so a submission reusing an official token's address, name, or symbol will be rejected.

Full submission guide: [Add New Tokens on KUB Wallet](https://bitkub-blockchain.gitbook.io/kub-wallet/assets/add-new-tokens-on-kub-wallet). This README is the field reference.

## Layout

One directory per token, named with the EIP-55 checksummed contract address.

```
tokens/
  0x1234567890AbcdEF1234567890aBcdef12345678/
    token.json
    logo/
      logo.svg
```

The checksummed address is the token's identity and cannot change. Copy it from [KUB Scan](https://kubscan.com/), which displays the checksummed form. A lowercase address is a different string and will be rejected. A submission adds exactly one directory. Pull requests touching more than one token will be asked to split.

## token.json

```json
{
  "name": "Example Token",
  "symbol": "EXM",
  "address": "0x1234567890AbcdEF1234567890aBcdef12345678",
  "chainId": 96,
  "decimals": 18,
  "logo": "logo/logo.svg"
}
```

| Field | Type | Notes |
|---|---|---|
| `name` | string | Must match the contract's `name()` exactly |
| `symbol` | string | Must match the contract's `symbol()` exactly |
| `address` | string | EIP-55 checksummed, and equal to the directory name |
| `chainId` | integer | Always `96` |
| `decimals` | integer | Must match the contract's `decimals()` |
| `logo` | string | Path to the logo, relative to this directory |

All six fields are required. Any field not listed here will be rejected. If you think something is missing, open an issue rather than adding it to your entry.

`name`, `symbol`, and `address` are duplicated between this file and the chain on purpose. The duplication is what makes them checkable, so do not tidy them into something nicer than the contract says.

`chainId` never varies. It is in the file because the [Token Lists](https://tokenlists.org) standard requires it on every entry. Copy it as-is.

## Logo

Put it in `logo/logo.svg` or `logo/logo.png`.

- 1:1 square
- SVG preferred. Self-contained only.
- PNG accepted at 256×256 or larger
- Under 100 KB

A logo close to an already-listed token's logo will be rejected. So will a symbol or name close to an existing one. This is the most common way impersonation is attempted, so expect questions if yours is close to something else.

## Submitting

1. Fork this repository
2. Create `tokens/<checksummed address>/` with your `token.json` and `logo/`
3. Open a pull request

The GitHub web editor is enough, you do not need a local Git setup.

Your token's source must be verified on [KUB Scan](https://kubscan.com/) before you submit. An unverified contract will be rejected.

Put your contact in the pull request description, not in `token.json`. This repository is public and permanent. We need a contact that reaches a human, including for security reports, and it is how we reach you if something goes wrong with your token entry later.