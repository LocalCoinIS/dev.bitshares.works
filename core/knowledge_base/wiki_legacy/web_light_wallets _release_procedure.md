## Web and light wallets release procedure

### Release Notes

- Checkout and test [graphene-ui master](https://github.com/cryptonomex/graphene-ui)
- Add release notes to `graphene-ui/release-notes.txt`
- Commit your changes

### localcoin wallet release:
- Clone [localcoin graphene-ui](https://github.com/localcoinis/localcoin-ui)
- Add upstream repo `git remote add cnx https://github.com/cryptonomex/graphene-ui`
- Fetch upstream `git fetch cnx`
- Merge upstream/master `git merge cnx/master`
- Run `npm install` in `dl/` and in `web/`
- Commit changes to Localcoin repository
- Tag using in this format: `2.X.YYMMDD`
- Push including tags `git push --tags`
- Build (`cd web/ && npm run build`)
- Open `dist/index.html` and make sure everything is working and the version in status bar matches tag
- Clone `https://github.com/cryptonomex/faucet` and checkout ol branch and install gems with bundle command
- In faucet dir run `mina wallet` - this will deploy to 'ol' server (specified in `.ssh/config`)
- Alternatively, copy the dist folder directly to the server: scp dist/* localcoin.LocalCoin.is:/www/current/public/wallet/
- Open [https://wallet.localcoin.is](https://wallet.localcoin.is/) and make sure there are no errors and version matches release tag

### Light wallets

- (one time) Install [NSIS](http://nsis.sourceforge.net/Main_Page)
- `git clone https://github.com/localcoinis/localcoin-ui` branch `localcoin`
- Add upstream repo `git remote add cnx https://github.com/cryptonomex/graphene-ui`
- Fetch upstream `git fetch cnx`
- Merge upstream/master into localcoin branch `git merge cnx/master`
- Run `npm install` in `dl/` ,` web/` and in `electron/`
- Tag it with release version
- Edit `electron/build/package.json` and update version
- Commit your changes and push both commits and tags
- Build it in `web/` via `npm run electron` command
- Goto to `electron/`
- Build light wallet via `npm run release` command
- It will create dmg/deb/exe file in `releases/`
- Make sure created file name matches tag/version
- Run installer and test the app
- Go to localcoin-uirepo
- Update gui_version, commit, tag and push - this will create a new tag
- Open https://github.com/localcoinis/localcoin-ui/releases, create new release under tag created in previous step
- Specify release notes, upload dmg/deb/exe wallets created earlie

### LocalCoin.is wallet and downloads page

- Go to localcoin.gihub.io repo (`git clone https://github.com/localcoinis/localcoin.github.io`)
- Copy `localcoin-ui/web/dist/*` to `wallet/`
- Edit `_includes/download.html` and update download links and gui release date
- Commit and push
