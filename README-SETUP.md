# Forest Cafe - setup notes

## Where the DUMMY values are (replace before going live)
| File | What to replace |
|---|---|
| `js/firebase-config.js` | `apiKey`, `projectId`, `authDomain` (Firebase > Project settings > Your apps > Web app) |
| `firestore.rules` | `PASTE_OWNER_UID_HERE` (Firebase > Authentication > Users > User UID of the owner) |
| `.firebaserc` | `forest-cafe-DUMMY-PROJECT-ID` (your real Project ID) |
| `robots.txt`, `sitemap.xml` | `forestcafe.in` only if the final domain is different |

## Firebase steps
1. Create project, then Firestore Database (region asia-south1), then Authentication > Email/Password ON.
2. Authentication > Users > Add user (owner email + password). Copy the User UID into `firestore.rules`.
3. Authentication > Settings > User actions: turn OFF "Enable create (sign-up)".
4. Deploy rules + site:  `firebase login`, then `firebase deploy`
5. Hosting > Add custom domain, then add the DNS records at the domain registrar.
6. Google Cloud Console > APIs & Services > Credentials > the Browser key > restrict to your domain (HTTP referrers):
   `https://forestcafe.in/*`, `https://www.forestcafe.in/*`, `https://<project>.web.app/*`

## Data stored
Firestore document `site/content` has one string field `json` (+ `updatedAt`).
Delete that document to go back to the built-in text.
