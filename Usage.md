The repository includes some automation to help with building and testing.  Check out `Gruntfile.js` for more details on how each task works.

## Building

Once you've built everything, it's just a bunch of files that all need to be put together, right? This is how it happens.

### Starting the build daemon

In most cases running `npm start` and letting the watcher do the builds for you will get the job done. This will automatically watch for any changes in the relevant Handlebars folders. `templates`, `layouts`, `partials`, and `stylesheets`.

```bash
npm start
```

### Building HTML or CSS

If you ever want to just rebuild the HTML or CSS independently, you can use either of the following.

```bash
npm run html
npm run css
```

### Managing Image Assets

In order to use images with your email templates in Postmark, you'll need to host the images on a CDN or asset server. Once you've finished with [configuration](https://github.com/wildbit/mailmason/wiki/Getting-Started#configuration), these tasks will automatically grab your images and upload them to your FTP server or Amazon S3 bucket.

Since MailMason assumes that you're not using images, there's currently no built-in monitoring for changes to image files. When you change images, you'll need to explicitly update them on your asset server when you make changes locally. 

To upload images to an **FTP server** use the `images:ftp` task.

```bash
npm run images:ftp
```

To upload images to an **Amazon S3** bucket use the `images:s3` task.

```bash
npm run images:s3
```

## Viewing

When you're working on a dozen different emails that all also need to be responsive and have plain text versions, it can be pretty tedious to reload and check on them all manually, so we've included a `preview.html` file that loads up all of the rendered emails for easy previewing. Of course, you'll still need to test them in Litmus, but this helps with the fundamental development.



## Testing

The emails need to look great, right? So you'll have to see them in action? So there are a handful of commands to help you do this. To use these, you'll have to configure Postmark settings in `secrets.json` so you can send the emails.


### Spamcheck

[Spamcheck](http://spamcheck.postmarkapp.com) is a free Postmark service to send the content of your emails through a basic Spam Assassin check for content. The current setup for [grunt-spamcheck](https://github.com/derekrushforth/grunt-spamcheck) doesn't include headers in the requests. So the API will return some header-related errors. It's safe to ignore these. We're working on updating the Spamcheck API and grunt-spamcheck to handle this a little more gracefully.

```bash
npm run spamcheck
```

### Litmus

If you have a Litmus account, this makes it easier for you to fire off a test email to your [Litmus](https://litmus.com) account. Once you specify the Litmus test email address in `config.json` you're off to the races.

**Important:** This test pulls emails from `/dist/compiled` since the CSS needs to be inlined to render an accurate test result on Litmus.

```bash
npm run litmus
```

### Send All the Emails

This will send a copy of each email in the `/dist/compiled` folder to your personal address. 

**Important:** If you have a lot of templates, this will send a lot of emails to your personal address. Use it wisely.

```bash
npm run flood
```

## Pushing templates to Postmark

MailMason uses the [postmark-cli](https://github.com/wildbit/postmark-cli) tool to push your templates up to Postmark. Before getting started, ensure that you enter the Postmark server token of the destination server in `secrets.json`. 

```bash
npm run deploy
```

This command pushes the templates from `/dist/postmark-templates` and layouts from `/dist/postmark-layouts` up to Postmark. Templates in these folders do not have inlined CSS since Postmark handles this for you.

You will also be asked to review and confirm your changes before pushing:
![Postmark CLI confirmation](https://raw.githubusercontent.com/wildbit/postmark-cli/master/media/push-confirm.png) 