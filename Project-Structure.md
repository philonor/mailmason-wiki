There are two key folders for MailMason. The first, where you'll be making changes is the `src` directory. The second, where the final files are generated is `dist`. 

## The Source Folder

The source folder (`/src`) is the home for everything you'll need to edit on a regular basis. It has a fairly straightforward structure:

```
/src
  /images
  /layouts
  /partials
  /stylesheets
  /templates
```

### Templates

The `/templates` folder is where you'll find the various types of emails. Each of these emails is designed based on a series of guides that we've written that discusses the best practices and provide helpful examples.

Templates are stored in their own separate folder along with a `meta.json` file for pushing it up to Postmark. The metadata file is only required if you plan on pushing your templates to Postmark. Here's an example of the JSON structure:

```js
{
  "Name": "Invoice",
  "Alias": "invoice",
  "Subject": "Please pay {{ total }} due by {{ due_date }}",
  "TemplateType": "Standard", // The type of template, either a "Standard" or "Layout"
  "LayoutTemplate": "basic" // Layout alias
}
```

For the most part, your `.hbs` files will be HTML with some Handlebars variables and partials, but each email will also need some YAML front matter to specify the layout and preheaders. You can use handlebars variables in these. Here's a sample to provide some context:

```yaml
---
layout: plain/content.hbs
preheader: This is an invoice for your purchase on {{ purchase_date }}. Please submit payment by {{ due_date }}
---
```

This only changes the layout on the email templates that are compiled together under `/dist/compiled`. To specify a different layout on a template that is uploaded to Postmark, you must edit the `LayoutTemplate` field in the template's `meta.json` file so that it contains the layout's alias.

### Images

The images folder is pretty simple. If you want to use images in your emails, make sure you've read up on how MailMason handles [images and assets](https://github.com/wildbit/mailmason/wiki/Getting-Started#images--assets) and the tools for [managing images and assets](https://github.com/wildbit/mailmason/wiki/Usage#managing-image-assets). If you don't need images in your templates, then you're all set, and things are much simpler.

### Layouts

Layouts wrap your templates with a reusable wrapper for each of the emails. If every email you have uses the same header and footer, then you'll probably only need a single layout. Since different emails have different purposes, you may want to have a few different layouts depending on the context of the emails.

MailMason comes with three different types of layouts to help you get up an running:
<img src="https://github.com/wildbit/mailmason/raw/master/media/starter-templates@2x.png" max-width="100%" alt="Starter templates side-by-side: Basic full, basic, and plain">

The layouts that come with MailMason also support dark mode on compatible email clients:
<img src="https://github.com/wildbit/mailmason/raw/master/media/dark-mode@2x.png" alt="Dark mode compatible template">

Layouts are stored in their own separate folder along with a meta.json file for pushing it up to Postmark. The metadata file is only required if you plan on pushing your templates to Postmark. Here's an example of the JSON structure:

```js
{
  "Name": "Basic",
  "Alias": "basic",
  "TemplateType": "Layout" // The type of template, either a "Standard" or "Layout"
}
```

You can specify which layout a given email uses in the YAML front matter of the email:

```yaml
---
layout: plain/content.hbs
---
```

However, this only affects the templates that are compiled together under `/dist/compiled`. To specify a different layout on a template that is uploaded to Postmark, you must edit the `LayoutTemplate` field in the template's `meta.json` file so that it contains the layout's alias.

### Partials

When you're working with a suite of emails, it's inevitable that they'll share some elements like a masthead or footer. So those files go here, and you'd reference them with Handlebars just like you might expect.

If you have a `masthead.hbs` partial, you could use it in your emails like so...

```
{{> masthead }}
```

### Stylesheets

The stylesheets support SASS, and the pre-existing stylesheets use SCSS syntax with partials. Each layout comes with its own separate stylesheet under `/src/stylesheets` that lets you style the layouts separately. 

## The Distribution Folder

All of your HTML and text emails will end up in the `/dist` folder. They are constantly overwritten by the build process, so it's important not to make changes here if you want to keep them. Even though the distribution files are generated, we include them in the repository for easy access to the static results. These files in the `/dist` folder are what you'd use within Postmark. 

The `/dist` folder contains three top-level directories: `compiled`, `postmark-layouts`, `postmark-templates`, and `stylesheets`.  

- `/dist/compiled` - Contains all of your templates with the layout combined. CSS is inlined by default so that you can upload them directory to your email service provider. These templates are also used for rendering [development previews](https://github.com/wildbit/mailmason/wiki/Development#the-previewer).
- `/dist/postmark-layouts` - Contains all of your compiled layouts so that they are compatible with Postmark. This essentially converts the handlebars `{{body}}` tag to the [Postmark `{{{@content}}}` placeholder](https://postmarkapp.com/support/article/1172-using-postmark-layouts) so that the template content can be dynamically inserted. These are what get pushed up to Postmark when running the [`deploy` command](https://postmarkapp.com/support/article/1172-using-postmark-layouts).
- `/dist/postmark-templates` - Contains all of your compiled templates so that they are compatible with Postmark. The `LayoutTemplate` in `meta.json` gets assigned to the template when pushing to Postmark via the [`deploy` command](https://postmarkapp.com/support/article/1172-using-postmark-layouts). The CSS is not inlined since Postmark handles this for you.
- `/dist/stylesheets` - Contains all of your compiled stylesheets. 