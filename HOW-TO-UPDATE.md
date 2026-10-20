# How to update the website

Everything below is done on **github.com** in your web browser. You never need to install
anything. After each change, GitHub rebuilds the site automatically; the live site updates in
1 to 2 minutes. (To watch progress, open the repository's **Actions** tab. A green check means
it's live; a red X means something in the edit broke the build, see "If something goes wrong".)

## Where things are

| To change... | Edit this file |
|---|---|
| The CV | Replace `assets/cv.pdf` |
| Courses on the Teaching page | `_data/teaching.yml` |
| Publications and presentations | `_data/research.yml` |
| The About Me text, address, phone | `index.html` |
| The photo | Replace `assets/photo.jpg` |
| Site name, tagline, menu | `_config.yml` |
| Colors and fonts | `assets/style.css` |

To edit a text file on GitHub: open the file, click the **pencil icon** (Edit) at the top
right, make the change, then click **Commit changes...** and **Commit changes** again.

## Update the CV

1. Save the new CV as a PDF and name it exactly **`cv.pdf`**.
2. On GitHub, open the **`assets`** folder.
3. Click **Add file > Upload files** and drag in `cv.pdf`.
4. Click **Commit changes**. It replaces the old one.

The CV page shows the PDF and offers it for download, so nothing else needs changing. If your
browser still shows the old CV, refresh the page (it can cache it for up to 10 minutes).

## Add a new term of courses

1. Open **`_data/teaching.yml`** and click the pencil icon.
2. Find the line `- term: Fall 2026` (the newest term, near the top).
3. Click at the start of that line and paste a new block **above** it, for example:

   ```yaml
       - term: Spring 2027
         courses:
           - code: STAT 8406
             title: Regression Methods
             link: https://brightspace.villanova.edu/d2l/home/12345

   ```

4. Commit.

The term at the top is automatically highlighted as the current term, and the previous one
turns grey. The `link:` line is optional: leave it out and the course is shown without a link.

**Indentation matters.** Use spaces (not Tab), and line each new line up with the matching
line in the term below it: `- term:` under `- term:`, `courses:` under `courses:`, and so on.

## Add a publication or presentation

1. Open **`_data/research.yml`** and click the pencil icon.
2. Under `publications:` (or `presentations:`), add a new line at the **top** of the list:

   ```yaml
     - 'Frey, J. and Zhang, Y. (2027). “Title,” Journal Name, 1(1), 1-10.'
   ```

   Start with two spaces, a dash, a space and a straight single quote `'`, and end with `'`.
   If the text itself contains a straight apostrophe, type it twice: `Fisher''s`. Curly
   quotes (“ ” ’) are fine as they are.
3. To link to the paper, wrap words like this: `[Title](https://doi.org/...)`.
4. Commit.

## Change the About Me text

Open **`index.html`**, click the pencil icon, and change the words between the tags (leave the
parts in `< >` alone). `<br>` means "new line"; each paragraph sits between `<p>` and `</p>`.

## If something goes wrong

- **The site didn't change and Actions shows a red X:** the last edit has a typo, usually
  indentation in a `.yml` file or a missing `'` at the end of a line. Open the file, compare
  your new lines with the ones around them, fix, and commit again.
- **Undo a change:** open the file, click **History**, open the earlier version, and copy its
  text back in. Every past version is kept.

---

## One-time setup (publishing the site)

1. Create a free account at https://github.com and sign in.
2. Create a new **public** repository (the **+** at top right, then **New repository**).
   - Name it **`<your-username>.github.io`** for the site to live at
     `https://<your-username>.github.io/`, or any name (for example `website`) for
     `https://<your-username>.github.io/website/`. Either works with the steps below.
3. On the new repository's page, click **uploading an existing file**, drag in **everything
   inside** the `github-site` folder (including the `_data` and `_layouts` folders), and
   commit.
4. Go to **Settings > Pages**. Under **Build and deployment**, set **Source** to
   **Deploy from a branch**, branch **main**, folder **/ (root)**, and **Save**.
5. After a minute or two, the address appears at the top of that page. Open it to check.

### Using zhangyimin.com (optional)

Do this once the github.io address looks right. Until then, zhangyimin.com keeps showing the
old WordPress site.

1. In the repository, **Settings > Pages > Custom domain**: enter `zhangyimin.com` and
   **Save**. (This adds a file called `CNAME` to the repository; leave it there.)
2. At the company that manages the domain's DNS (currently WordPress.com, under
   **Domains > zhangyimin.com > DNS records**), replace the existing A records for the bare
   domain with these four:

   | Type | Name | Value |
   |---|---|---|
   | A | @ | 185.199.108.153 |
   | A | @ | 185.199.109.153 |
   | A | @ | 185.199.110.153 |
   | A | @ | 185.199.111.153 |
   | CNAME | www | `<your-username>.github.io` |

3. Wait for the DNS check in **Settings > Pages** to pass (from minutes to a day), then tick
   **Enforce HTTPS**.

Page addresses stay the same as on the old site (`/cirriculum-vitae/`, `/research/`,
`/teaching/`), so existing links to those pages keep working. Links to old lecture-video
pages and the contact form show a "Page not found" page.
