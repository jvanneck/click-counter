# Setup Guide

Two free services power this site:

| What | Service | Cost |
|------|---------|------|
| Hosting | GitHub Pages | Free |
| Persistent counter (real-time) | Firebase Realtime Database | Free |

---

## Step 1 — Set up Firebase

1. Go to [console.firebase.google.com](https://console.firebase.google.com) and sign in with a Google account.
2. Click **Add project**, give it any name (e.g. `hello-world-counter`), and follow the prompts.
3. In the left sidebar go to **Build → Realtime Database**.
4. Click **Create Database**, choose a region close to you, and start in **test mode** (you can lock it down later).
5. In the left sidebar go to **Project settings** (the gear icon ⚙️ at the top).
6. Scroll down to **Your apps** and click the **Web** icon (`</>`).
7. Register the app (any nickname). Firebase will show you a config object like this:

```js
const firebaseConfig = {
  apiKey: "AIza...",
  authDomain: "your-project.firebaseapp.com",
  databaseURL: "https://your-project-default-rtdb.firebaseio.com",
  projectId: "your-project",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123...",
};
```

8. Open `index.html` and replace the seven `REPLACE_WITH_...` placeholder values with the real values from Firebase.
9. Commit and push the change:
```bash
git add index.html
git commit -m "Add Firebase config"
git push
```

---

## Step 2 — Enable GitHub Pages

1. Go to your repository on GitHub.
2. Click **Settings** → **Pages** (in the left sidebar).
3. Under **Source**, select **Deploy from a branch**.
4. Choose **main** (or whichever branch has your `index.html`) and folder **/ (root)**.
5. Click **Save**.

GitHub will give you a URL like `https://<your-username>.github.io/Hello_World/` within a minute or two. That's your live site — share it with anyone!

---

## How it works

- The counter lives in Firebase Realtime Database under the key `clickCount`.
- Every click calls Firebase's `transaction()`, which is atomic — no race conditions even if thousands of users click at the same moment.
- All open browser tabs receive updates in real time via a WebSocket listener, so the number updates live without refreshing.
- Firebase's free Spark plan supports 100 simultaneous connections and 1 GB of data — more than enough for a click counter.
