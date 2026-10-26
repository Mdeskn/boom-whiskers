# Boom Whiskers

A two-player cat card game for phones. Draw cards, dodge the Kaboom Cat, and be the last cat standing.

## Playing

1. Open `index.html` on both phones (for example through GitHub Pages).
2. One player taps **Start a game** and sends the 4-letter code to their friend.
3. The friend types the code and taps **Join**. The cards are dealt right away.

Tap **Rules** in the game for the full card list.

Keep both screens on during a game. The game asks the browser to keep the screen awake, but the host's phone runs the game, so locking it pauses play for both of you. If the guest disconnects, their move clock pauses until they come back.

## How it works

Everything is in `index.html`. There is no build step and no server of its own.

- **Connection:** the phones try to connect directly with [PeerJS](https://peerjs.com). PeerJS's public server only introduces the two phones to each other.
- **Fallback relay:** many mobile networks block direct connections. When there is no direct line, game messages go through two free public MQTT brokers ([HiveMQ](https://www.hivemq.com/mqtt/public-mqtt-broker/) and [EMQX](https://www.emqx.com/en/mqtt/public-mqtt5-broker)) at the same time, so either one can be down. No account is needed. Once a direct line opens, the relay is no longer used.
- **Rules:** the host's phone holds the full game state and checks every move. The guest only receives what they are allowed to see.
- **Card art:** every card is drawn as SVG in code.

The public brokers are free test servers with no guarantees, and anyone who knows a game's code could read that game's messages while they go through the relay, including the guest's hand and chat. That's fine for a casual game, but don't share anything private in the chat.

## Credits

Inspired by the mechanics of Exploding Kittens. All names, card art and text in this game are original. Uses [PeerJS](https://github.com/peers/peerjs) and [MQTT.js](https://github.com/mqttjs/MQTT.js) (both MIT licence) and the Google Fonts Bowlby One and Bricolage Grotesque (SIL Open Font License).
