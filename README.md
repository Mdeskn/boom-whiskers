# Boom Whiskers

A cat card game for 2 to 10 phones. Draw cards, dodge the Kaboom Cat, and be the last cat standing.

## Playing

1. Open `index.html` on every phone (for example through GitHub Pages).
2. One player picks how many players there will be (2 to 10), taps **Start a game**, and sends the 4-letter code to the others.
3. Everyone else types the code and taps **Join**. The cards are dealt when everyone is in. The host can also start early with the players who have joined.

Tap **Rules** in the game for the full card list.

Keep your screen on during a game. The game asks the browser to keep the screen awake, but the host's phone runs the game, so locking it pauses play for everyone. If someone disconnects, their move clock pauses until they come back. If they aren't coming back, the host can remove them and the game carries on.

## How it works

Everything is in `index.html`. There is no build step and no server of its own.

- **Connection:** the phones try to connect directly with [PeerJS](https://peerjs.com). PeerJS's public server only introduces the phones to each other.
- **Fallback relay:** many mobile networks block direct connections. When there is no direct line, game messages go through two free public MQTT brokers ([HiveMQ](https://www.hivemq.com/mqtt/public-mqtt-broker/) and [EMQX](https://www.emqx.com/en/mqtt/public-mqtt5-broker)) at the same time, so either one can be down. No account is needed.
- **Rules:** the host's phone holds the full game state and checks every move.
- **Privacy:** each player's hand, moves and chat are encrypted between that phone and the host (ECDH key exchange and AES-GCM in the browser). Other players and anyone listening on the public relay can't read them. Encryption needs the page to be served over HTTPS, which GitHub Pages does.
- **Card art:** every card is drawn as SVG in code.

The public brokers are free test servers with no guarantees.

## Credits

Inspired by the mechanics of Exploding Kittens and its expansions. All names, card art and text in this game are original. Uses [PeerJS](https://github.com/peers/peerjs) and [MQTT.js](https://github.com/mqttjs/MQTT.js) (both MIT licence) and the Google Fonts Bowlby One and Bricolage Grotesque (SIL Open Font License).
