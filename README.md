# bitPOS Card Writer

Android app for programming and wiping NTAG 424 DNA Bolt Cards.
Part of the [bitPOS](https://github.com/satosys-tech) open-source Lightning payments platform.

---

## Download

**[Download bitPOS-Card-Writer.apk](https://github.com/satosys-tech/bitpos-card-writer/releases/latest/download/bitPOS-Card-Writer.apk)**

### Install steps
1. Download the APK on your Android device
2. Go to **Settings - Security - Install unknown apps** and allow your browser or file manager
3. Open the downloaded APK and tap **Install**
4. Launch **bitPOS Card Writer**

---

## What it does

| Screen | Action |
|--------|--------|
| **Write** | Paste a bitPOS provision URL, hold card to phone - card is programmed as a working Bolt Card |
| **Wipe** | Paste the wipe JSON from bitPOS, hold card to phone - card is reset to factory defaults |

### Requirements
- Android phone with NFC
- NTAG 424 DNA card (standard Bolt Card blank)
- A running [bitPOS](https://github.com/satosys-tech/bitpos-core) instance

---

## How it works

The app implements the full NTAG 424 DNA APDU sequence over NFC:

1. **AuthenticateEV2First** - AES-128 mutual authentication with the card
2. **ChangeKey x5** - Programs k0 (app master) and k1-k4 (Bolt Card CMAC keys)
3. **ChangeFileSettings** - Enables SDM (Secure Dynamic Messaging) with LNURL-W parameters
4. **WriteBinary** - Writes the NDEF record containing the LNURL-W URL

All key material is fetched from the bitPOS API at provision time. Nothing is stored on the device.

---

## Build from source

**Requirements:** Node 20+, pnpm 9+, Expo CLI, Android phone with USB debugging or EAS account

```bash
git clone https://github.com/satosys-tech/bitpos-card-writer.git
cd bitpos-card-writer
pnpm install

# Run in Expo Go (development)
cd artifacts/card-writer
pnpm exec expo start --localhost

# Build APK via EAS cloud (requires free EAS account)
pnpm exec eas build --platform android --profile preview
```

### EAS setup (first time)
```bash
pnpm exec eas login
pnpm exec eas build:configure
```

---

## Project structure

```
artifacts/card-writer/
  app/
    (tabs)/
      index.tsx      # Write screen
      wipe.tsx       # Wipe screen
  utils/
    ntag424.ts       # NTAG 424 DNA APDU sequences
    crypto.ts        # AES-128 primitives (crypto-js)
    cmac.js          # AES-CMAC (artjomb extension)
    ndef.ts          # NDEF builder + SDM offset computation
```

---

## Contributing

Pull requests welcome. The core NFC logic is in `artifacts/card-writer/utils/ntag424.ts`.

---

## License

MIT
