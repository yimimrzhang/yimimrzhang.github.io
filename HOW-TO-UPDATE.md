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

## How the site is hosted (for reference)

| | |
|---|---|
| Address | https://zhangyimin.com (www.zhangyimin.com and yimimrzhang.github.io redirect to it) |
| GitHub repository | `yimimrzhang/yimimrzhang.github.io`, published from branch **main**, folder **/ (root)** (**Settings > Pages**) |
| Domain | Registered at Namecheap (auto-renew on). Its DNS is **Namecheap PremiumDNS**: Domain List > zhangyimin.com > Manage > **Advanced DNS**. |
| Visitor stats | Two services, both without cookies. **Umami** (shows cities): sign in at cloud.umami.is. **Cloudflare Web Analytics** (country only): dash.cloudflare.com > **Analytics & Logs** > **Web Analytics**. Each has one tracking line in `_layouts/default.html` (Umami's in the `<head>`, Cloudflare's just before `</body>`); deleting a line turns that service off. |

The domain's DNS records that point it at GitHub:

| Type | Host | Value |
|---|---|---|
| A Record | @ | 185.199.108.153 |
| A Record | @ | 185.199.109.153 |
| A Record | @ | 185.199.110.153 |
| A Record | @ | 185.199.111.153 |
| CNAME Record | www | yimimrzhang.github.io |

There is no email on this domain. The Mail Settings section can stay as it is.

**Don't delete the `CNAME` file** in the repository. It tells GitHub to serve the site at
zhangyimin.com. If the domain ever stops working, check **Settings > Pages > Custom domain**
still says `zhangyimin.com`, and that **Enforce HTTPS** is ticked.

Page addresses are the same as on the old WordPress site (`/cirriculum-vitae/`,
`/research/`, `/teaching/`). Old lecture-video, course and contact-form addresses show a
"Page not found" page. The course pages were saved offline in `D:\Yimin_Course_Pages\`.

### Setting it up again from scratch

1. Create a **public** GitHub repository named `<username>.github.io`.
2. Click **uploading an existing file**, drag in **everything inside** the `github-site`
   folder (including `_data`, `_layouts`, `assets` and `CNAME`), and commit.
3. **Settings > Pages**: Source **Deploy from a branch**, branch **main**, **/ (root)**,
   **Save**. Enter the custom domain and **Save**.
4. Point the domain's DNS at GitHub with the records above, replacing `yimimrzhang` with the
   new username. When the DNS check passes, tick **Enforce HTTPS**.
