This is an overview of MailMason to help you understand if it can help you with your application's transactional templates.

# What is MailMason?

It's a toolset to streamline building and updating a set of consistent transactional emails. It uses Grunt, Handlebars, and SCSS to streamline building a consistent set of transactional email templates using layouts and partials to reduce redundancy and create both the HTML and plain text versions of your transactional emails in one fell swoop.

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

1. **Example** A base template designed only to showcase the available elements in the emails and to make it easy to test all of the styles from a single email.
1. **Welcome** A traditional welcome email when someone new creates an account on your service.
1. **User Invitation** A modified version of the welcome email that's designed when one of your existing users invites a new user, who may not be familiar with your product, to join the product and collaborate.
1. **Invoice** An email requesting payment for a sale.
1. **Receipt** An email acknowledging payment for a sale.
1. **Reset Password** An email including a link for the recipient to securely change their password.
1. **Reset Password Alt** An email sent to email addresses when they do not exist in the system. You can read [Everything you ever wanted to know about building a secure password reset feature](https://www.troyhunt.com/everything-you-ever-wanted-to-know/)For more detailed information on this approach.
1. **Trial Expiring** A notification sent in advance of a trial expiring so that a user can take action to avoid an interuption in service.
1. **Trial Expired** A notification sent after a trial expired providing the recipient with assurances about their data and offering options for next steps.
1. **Comment Notification** A simple notification that a comment has been made or an action taken.