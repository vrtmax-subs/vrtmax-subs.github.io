# vrtmax-subs.github.io

Static installation site and Firefox update endpoint for VRT MAX English
Subtitles.

## Publish the first Firefox release

The extension repository's release command obtains a Mozilla-signed XPI and
stages it here:

```sh
cd ../vrt_subtitles_extension_chrome
npm ci
export WEB_EXT_API_KEY='user:…'
export WEB_EXT_API_SECRET='…'
npm run release:firefox
```

Review the resulting `firefox/vrtmax-english-subtitles.xpi` and
`firefox/updates.json`, then commit and push both repositories. GitHub Pages
must publish the `main` branch from the repository root.

After deployment, verify the two response headers:

```sh
curl -I https://vrtmax-subs.github.io/firefox/vrtmax-english-subtitles.xpi
curl -I https://vrtmax-subs.github.io/firefox/updates.json
```

The XPI must be served as `application/x-xpinstall`; `updates.json` must be
served over HTTPS. Do not publish an unsigned XPI.

## Later releases

Increment the version in both `manifest.json` and `package.json` in the
extension repository, run `npm run release:firefox`, and publish the newly
staged XPI and update manifest together.
