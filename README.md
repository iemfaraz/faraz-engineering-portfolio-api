# Faraz Engineering Portfolio API

GitHub-ready documentation and validation starter for the existing Faraz Engineering Portfolio API.

## Important: what this repository does

- Stores the OpenAPI 3.0.3 specification in `openapi.json`.
- Provides a Swagger UI page (`index.html`) for exploring and testing the API.
- Validates the OpenAPI document automatically with GitHub Actions.

**The API backend is still hosted at Base44** at the server URL defined in `openapi.json`. GitHub is repository hosting (and can host static documentation with GitHub Pages); uploading this repository to GitHub does **not** deploy or replace the backend API.

## Before you start

1. Confirm you can access the Base44 portfolio app and that its API is enabled.
2. Obtain an API key from the API provider. Never commit the key to this repository.
3. Check that the provider permits requests from the domain where Swagger UI is hosted. Browser CORS restrictions are controlled by the API server.

## Run Swagger UI locally

You can open `index.html` in a browser, but some browsers restrict local file access. A simple local server is more reliable:

```bash
python -m http.server 8000
```

Then open <http://localhost:8000>.

In Swagger UI:
1. Click **Authorize**.
2. Enter your API key in the `api_key` field.
3. Click **Authorize**, then close the dialog.
4. Try a safe `GET` endpoint first.

Do not use the bulk `DELETE` endpoints with an empty `{}` filter: the specification warns that this can delete all records for an entity.

## Upload to GitHub

1. Create a repository on GitHub, for example `faraz-engineering-portfolio-api`.
2. Upload the files in this folder, or run these commands from this folder after installing Git:

```bash
git init
git add .
git commit -m "Add portfolio API specification and Swagger docs"
git branch -M main
git remote add origin https://github.com/YOUR_GITHUB_USERNAME/faraz-engineering-portfolio-api.git
git push -u origin main
```

Replace `YOUR_GITHUB_USERNAME` with your actual GitHub username.

## Enable GitHub Pages (optional)

In GitHub, open **Settings → Pages** and choose **Deploy from a branch**, select `main` and `/ (root)`, then save. GitHub Pages will publish the static Swagger UI documentation. This does not host the API backend itself.

## API authentication

The specification uses an `api_key` HTTP header. Do not put a real key into `index.html`, `openapi.json`, GitHub Actions files, screenshots, or commits. Swagger UI asks the operator to enter the key at runtime.

## Troubleshooting

- **401/403:** verify the key and account permissions with the API provider.
- **CORS error:** configure allowed origins on the Base44/backend side; GitHub cannot fix server CORS policy.
- **404:** verify the server URL and endpoint path in `openapi.json`.
- **GitHub Pages displays the docs but API calls fail:** Pages hosts only the documentation; the API remains on the configured Base44 server and must be reachable from the browser.
