# Kilombinel

Fork of [wanderingking072/sentinel-android](https://github.com/wanderingking072/sentinel-android)
(itself a fork of Samourai's Sentinel), a watch-only bitcoin wallet for Android.

Why: since 2026-10-28 the Tor network requires the `Desc=3`/`Microdesc=3`
protocols, which Tor 0.4.8 does not have. Sentinel bundled Tor 0.4.8 via
kmp-tor 1.x and got stuck at "Bootstrapped 30%". Kilombinel moves to
kmp-tor 2.6.0 with Tor 0.4.9.5.

Changes on top of upstream `master`:
- kmp-tor 1.4.4 -> `io.matthewnelson.kmp-tor:runtime` / `runtime-service` 2.6.0
  + `resource-exec-tor` 409.5.0 (Tor 0.4.9.5). `TorKmpManager` rewritten, same interface.
- Kotlin 2.2.21, KSP 2.2.21-2.0.4, Room 2.7.2, compileSdk 35 (required by kmp-tor 2.x).
- Fix two compile errors left on upstream `master`.
- `SentinelTorManager.setUp` keeps the first manager (kmp-tor 2.x returns the same
  runtime per environment, so a second manager never received state events).
- `kilombinel` product flavor: own applicationId (`com.kilombino.kilombinel`),
  name and logo. The `production`/`staging` flavors still build plain Sentinel
  with the Tor fix.

Build: `./gradlew assembleKilombinelRelease` (JDK 17+, Android SDK 35), then
zipalign + apksigner with your own key.

---

# Sentinel for Android

### Build:

Import as Android Studio project. Should build "as is".

### BIP44:

Sentinel implementation based on [original BIP](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki) (https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki) extends [bitcoinj](https://bitcoinj.github.io/).

### BIP49 (Segwit):

Sentinel implementation based on [original BIP] (https://github.com/bitcoin/bips/blob/master/bip-0049.mediawiki) by Daniel Weigl and includes support for BIP49-specific XPUBs: [YPUB](https://github.com/Samourai-Wallet/sentinel-android/issues/16).

### BIP84 (Segwit):

Sentinel implementation based on [original BIP](https://github.com/bitcoin/bips/blob/master/bip-0084.mediawiki) by Pavol Rusnak.

### BIP141 (Segwit):

Sentinel P2WPKH based on [original BIP](https://github.com/bitcoin/bips/blob/master/bip-0141.mediawiki) by Eric Lombrozo, Johnson Lau and Pieter Wuille.

### BIP173 (Segwit):

Sentinel implementation based on [original BIP](https://github.com/bitcoin/bips/blob/master/bip-0173.mediawiki) by Pieter Wuille and Greg Maxwell.

### License:

[Unlicense](https://github.com/Samourai-Wallet/samourai-wallet-android/blob/master/LICENSE) (https://github.com/Samourai-Wallet/samourai-wallet-android/blob/master/LICENSE)

### Contributing:

All development goes in 'develop' branch - do not submit pull requests to 'master'.

### Contact:

[PGP](http://pgp.mit.edu/pks/lookup?op=get&search=0x72B5BACDFEDF39D7)
