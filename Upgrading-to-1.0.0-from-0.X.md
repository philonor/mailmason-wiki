Upgrading to the latest version can get pretty tricky depending on whether you've customized your workflow. For most projects, it's not as simple as merging the latest MailMason updates and calling it a day. This guide walks you through how to manually integrate your existing MailMason templates into the latest version of the project.

🚨**Attention!** 🚨This guide assumes a few things:
- You have an existing project that uses a previous version of MailMason's workflow
- You are using the default Grunt workflow that shipped with previous versions of MailMason. If you've made a bunch of changes to the tasks or targets in your Gruntfile.js, you will need to improvise.
- You find the latest improvements in the [v1.0.0 release notes](#) useful. If that's a no, then it's not worth upgrading.


***

### 🧱General setup
1. Clone the latest version of MailMason to your desktop. This will serve as the new project for your MailMason templates.
2. From terminal, navigate to the new MailMason project and install the node.js dependencies: 
    ```bash
    cd ~/your-project
    nvm install
    nvm use
    npm install
    ```

3. From your old MailMason folder, copy `config.json` and `secrets.json` to the new project folder

### 🎨Stylesheets

1. From your old MailMason folder, copy `/src/stylesheets` to the new project folder
2. Delete any compiled stylesheet(.css) files in `/src/stylesheets` since they will now be compiled to `/dist/stylesheets`
3. Run `npm run css` to ensure that the stylesheets are being compiled properly

### 📘Layouts
1. From your old MailMason folder, copy the layouts from `/src/layouts` to the new project folder. The folder structure has changed in `1.0`, so be sure to follow the new conventions.
    * Each layout is stored in its own folder. e.g. `/src/layouts/plain/content.hbs`
    * Layout file is named `content.hbs`
    * Layouts must have a `meta.json` file in the same folder so that they can be uploaded to Postmark. The metadata file must follow this structure: 
        ```json
        {
          "Name": "Your layout name",
          "Alias": "your-layout-alias",
          "TemplateType": "Layout"
        }
        ```
2. Now that the compiled CSS is stored in `/dist/stylesheets`, you will need to update the stylesheet path in your layout to use the new relative path. e.g. `../../stylesheets/global.css?__inline=true`

### 📄Templates
1. From your old MailMason folder, copy the templates from `/src/emails` to `/src/templates` in the new project folder. Similar to layouts, the template folder structure has changed in `1.0`. Be sure to follow the new convention. 
    * Each template is stored in its own folder. e.g. `/src/templates/welcome/content.hbs`
    * Template file is named `content.hbs`
    * All templates must have a `meta.json` file in the same folder so that they can be uploaded to Postmark. The metadata file must follow this structure:
        ```json
        {
          "Name": "Your template name",
          "Alias": "your-template-alias",
          "Subject": "Your subject line",
          "TemplateType": "Standard",
          "LayoutTemplate": "your-layout-alias"
        }
        ```
2. Now that the layout folder structure has changed, you will need to update your templates to reference the new layout. Open up your template files and update the layout path found in the YAML front matter.

    ```yaml
    ---
    layout: your-layout/content.hbs
    ---
    ```

### 🧪Testing
1. Ensure that everything is set up properly by running `npm run build`. Check the console output to see if the Grunt tasks are executing properly.
2. Open `~/your-project/previews.html` file in your browser and double-check that the emails look good

***

If you're looking to take advantage of the latest design improvements like custom fonts, dark mode compatibility, or improved accessibility, you will need to use one of the starter layouts that come with MailMason 1.0.0. From there you can add in any brand-specific colors, elements, etc.

Hopefully you found this helpful. If you have any issues or feel like something needs to be clarified, please file a Github issue. 