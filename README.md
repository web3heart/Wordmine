# WordMine: hosting, online play and Android app

This folder is the complete web version of WordMine.

## 1. Switch on duels and the leaderboard (free, about 10 minutes)
1. Go to https://console.firebase.google.com and click **Add project** (any name, you can turn Analytics off).
2. In the left menu choose **Build > Realtime Database > Create Database**. Pick the region nearest your players and start in **locked mode**.
3. Open the **Rules** tab, delete what is there, paste the contents of `firebase-rules.json` from this folder, then click **Publish**.
4. Copy the database URL shown at the top of the Data tab. It looks like `https://yourname-default-rtdb.firebaseio.com`.
5. Open `config.js` in this folder and paste that URL between the quotes after `window.WM_NET =`.

Without this step the game still works. Duels and the leaderboard simply show as switched off. Friend challenges work either way, because the challenge code carries everything.

## 2. Put it online (free, needs https)
Upload this whole folder to any static host. The easiest options:
- **Netlify Drop**: go to https://app.netlify.com/drop and drag the folder in. You get a link right away.
- **Firebase Hosting** or **GitHub Pages** also work.

Open the link on your phone. In Chrome you can tap **Add to Home screen** and it installs like an app, works offline, and has its own icon.

## 3. Make an Android APK
1. Go to https://www.pwabuilder.com and paste your hosted link.
2. Choose **Package for stores > Android**, then download the package.
3. The zip contains an APK you can send to friends (they must allow "install unknown apps") and an AAB file if you ever publish on Google Play. Keep the signing key file it gives you safe. You need it for every update.

## 4. How online play works
- **Duel**: one player creates a 4-letter room code, the other joins. Both get the same word and 90 seconds. Scores update live. The higher score wins.
- **Leaderboard**: shows today's Daily Challenge scores and all-time total points.
- **Challenge**: after any level, Share result sends a code. A friend pastes it in Play online > Challenge and plays the same word.

## 5. Good to know
- Scores are sent from the phone, so a determined player could fake one. That is fine for a friends game. A strict leaderboard would need a server that checks scores.
- Only the player name, scores and room codes are stored. No emails or phone numbers.
- Old duel rooms are deleted by the host after a game. Ones that were abandoned can be cleared in the Firebase console any time (Data tab, delete the `duel` node).
- The free Firebase plan is plenty for a friends group. Watch the usage tab if the game grows.
- To test duels faster, add `window.WM_DUEL_TIME = 15;` to `config.js` (seconds). Remove it afterwards.
