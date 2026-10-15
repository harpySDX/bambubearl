# EMSS 3D Print Club website

Catalog, ordering and custom 3D printing for the Earl Marriott Secondary School 3D Printing Club.

- **Catalog** with All, Hot, Seasonal, Classics and Clearance collections, plus a "Hot right now" row at the top
- **Accounts**: sign up, sign in, password reset, profile, change password, delete account
- **Ordering**: cart and checkout for catalog items, custom-order requests with quotes, order tracking in each account. Customers pay in person at pickup.
- **Admin menu** (Settings ⚙ → Club administration, password protected): orders, pickup list, messages, catalog editor, filament and item stock, announcements, site settings, accounts (block troll accounts), admin password
- **Themes**: White Oak, Meadow, Sunrise, Forest, Night, or Automatic

It's a single static page (`index.html`) backed by Firebase for accounts and data. Everything after setup is done from the admin menu. No code editing.

---

## One-time setup (about 15 minutes)

### 1. Put the site on GitHub and Vercel
1. Create a new GitHub repository and upload everything in this folder (`index.html`, `firebase-config.js`, `vercel.json`, `README.md`, `.gitignore`).
2. On [vercel.com](https://vercel.com), choose **Add New → Project**, import the repository, and press **Deploy**. No build settings are needed.
3. The site goes live in demo mode right away. You'll get an address like `your-project.vercel.app`.

### 2. Create the Firebase project (free)
1. Go to [console.firebase.google.com](https://console.firebase.google.com) and **Add project**. Google Analytics is optional.
2. **Build → Authentication → Get started → Email/Password → Enable → Save.**
3. Still in Authentication, open **Settings → Authorized domains → Add domain** and add your Vercel address (for example `your-project.vercel.app`). Add your custom domain too if you have one.
4. **Build → Firestore Database → Create database.** Pick a location near you (for example `northamerica-northeast1`) and start in **production mode**.
5. In Firestore, open the **Rules** tab, delete what's there, paste the contents of the `firestore.rules` file you were given separately, and press **Publish**.
   - Keep `firestore.rules` private. Don't upload it to GitHub, because it holds the starting admin password.

### 3. Connect the site to Firebase
1. In Firebase, open **Project settings (gear) → General → Your apps → Web (</>)**, register an app (no hosting needed), and copy the `firebaseConfig` values.
2. On GitHub, open `firebase-config.js`, press the pencil icon, paste the values into the matching fields, and **Commit changes**.
3. Vercel redeploys automatically in about a minute. The yellow "Demo mode" bar disappears when it's connected.

### 4. Become an admin and load the catalog
1. On the live site, press **Sign in → Create account** and make your account.
2. Press the **⚙ Settings** button, scroll to **Club administration**, and enter the admin password.
3. In the admin menu, open **Catalog → Load starter catalog** to add example items. Then edit, replace or delete them.
4. Open **Site settings** to check the email, pickup details and payment note.
5. Recommended: open **Security** and change the admin password to a new one only your club knows.

Other club leaders make their own accounts and unlock the admin menu the same way.

---

## Everyday use (admin menu)
| Tab | What it's for |
|---|---|
| Overview | What needs doing, sales, best sellers |
| Orders | Confirm orders, send quotes for custom jobs, mark as being made or ready, cancel troll orders with a reason, block the account |
| Pickup list | Everyone waiting to collect. Press "Picked up & paid" when they pay |
| Messages | Questions from signed-in customers |
| Catalog | Add, edit, hide, delete, reorder items. Move between Classics, Seasonal and Clearance. Mark items Hot |
| Stock | Mark filament colours out of stock, track spool grams, count item stock |
| Announcements | Banners at the top of the site |
| Site settings | Pause ordering, season name, descriptions, email, pickup and payment info, rates, filament colours |
| Accounts | Every account, block or unblock, remove admin access |
| Security | Change the admin password |

**Editing right on the catalog:** when you're signed in as an admin, every item on the public catalog shows **Edit**, **Duplicate**, **Hide** and **Delete** buttons, and each collection starts with an **Add an item** tile. Hidden items stay visible to admins (faded) so you can show them again.

All changes save to the live site instantly for every visitor. Nothing ever needs a code editor.

## Free plan limits
Firebase's free Spark plan includes 50,000 document reads and 20,000 writes per day, which is plenty for a school club. Product photos are resized automatically and stored with the item.
