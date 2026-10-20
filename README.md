# spotify-deck-link

Redirect page for the Spotify Deck (an ESP32 "now playing" display).

Spotify only sends a browser back to an `https://` address after login, but the deck
is a plain-HTTP device on the home network. This one static page, served by GitHub
Pages, receives Spotify's redirect and forwards the browser to the deck at the
private address carried in the OAuth `state` parameter. The deck then finishes the
login (Authorization Code with PKCE) itself.

The page stores nothing, loads nothing from other sites, and only forwards to
private IPv4 addresses (10/8, 172.16/12, 192.168/16). The authorization code is
useless without the PKCE verifier, which never leaves the deck.

Redirect URI to register in the Spotify app: `https://p-shreyas543.github.io/spotify-deck-link/`
