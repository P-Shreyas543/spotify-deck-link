# Spotify Deck website

Website, one-click web installer and Spotify login redirect for
**[Spotify Deck](https://github.com/P-Shreyas543/esp32-spotify-deck)**, an open-source
ESP32 Spotify "now playing" touch display (album art, play/pause, skip, volume).

**Live: https://p-shreyas543.github.io/spotify-deck-link/**

| File | Purpose |
|---|---|
| `index.html` | Landing page and install button; also the OAuth redirect target (see below) |
| `firmware/` | `manifest.json` and `spotify_deck-full.bin` for [ESP Web Tools](https://esphome.github.io/esp-web-tools/) |
| `privacy.html` | What the deck and this site do with data |

## Spotify login redirect

Spotify only sends a browser back to an `https://` address after login, but the deck
is a plain-HTTP device on the home network. When `index.html` is opened with
`?code=` or `?error=`, it forwards the browser to the deck at the private address
carried in the OAuth `state` parameter (`<IPv4>_<nonce>`); the deck then finishes the
Authorization Code + PKCE exchange.

The page stores nothing, has no analytics, and only forwards to private IPv4
addresses (10/8, 172.16/12, 192.168/16). The code is single-use and useless without
the PKCE verifier, which never leaves the deck.

Redirect URI to register in a Spotify app: `https://p-shreyas543.github.io/spotify-deck-link/`
(any Spotify app may use it).

## Updating the installer firmware

Copy `spotify_deck-full.bin` from a
[firmware release](https://github.com/P-Shreyas543/esp32-spotify-deck/releases) into
`firmware/` and bump `version` in `firmware/manifest.json`.

MIT license. Spotify is a trademark of Spotify AB; this project is not affiliated
with Spotify.
