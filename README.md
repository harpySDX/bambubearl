# Bambubearl

The online catalog for **Bambubearl**, the Earl Marriott Secondary 3D Printing Club. Visitors browse what the club prints and what it costs; there's no cart or customer accounts. To get something, they email the club (bambearl@gmail.com) and pay in person at pickup.

**What visitors see**
- The catalog: Basic, Gentleman, Traffic Cone, Santa, Elf, Gingerbread and Custom geese; the Death Whistle; the Infinity Cube; and custom 3D prints
- Tabs for All, Hot, Holiday, Classics and Clearance (empty tabs stay visible), plus search, sort and category filters
- Each item opens with photos, a size picker (Standard 23.46 mm, Jumbo 35.19 mm, SJM 93.84 mm, Super Jumbo 187.68 mm), the price for each size, colours, and an "Ask about this item" email button
- A goose price chart: Classic, Special and Custom geese, with regular and holiday sale prices
- Liquid-glass design with themes in ⚙ Settings

**What admins can do** (⚙ Settings → Club admin)
- Edit right on the catalog: every card shows Edit, Duplicate, Hide and Delete, and each collection starts with an "Add an item" tile
- Catalog tab: reorder items, move them between collections, mark items Hot or sold out. Each item either uses the goose price chart (Classic, Special or Custom), has its own sizes and prices, or is "custom quote"
- Site settings → Goose price chart: change the goose sizes and prices in one place; every goose updates
- Site settings → Sale: switch the holiday sale prices on or off
- Stock tab: mark filament colours out of stock, track grams left, count items already printed
- Announcements: banners at the top of the site
- Site settings: holiday decorations on or off, headline text, season name, collection descriptions, email, rates, filament colours
- Admins: see who has access, remove access, change the club admin password

Every change saves to Firebase and appears for everyone right away. You never need to edit code.

---

## Setup (about 15 minutes)

### 1. GitHub and Vercel
1. Make a new GitHub repository and upload everything in this folder, including the `img` folder with the product photos.
2. On vercel.com, choose **Add New → Project**, import the repository, and press **Deploy**. It goes live in demo mode.

### 2. Firebase (free)
1. Go to console.firebase.google.com and choose **Create a project**.
2. Go to **Build → Authentication → Get started → Email/Password**, turn on the first switch and **Save**. This is only for admin logins.
3. Go to **Authentication → Settings → Authorized domains → Add domain** and enter your Vercel address, for example `bambubearl.vercel.app`.
4. Go to **Build → Firestore Database → Create database**:
   - Choose Standard edition, keep the ID as **(default)**, pick a nearby location, and choose **production mode**.
   - Open the **Rules** tab, replace everything with the contents of `firestore.rules`, and press **Publish**.
   - Keep `firestore.rules` private, because it holds the starting club admin password. Never upload it to GitHub.
5. Go to **Project settings → Your apps → Web `</>`**, register an app, and copy the config values.

### 3. Connect
1. On GitHub, open `firebase-config.js`, press the pencil icon, paste in the values, and **Commit changes**.
2. Wait about a minute for Vercel to redeploy. Admin changes now save for everyone.

### 4. First admin
1. Open ⚙ Settings → Club admin → **New admin**.
2. Enter your email, a password of your own, and the club admin password.
3. Open the admin menu → **Catalog → Load our product list**. If you loaded the old sample items before, use **Reset to our product list** instead.
4. In **Admins**, change the club admin password to a new one.

### Check it works
- Open the site in a private window: the catalog shows and there are no admin buttons.
- Change a price as an admin, then refresh the private window. The new price shows.
- If something fails, press F12 → Console. `auth/unauthorized-domain` means you need to add your address to Authorized domains. `permission-denied` means the rules weren't published.
