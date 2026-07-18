# Ultimate Tic Tac Toe 🎮

A fun twist on tic tac toe you can play with a friend on your phones — no app
store, no sign-up, no accounts. It's just one file. Text or email it to a friend,
you both open it, and you're playing in under a minute.

**The game is the file `ultimate-ttt.html`.** Open it in your phone's browser.

---

## How to start a game

Once one-tap connect is set up (see below — a 5-minute, one-time, free step), starting
a game is as easy as sending a text:

1. **Both** open `ultimate-ttt.html` on your phones.
2. **Player A** taps **Create game** and gets a short code like `PLUM7`. Send it to your
   friend however you like (text it!).
3. **Player B** taps **Join with a code**, types it in, and taps **Join game**.

That's it — the board pops up on both phones automatically. No second code to send back.
Your moves show up on each other's screens instantly.

> **Just want to try it out?** Tap **Practice on this device** to play both sides on
> one phone. No codes, no friend needed.

> **Haven't set up one-tap connect yet?** The game still works — it just falls back to
> trading two codes by hand: Player A sends their code, Player B pastes it and sends back
> a second code, Player A pastes that. Setting up the step below removes the second code.

---

## How to play (the rules)

It's tic tac toe inside tic tac toe. The board is a big 3×3 grid, and **every square
is its own little tic tac toe board.**

- **The move you make decides where your opponent plays next.** If you play in the
  *top-right* square of a small board, your opponent must play in the *top-right* small
  board. The board they have to use lights up so it's easy to see.
- If you get sent to a board that's already won or full, you get to **play anywhere**.
- **Win a small board** by getting three in a row in it — it gets stamped with your X or O.
- **Win the game** by winning three small boards in a row.
- If a board fills up with no winner, it's a tie for that board. If the whole game fills
  up with no three-in-a-row, whoever won more small boards wins.

When the game ends, tap **Rematch** to play again — no need to trade codes a second time.

---

## Set up one-tap connect (optional, free, one time)

This is what makes it feel like iMessage: one person sends a short code, the other types
it in, done. It uses a free Google Firebase database as a tiny "post office" that passes
the connection details along for the few seconds it takes to link up. **It's free, needs
no credit card, and your friends don't set up anything** — only you do this once.

1. Go to **https://console.firebase.google.com** and sign in with a Google account.
2. Click **Add project**, give it any name, and finish (you can skip Google Analytics).
3. In the left menu, open **Build → Realtime Database**, click **Create Database**,
   pick a location, and choose **Start in test mode**.
4. At the top of the database page you'll see a URL like
   `https://your-project-default-rtdb.firebaseio.com`. Copy it.
5. Open `ultimate-ttt.html` in any text editor, find this near the top of the script:
   `const FIREBASE_DB_URL = "";` and paste your URL between the quotes. Save.
6. Send everyone the updated file. Done — now it's one code to connect!

*(Test mode opens the database for about a month; to keep it working long-term, open
Realtime Database → Rules and set them to allow the game's `rooms`. The exact rules are
written in a comment right above the `FIREBASE_DB_URL` line in the file.)*

---

## If it won't connect

The most reliable setup is to have **both phones on the same Wi-Fi** when you connect.
That works almost every time.

Playing across different homes or on cellular data can be hit or miss — some phone
networks block direct connections between phones. The game tries to work around it
automatically, and it'll show you what's happening (“connecting…”, “couldn't connect”)
instead of just freezing. If it can't connect after a bit, try again with both phones
on the same Wi-Fi.

**Dropped connection?** No problem — your game is saved. Just reconnect (make a new code
and rejoin) and the board picks up right where you left off.

---

## Good to know

- **Works on iPhone (Safari) and Android (Chrome).**
- **Everyone needs the same copy of the file.** If you make changes or get a newer
  version, re-send it so everyone's playing the same one.
- **There's no game server** — nothing ever stores or runs the game but the two phones.
  In the normal case your moves go straight phone-to-phone over an encrypted connection.
  (If a strict network blocks a direct link, that same encrypted data is routed through a
  relay so you can still play — still just the two of you, with no server seeing the game.)
- The free database only touches the connection code during the few seconds of setup, and
  that gets deleted the moment you're connected.
- No accounts, no tracking, no game history. It's just the two of you.

Have fun! 🙂
