## Setup

1) Install [node version manager](https://github.com/creationix/nvm)
```bash
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.4/install.sh | bash
```

2) Install and use node version specified from `.nvmrc`.
```bash
nvm install && nvm use
```

3) Install Grunt CLI globally
```bash
npm install -g grunt-cli
```

4) Install local dependencies
```bash
npm install
```

5) Install premailer and nokogiri gems
```bash
gem install premailer
gem install nokogiri
```

## Configuration

There are two primary configuration files for MailMason: `secrets.json` and `config.json`. By default these files are ignored using `.gitignore`. Examples of these files are included at `example_secrets.json` and `example_config.json`. You can copy these files and rename them to create your own. The specific secrets and configurable values are documented within these files.

If you project is shared among team members, you may want to to update your `.gitignore` to recognize `config.json` so that each member of your team isn't forced to recreate it.

### Secrets

By design `secrets.json` is ignored so that it's not accidentally committed. The base project includes an `example_secrets.json` that you can copy and rename in order to create your base secrets file. The relevant secrets are documented in the file.

If you're not sending test emails through Postmark and don't want to upload any images to a CDN, you don't have to provide values for these files. 

### Configuration

By default, `config.json` is ignored. The base project includes an `example_config.json` that you can copy and rename in order to create your base configuration file. The configuration file lets you set a variety of things like product name, sender name, corporate address, and various other strings. Each section and individual option is documented within the `example_config.json` file.

### Images & Assets

Postmark doesn't currently provide hosting for images in templates. (It's on our roadmap, though.) So for the time being, if you'd like your emails to use images, you'll need to host these assets somewhere in order for them to show up. In general, we advise a subdomain of your primary domain for the emails. For instance, if you're sending email from `jane@example.com`, a great URL for the email assets would be `assets.example.com`.

Since images complicate things, they're off by default. If you turn them on, you'll need to upload the relevant images to a publicly available CDN so they can be displayed in the email. To do this, you'll need to provide information for your FTP server within `config.json` and provide the username and password for the FTP server in `secrets.json`. Once that's complete, you'll be able to upload all images from `/src/images` to  the specified directory on your FTP server.

Once that's done, just add the value for the `images_url` within the `config.json` file. That URL will be used throughout to provide absolute references to the image locations.

### Social Images

If you're using images, the templates can include logos and links for relevant social networks in the footer. If you're not using images, there won't be any social network links. In order for the social images to show up, you'll need to set `use_images` to `true` in the configuration file. Then you can provide the full URL for the social networks you use. For every URL you provide, the image and link will automatically be added. If you leave a social network URL blank, it will simply be ignored.

Finally, there are two versions of the social images for the footer. The first version is just the logos. The second version is circles with the logos cut out. There is a `use_circles` option in the config file as well. If you're only using a few social links, the original logos work best. However, if you have quite a few social networks to include, the logos begin to clash, and it looks better to use the circle versions.