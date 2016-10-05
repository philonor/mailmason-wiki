The repository includes some automation to help with building and testing.  Check out `Gruntfile.js` for more details on how each task works.

## Starting the build daemon

In most cases running `npm start` and letting the watcher do the builds for you will get the job done. This will automatically watch for any changes in the relevant Handlebars folders. `emails`, `layouts`, `partials`, and `stylesheets`.

`npm start`

## Building HTML or CSS

If you ever want to just rebuild the HTML or CSS independently, you can use either of the following.

`npm run html`
`npm run css`

## Managing Image Assets

In order to use images with your email templates in Postmark, you'll need to host the images on a CDN or asset server. Once you've finished with [configuration](https://github.com/wildbit/mailmason/wiki/Getting-Started#configuration), this task will automatically grab your images and FTP them to your asset server.

`npm run images`

## Testing

The emails need to look great, right? So you'll have to see them in action? So there are a handful of commands to help you do this. To use these, you'll have to configure Postmark settings in `secrets.json` so you can send the emails.


### Spamcheck

[Spamcheck](http://spamcheck.postmarkapp.com) is a free Postmark service to send the content of your emails through a basic Spam Assassin check for content. The current setup for [grunt-spamcheck](https://github.com/derekrushforth/grunt-spamcheck) doesn't include headers in the requests. So the API will return some header-related errors. It's safe to ignore these. We're working on updating the Spamcheck API and grunt-spamcheck to handle this a little more gracefully.

`npm run spamcheck`

### Litmus

If you have a Litmus account, this makes it easier for you to fire off a test email to your [Litmus](https://litmus.com) account. Once you specify the Litmus test email address in `config.json` you're off to the races.

`npm run litmus`

### Send All the Emails

**Important:** If you have a lot of templates, this will send a lot of emails to your personal address. Use it wisely.

`npm run flood`


### Run specific tasks


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