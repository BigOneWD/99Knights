# Deploy 99Knights 2D to GitHub Pages

Repository: `BigOneWD/99Knights-2D-`

## 1. Make the repository public

For GitHub Free, GitHub Pages requires a public repository. On GitHub:

1. Open the repository.
2. Go to **Settings → General**.
3. Scroll to **Danger Zone**.
4. Choose **Change repository visibility → Make public**.

Skip this step if the account has GitHub Pro and you deliberately want to keep the source repository private.

## 2. Push the game with GitHub Desktop

The `index.html` file is about 38 MiB, which is too large for GitHub's browser upload but is below GitHub's 100 MiB Git limit.

1. Open GitHub Desktop.
2. Choose **File → Clone Repository**.
3. Select `BigOneWD/99Knights-2D-` and clone it.
4. Copy these three files into the cloned repository root:
   - `index.html`
   - `.nojekyll`
   - `README.md`
5. In GitHub Desktop, enter the summary: `release: publish illustrated v1.0`
6. Click **Commit to main**.
7. Click **Push origin**.

## 3. Enable GitHub Pages

1. Open **Settings → Pages** in the repository.
2. Under **Build and deployment**, choose **Deploy from a branch**.
3. Select branch **main** and folder **/(root)**.
4. Click **Save**.

The expected play URL is:

`https://bigonewd.github.io/99Knights-2D-/`
