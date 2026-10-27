# Kawa

A riichi mahjong discard helper. Take a photo of the table (or tap the tiles in) and Kawa shows the most efficient discard, the safest discard, a digital pick, and an analog read based on strategy books.

Everything lives in one file: `www/index.html`. The tile engine (shanten, acceptance, lookahead, deal-in rates, push/fold) runs on the phone with no internet. Photo reading and the analog read call Google's Gemini API, which needs your own Gemini API key.

## Get the Android app

1. Push this repository to GitHub.
2. Open the **Actions** tab. The **Build Android APK** workflow runs on every push to `main` (or run it by hand with **Run workflow**).
3. When it finishes, open the run and download **kawa-apk** under Artifacts. Unzip it to get `app-debug.apk`.
4. Copy the APK to your phone and open it. Android will ask you to allow installs from that source the first time.

## Or use it as a web app

1. In the repository settings, go to **Pages** and set the source to **GitHub Actions**.
2. The **Publish web app** workflow puts the app at `https://<your-user>.github.io/<repo>/`.
3. Open that link in Chrome on your phone and choose **Add to Home screen**. The camera works from the browser too.

## Connect Gemini

Open **Rules and scores** in the app, paste a Gemini API key (from Google AI Studio, aistudio.google.com/apikey), and tap **Save**. The key is stored only on that device, never in the repository. Calls are billed to your Google AI account; the model defaults to `gemini-flash-latest` and can be changed in the same box (for example to `gemini-pro-latest` for harder photos).

Never commit an API key to GitHub.

## Editing

- The engine, the safety tables and the book principles are all in the `<script>` block of `www/index.html`.
- `PRINCIPLES` holds the book rules the analog read uses.
- `NUM` and `HON` are the deal-in tables from *Statistical Mahjong Strategy*.
- `digitalScore` in `pick()` holds the weights fitted against the wwyd-chan books.

To test changes on a computer, open `www/index.html` in a browser, or run any static server in the `www` folder.
