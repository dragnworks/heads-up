# Heads Up!

A browser version of the forehead party game. One player holds the device to their forehead so everyone else can see the word. Friends give clues — no saying the word itself, or a form of it. The player guesses, then marks **got it** or **pass** and the next word appears.

You do not need a server or an internet connection. The full category database lives inside `index.html`.

## Play on a Mac

1. Double-click `index.html` (or open it in Safari or Chrome).
2. Pick a category, or try **Random category** / **Mix of everything**.
3. When the 3-2-1 countdown finishes, hold the device up (or just play at the desk with the keyboard).
4. **Got it:** tap the right half of the screen, press Space, or press the right arrow.
5. **Pass:** tap the left half, or press the left arrow.
6. When time is up, you'll see the score and every word from the round.

## Play on a phone

Copy `index.html` to the phone (AirDrop, Messages, or Files) and open it in Safari or Chrome. Adding it to the Home Screen makes a nice full-screen party app.

**Tilt controls** (down = got it, up = pass) only work in a *secure context*: **HTTPS** or `localhost`. They will not work if you open the file as `file://` or over plain `http://`. That's a browser rule, not a bug. Taps and keys always work, so you can still play.

On iPhone, tilt also needs a permission prompt. Open **Settings** and tap **Enable tilt**, or just start a round — the Start tap is what iOS needs to ask.

The screen stays awake during a round when the browser's Wake Lock API is available (often HTTPS only).

## Settings

Tap the gear. Changes are saved in this browser:

- Round length: 30 / 60 / 90 / 120 seconds (default 60)
- Sound on/off — short beeps made in the browser, no audio files
- Tilt on/off
- Tilt sensitivity: Low, Medium, or High (default Medium). Tilting the screen toward the floor is "got it"; toward the ceiling is "pass." Got-it is tuned to register a bit faster and with a slightly smaller tilt than pass. After a score, bring the phone back toward upright before the next tilt will count.
- The green (got it) and orange (pass) full-screen flash is the main confirmation — it shows even when the phone is on silent or vibrate. iPhone Safari can't vibrate in a web page; Android will buzz if the browser allows it.

## Categories

There are 29 built-in decks (movies, Star Wars, Film Set & Props, and more), each with at least 60 family-friendly words. Search the grid, or play a mix of every deck.

### Add a category in the app

1. Tap **+**.
2. Give it a name and paste one word or phrase per line.
3. Save. Custom decks show a CUSTOM badge and can be edited or deleted later.

Custom categories stay in this browser's local storage.

### Edit the shared database

`categories.json` is the same database in a human-editable file:

```json
{
  "categories": [
    {
      "id": "film-set",
      "name": "Film Set & Props",
      "emoji": "🎥",
      "description": "Cameras, grip gear, props, and the stuff that makes a movie",
      "words": ["Gaffer tape", "Slate", "Boom mic"]
    }
  ]
}
```

- **Export all** downloads a `categories.json` of every built-in and custom deck (including any words you imported).
- **Import JSON** merges a file of that shape: new ids are added as custom decks; existing ids get any new words merged in (no duplicates).

If you edit `categories.json` by hand and also want those changes inside `index.html`, run:

```bash
python3 build_categories.py
```

from this folder (it rebuilds the JSON from the word lists, then embeds it). Or paste the JSON into the `BUILTIN_DB` object near the bottom of `index.html`.

A quick check for empty decks and duplicate words:

```bash
python3 validate_categories.py
```
