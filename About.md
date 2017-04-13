This is an overview of MailMason to help you understand if it can help you with your application's transactional templates. MailMason gives you a couple of options. The simplest and easiest option is to use the generated html and txt templates located in the distribution (`/dist`) folder. These are static files that can be plugged directly into [Postmark's](https://postmarkapp.com) templating feature. However, it's much more powerful...

# What is MailMason?

MailMason streamlines building and updating a set of consistent transactional emails. It uses Grunt, Handlebars, and SCSS in conjunction with layouts and partials to reduce redundancy and create both the HTML and plain text versions of your transactional emails in one fell swoop.

MailMason was born out of our desire to have a tool kit for generating a consistent set of transactional email templates for use within [Postmark's](https://postmarkapp.com) templating feature. However, it's something that anyone could take and fork to help them maintain their own set of email templates for Postmark or really any other email provider that offers similar functionality.

By default, the generated templates use [Mustachio](https://github.com/wildbit/mustachio) for the variable placeholders so that you can easily use them as [Postmark](https://postmarkapp.com) templates. However, the Mustachio pieces are only placeholders, and the generated templates could easily be adapted to work with any email provider.

## What can it do?

* [X] Gives you a thoroughly tested and reliable starting point for building consistent email templates
* [X] Uses Handlebars to enable layouts and partials in templates and avoid redundancy
* [X] Enables the use of SCSS for generating the styles
* [X] Automatically inlines the resulting CSS to maximize email client compatibility
* [X] Automatically generates text versions of emails with the same content as the HTML versions
* [X] Enables easy sending of test emails through your Postmark account
* [X] Enables easy batch testing against the [Postmark Spamcheck API](http://spamcheck.postmarkapp.com)
* [X] Enables easy batch testing through [Litmus](http://litmus.com)
* [X] Enables easy uploading of image assets to your CDN so you can include images in your templates (but you don't have to)

## What templates are included?

You can find the included templates as Handlebars (.hbs) files in the `/src/emails` folder. Each of these templates is based off of the advice in our thoroughly researched [Postmark Guides](https://postmarkapp.com/guides). These are just the initial templates, we'll definitely be adding more in the future.

1. **[Example](http://assets.wildbit.com/postmark/templates/index.html#example)** A base template designed only to showcase the available elements in the emails and to make it easy to test all of the styles from a single email.
1. **[Welcome](http://assets.wildbit.com/postmark/templates/index.html#welcome)** A traditional welcome email when someone new creates an account on your service.
1. **[User Invitation](http://assets.wildbit.com/postmark/templates/index.html#user_invitation)** A modified version of the welcome email that's designed when one of your existing users invites a new user, who may not be familiar with your product, to join the product and collaborate.
1. **[Invoice](http://assets.wildbit.com/postmark/templates/index.html#invoice)** An email requesting payment for a sale.
1. **[Receipt](http://assets.wildbit.com/postmark/templates/index.html#receipt)** An email acknowledging payment for a sale.
1. **[Password Reset](http://assets.wildbit.com/postmark/templates/index.html#password_reset)** An email including a link for the recipient to securely change their password.
1. **[Password Reset Help](http://assets.wildbit.com/postmark/templates/index.html#password_reset_help)** An email sent to email addresses when they do not exist in the system. You can read [everything you ever wanted to know about building a secure password reset feature](https://www.troyhunt.com/everything-you-ever-wanted-to-know/) for more detailed information on this approach.
1. **[Trial Expiring](http://assets.wildbit.com/postmark/templates/index.html#trial_expiring)** A notification sent in advance of a trial expiring so that a user can take action to avoid an interuption in service.
1. **[Trial Expired](http://assets.wildbit.com/postmark/templates/index.html#trial_expired)** A notification sent after a trial expired providing the recipient with assurances about their data and offering options for next steps.
1. **[Comment Notification](http://assets.wildbit.com/postmark/templates/index.html#comment_notification)** A simple notification that a comment has been made or an action taken.