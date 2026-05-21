# bitPOS Card Writer

  Android app for programming and wiping NTAG 424 DNA Bolt Cards.
  Part of the [bitPOS](https://github.com/satosys-tech) open-source Lightning payments platform.

  ## Download

  [Download latest APK - GitHub Releases](../../releases/latest)

  Enable "Install unknown apps" on your Android device, then open the APK to install.

  ## Features

  - Write screen - paste a bitPOS provision URL, tap card, card is programmed as a Bolt Card
  - Wipe screen - paste the wipe JSON from bitPOS, tap card, card is reset to factory defaults
  - NTAG 424 DNA only (required for Bolt Card LUD-17 authentication)
  - Android only (iOS NFC stack does not support raw APDU for key personalization)

  ## Build from source

  Requirements: Node 20+, pnpm 9+, Expo CLI

  ```bash
  git clone https://github.com/satosys-tech/bitpos-card-writer.git
  cd bitpos-card-writer
  pnpm install
  cd artifacts/card-writer
  pnpm exec expo start --localhost
  ```

  ## License

  MIT
  