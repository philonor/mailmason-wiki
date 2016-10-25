Building HTML emails is a little tedious, so we've added some convenience tools to make things move a little quicker.

# The Previewer

When you're working locally, there's a `preview.html` file that provides quick access to view the various versions and widths of the emails. There's nothing fancy going on here, but it is generated dynamically to make it easy to update. Just add a new template name and description, and you're off to the races.

Each template will generate a desktop-width (800px) and mobile-width (480px) view of both the HTML and plain text versions of each email. In addition to making it easy to jump to and review a specific email, it also provides the ability to quickly spot-check all of the emails at once.

<a href="http://assets.wildbit.com/postmark/templates/"><img src="http://assets.wildbit.com/postmark/templates/docs/preview.png"></a>

# Code

In order to maintain a high level of compatibility across email clients, the modules are visually simple, but involve some traditional table hacking. This is a quick list of code samples for quick references. You can see an example of these rendered in the `example.html` template. This template is also the one used for quick visual testing on Litmus.

## Mustachio & Handlebars

Postmark templates use [Mustachio](https://github.com/wildbit/mustachio), our lightweight yet powerful templating engine for C#. However, MailMason uses Handlebars for local development. Since MailMason ultimately generates Mustachio templates for Postmark, the chances are pretty good that you'll want to include some Mustachio variables in your templates. If you don't escape these variables, MailMason will treat them like Handlebars and attempt to parse them.

You can escape values in Handlebars like this:

```
\{{ value }}
```

...and Handlebars will turn that into...

```
{{ value }}
```

...inside of your end result Mustachio templates.

## Basic Markup

All of the following are pre-styled with simple clean and compatible styles.

1. Headings - h1, h2, h3
2. Body text - p, em, strong
3. Links - a
4. Lists - ul, ol, li

## Buttons

A very nice set of cross-client compatible and colored buttons are available and great to use for the primary desired actions of your email.

Colors supported: blue, green, and red. (The precise colors can be tweaked in `/src/stylesheets/scss/_variables.scss`)

```html
<table class="body-action" align="center" width="100%" cellpadding="0" cellspacing="0">
  <tr>
    <td align="center">
      {{> button color="blue" label="Download as PDF" target_url="\{{action_url}}" }}
    </td>
  </tr>
</table>
```