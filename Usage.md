## Usage

The repository includes some automation to help with building and testing. 

Check out `Gruntfile.js` for more details on how each task works.

### Run specific tasks
In most cases running `npm start` and letting the watcher do the builds for you will get the job done. But sometimes you may need to run granular scripts to just build the HTML or CSS.

```bash
npm run html
npm run css
```

### Send test emails via Postmark
See the [Postmark grunt task](https://github.com/wildbit/postmark-build-templates/blob/master/Gruntfile.js#L194) for more details.

### Spamcheck all the emails
```bash
npm run spamcheck
```
See the [Spamcheck grunt task](https://github.com/wildbit/postmark-build-templates/blob/master/Gruntfile.js#L182) if you’d like to spamcheck specific emails.

### Test emails through Litmus
```bash
npm run litmus
```
See the [Litmus grunt task](https://github.com/wildbit/postmark-build-templates/blob/master/Gruntfile.js#L209) if you’d like to send the emails to Litmus for visual testing.