# Ultimate Tic Tac Toe — P2P

A complete game of **Ultimate Tic Tac Toe** in a single, self-contained HTML file.
No build step, no server, no accounts. Text or email the file to a friend, both
open it on your phones, trade two short codes, and play.

**File:** [`ultimate-ttt.html`](ultimate-ttt.html)

## How to play

1. Open `ultimate-ttt.html` in a mobile browser (iOS Safari / Android Chrome).
2. **Player A** taps **Create game**, copies the generated code, and sends it to Player B.
3. **Player B** taps **Join game**, pastes A's code, taps **Generate answer**, and sends
   the answer code back to A.
4. **Player A** pastes the answer and taps **Connect**. The board appears on both phones.

Moves sync directly, phone-to-phone. A **Practice on this device** button plays hot-seat
on one phone with no connection needed (handy for trying it out).

## Rules

- 9 sub-boards (a 3×3 grid of 3×3 boards, 81 cells).
- The cell you play sends your opponent to the matching sub-board.
- If that sub-board is already won or full, they may play in any open sub-board (highlighted).
- Win 3 in a row inside a sub-board to claim it; claim 3 sub-boards in a row to win the game.
- Full-with-no-line counts as a draw at the sub-board level; a full meta-board with no line
  goes to whoever claimed more sub-boards (draw if tied).

## Networking

- **WebRTC data channel**, peer-to-peer, with a **manual copy/paste handshake** — no
  signaling server and no backend.
- Game moves travel as JSON over the data channel (e.g. `{type:"move", board:4, cell:7}`).
- **Disconnect/reconnect is handled gracefully:** the board is preserved locally, and when a
  channel (re)opens both sides exchange a full-state `sync` message so the game resumes in
  agreement (higher move-count wins).

### One design note: STUN

The handshake uses public **STUN** servers (Google + Cloudflare) purely to discover each
phone's network address so the two devices can connect across different networks/NATs. STUN
is not a signaling server and carries **no game data** — all moves flow directly peer-to-peer.
This is the only network dependency, and it's only touched during the initial handshake; once
connected the game needs nothing external. (Very restrictive/symmetric NATs that require TURN
are the known limitation of any serverless P2P handshake.)

## Testing

Pure game logic and the full networked flow were verified headlessly:

- **Logic** (`scratchpad/logic2.test.mjs`): 16 assertions covering move validation, the
  redirect rule, redirect-to-won-board → free choice, sub-board/meta win + draw detection,
  and serialization. The same checks run in-browser via `__selftest()` in the console.
- **End-to-end** (Playwright, two pages): real offer/answer handshake, bidirectional move
  sync, turn indicator, illegal-move locking, the sync/reconnect resync path, the win screen,
  and rematch (resets both sides and alternates who starts).

Per the build order, the final validation target is two **physical phones on separate
networks** — that's what surfaces real handshake behavior that a single browser can't.
