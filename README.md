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

- **Connection:** the phones connect directly with [PeerJS](https://peerjs.com). PeerJS's public server only introduces the two phones to each other.
- **Rules:** the host's phone holds the full game state and checks every move. The guest only receives what they are allowed to see.
- **Card art:** every card is drawn as SVG in code.

## If phones can't connect

Some mobile and office networks block direct connections. To fix that, add a TURN relay server to the `TURN` list at the top of the connection script in `index.html`, using credentials from a TURN provider.
