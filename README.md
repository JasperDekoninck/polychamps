# Polychamps

Website for the chess tournament between ETH Zurich and EPFL.

The static website lives in `Array/`. It needs no package installation or build
command. This repository starts from the website snapshot at commit
`b313516d3190cb4a0a84ba176c631516d9171b3d` in the original repository.

## Publish with GitHub Pages

1. Open [Settings → Pages](https://github.com/JasperDekoninck/polychamps/settings/pages).
2. Under **Build and deployment**, set **Source** to **GitHub Actions**.
3. Open [the deployment workflow](https://github.com/JasperDekoninck/polychamps/actions/workflows/pages.yml).
   Select **Run workflow**, choose `main`, and run it. If the initial push failed
   because Pages was not enabled, this new run replaces that failed attempt.
4. After the workflow succeeds, visit
   <https://jasperdekoninck.github.io/polychamps/> and check the site.

The workflow publishes the contents of `Array/`, so `Array/index.html` becomes
the site's homepage. Future pushes to `main` deploy automatically.

## Connect polychamps.ch

Only switch the domain after testing the temporary Pages address.

1. In [your account's Pages settings](https://github.com/settings/pages), add
   `polychamps.ch` and follow GitHub's DNS TXT verification instructions. Keep
   the verification record after verification.
2. In this repository's **Settings → Pages**, set **Custom domain** to
   `www.polychamps.ch` and save.
3. At the authoritative DNS provider, replace the website records with:

   | Type | Name | Value |
   | --- | --- | --- |
   | A | @ | 185.199.108.153 |
   | A | @ | 185.199.109.153 |
   | A | @ | 185.199.110.153 |
   | A | @ | 185.199.111.153 |
   | CNAME | www | jasperdekoninck.github.io |

   On 29 September 2026, the domain's nameservers were
   `cosmos.dns-parking.com` and `nova.dns-parking.com`. DNS edits must be made
   at that provider unless the nameservers are changed. If moving DNS to
   GoDaddy, preserve the existing DNS zone, including email records and other
   subdomains, before switching nameservers. Replace the old website A/CNAME
   records; preserve unrelated records. If obsolete website AAAA records are
   present, remove or replace them with GitHub's documented IPv6 addresses.
4. Once DNS validation and certificate issuance finish, enable **Enforce HTTPS**
   in Pages settings. Check both `https://www.polychamps.ch/` and
   `https://polychamps.ch/`; the latter should redirect to `www`.

No changes to the previous Netlify account are needed. No `CNAME` file is needed
for this Actions-based deployment; set the custom domain in repository settings.

Reference: [GitHub custom domain documentation](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site).

## Local preview

From the repository directory, run:

```sh
python3 -m http.server 8000 --directory Array
```

Then open <http://localhost:8000/>.

The lowercase directories containing small `index.html` redirects preserve the
extensionless page URLs previously served by Netlify. The original HTML pages
and assets retain their filenames.
