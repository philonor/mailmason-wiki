There are two key folders for MailMason. The first, where you'll be making changes is the `src` directory. The second, where the final files are generated is `dist`. 

## The Distribution Folder

All of your HTML and text emails will end up here. They are constantly overwritten by the build process, so it's important not to make changes here if you want to keep them. Even though the distribution files are generated, we include them in the repository for easy access to the static results.

## The Source Folder

The source folder is the home for everything you'll need to edit on a regular basis. It's fairly straightforward.

```
/src
  /emails
  /images
  /layouts
  /partials
  /stylesheets
```

### Emails

The `/emails` folder is where you'll find the various types of emails. Each of these emails is designed based on a series of guides that we've written for each to discuss best practices and provide examples. Of course, we're planning on expanding both the guides and emails to include many more common templates, but we had to start somewhere.

* example.hbs
* comment_notification.hbs
* invoice.hbs & receipt.hbs
* reset_password.hbs & reset_password_alt.hbs
* trial_expiring.hbs & trial_expired.hbs
* user_invitation.hbs
* welcome.hbs

For the most part, your `.hbs` files will be HTML with some Handlebars variables and partials, but each email will also need some YAML front matter to specify the layout, subject, and preheaders. You can use handlebars variables in these. Here's a sample to provide some context:

```yaml
---
layout: layout.hbs
subject: Please pay {{ total }} due for {{ product_name }}
preheader: This is an invoice for your purchase on {{ purchase_date }}. Please submit payment by {{ due_date }}
---
```

### Images

The images folder is pretty simple. If you want to use images in your emails, make sure you've read up on how MailMason handles [images and assets](https://github.com/wildbit/mailmason/wiki/Getting-Started#images--assets) and the tools for [managing images and assets](https://github.com/wildbit/mailmason/wiki/Usage#managing-image-assets). If you don't need images in your templates, then you're all set, and things are much simpler.

### Layouts

Layouts are your templates for each of the emails. If every email you have uses the same header and footer, then you'll probably only need a single layout. Since different emails have different purposes, you may want to have a few different layouts depending on the context of the emails.

You can specify which layout a given email uses in the YAML front matter of the email:

```yaml
---
layout: layout.hbs
---
```

### Partials

When you're working with a suite of emails, it's inevitable that they'll share some elements like a masthead or footer. So those files go here, and you'd reference them with Handlebars just like you might expect.

If you have a `masthead.hbs` partial, you could use it in your emails like so...

```
{{> masthead }}
```

### Stylesheets

