## Setup

1) Install [node version manager](https://github.com/creationix/nvm)
```bash
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.4/install.sh | bash
```

2) Install and use node version specified from `.nvmrc`.
```bash
nvm install && nvm use
```

3) Install local dependencies
```bash
npm install
```

4) Install premailer and nokogiri gems
```bash
gem install premailer
gem install nokogiri
```

5) Create and edit `config.json` and `secrets.json` (Secrets are only necessary if you want to send test emails.)

6) Start the build service that watches the `src` directory for changes and builds to `dist`.  
```bash
npm start
```

7) Open `preview.html` in a browser. It provides a normal width and mobile device width view of both the HTML and text versions of each email for easy previewing and scanning.

## Configuration

There are two primary configuration files for MailMason: `secrets.json` and `config.json`. By default these files are ignored using `.gitignore`. Examples of these files are included at `example_secrets.json` and `example_config.json`. You can copy these files and rename them to create your own. The specific secrets and configurable values are documented within these files.

If your project is shared among team members, you may want to to update your `.gitignore` to recognize `config.json` so that each member of your team isn't forced to recreate it.

### Secrets.json

By design `secrets.json` is ignored so that it's not accidentally committed. The base project includes an `example_secrets.json` that you can copy and rename in order to create your base secrets file. The relevant secrets are documented in the file.

If you're not sending test emails through Postmark and don't want to upload any images to a CDN, you don't have to provide values for these files. 

```javascript
// Create a copy of this file as 'secrets.json'

{
  "ftp": {

    // If you want to use images in your emails, you'll need to host them
    // on your own server. There's a grunt task to automatically upload your
    // images to your asset server via FTP. You would just need to provide
    // your username and password here.
    "username": "YOUR_FTP_USERNAME_HERE",
    "password": "YOUR_FTP_PASSWORD_HERE"
  },
  "postmark": {
    
    // If you want a way to send yourself test emails through Postmark
    "server_token": "YOUR_POSTMARK_SERVER_TOKEN_HERE"
  }
}
```

### Config.json

By default, `config.json` is ignored. The base project includes an `example_config.json` that you can copy and rename in order to create your base configuration file. The configuration file lets you set a variety of things like product name, sender name, corporate address, and various other strings. Each section and individual option is documented within the `example_config.json` file.

```javascript
// Create a copy of this file as 'variables.json'

{
  "postmark": {

    // The from address to use to send the email through Postmark
    // Important: Make sure that the Sender Signature has been setup or the 
    //            domain authenticated
    "from": "jane@example.com", 

    // The email address to send your tests to for looking at things manually
    // Note: You don't need to change this for Litmus. The Litmus testing has
    //       its own dedicated email variable below
    "to": "jon@example.com",    

    // Subject for test emails (this can help make it easier to find them)
    "subject": "Test Email"
  },
  "strings": {

    // The name you want to appear in email clients ()
    "sender_name": "[Jane from Acme]",

    // Your product's common name for use throughout the emails
    "product_name": "[Acme]",     

    // Your product's home page for the logo to link to
    "product_url": "https://example.com", 

    // The name of your company as it will appear on credit card statements
    "credit_card_statement_name": "[Acme Affiliate Corporation, LLC]",

    // The name of your company as it would appear in the footer of your emails
    "formal_company_name": "[Acme, LLC]",              

    // For your company's address (optional)
    "address_line_1": "1234 Street Rd.",
    "address_line_2": "Suite 1234",
    "city": "Cityville",
    "state": "ST",
    "country": "United States",

    // Your company's phone number (optional)
    "phone": "123-456-7890",

    // This is your Litmus test addres for your team to email tests to Litmus
    "litmus_email": "something@litmus.com"
  },
  "images": {

    // True if you want to use images, false if you don't.
    // If you disallow images, the masthead will just use the product name
    // in large bold text
    "use_images": false,

    // If you use images in you remails, you'll need to host the images
    // somewhere. Adding image hosting to Postmark templates is on the roadmap,
    // but it's not ready yet. So this is the fully qualified URL where the 
    // emails can find the images
    "images_url": "https://example.com/example/images/",

    // The file name for the logo you'd like to display in the header
    "logo_file": "logo.png",

    // The width of the logo in the header
    "logo_width": "186",

    // By default, the social media icons will display the standard logos, but
    // you can set this to true to use circle versions with the logos cut out.
    // Generally, circles look best if you have a lot of social links, but 
    // standard logos look better if you only have a few. Try both and see 
    // which one you like best. :)
    "use_social_circles": false,

    // The URLs for the relevant social profiles. If you don't have one or don't
    // want to include it, just leave it blank.
    "twitter_url": "",
    "facebook_url": "",
    "pinterest_url": "",
    "instagram_url": "",
    "google_plus_url": "",
    "youtube_url": "",
    "linkedin_url": "",
    "dribbble_url": ""
  },

  // If you want to use images in your emails, you'll need to host them on your
  // own server. There's a grunt task to automatically upload your images to 
  // your asset server via FTP. You would just need to provide your connection
  // information here.
  "ftp": {

    // Make sure to set this to your IP or domain for your image asset server
    "host": "12.34.56.79",

    // You're most likely using port 21 for FTP
    "port": "21",

    // The local directory from which you want to copy files
    "src": "src/images",        

    // The target directory where the files should be uplaoded on your asset
    // server
    "dest": "/example/images"   
  }  
}
```

### Images & Assets

Postmark doesn't currently provide hosting for images in templates. (It's on our roadmap, though.) So for the time being, if you'd like your emails to use images, you'll need to host these assets somewhere in order for them to show up. In general, we advise a subdomain of your primary domain for the emails. For instance, if you're sending email from `jane@example.com`, a great URL for the email assets would be `assets.example.com`.

Since images complicate things, they're off by default. If you turn them on, you'll need to upload the relevant images to a publicly available CDN so they can be displayed in the email. To do this, you'll need to provide information for your FTP server or Amazon S3 bucket.

To upload your assets to an **FTP server**, add your server details within `config.json` and provide the username and password for the FTP server in `secrets.json`. Once that's complete, you'll be able to upload all images from `/src/images` to  the specified directory on your FTP server.

Alternatively, you can upload your images to an **Amazon S3** bucket. You'll need to add your Access Key ID and Secret Access Key to the `secrets.json` file. Once that's sorted, go ahead and add your bucket name and region to the `config.json` file.

To finish up, just add the value for the `images_url` within the `config.json` file. That URL will be used throughout to provide absolute references to the image locations.

### Social Images

If you're using images, the templates can include logos and links for relevant social networks in the footer. If you're not using images, there won't be any social network links. In order for the social images to show up, you'll need to set `use_images` to `true` in the configuration file. Then you can provide the full URL for the social networks you use. For every URL you provide, the image and link will automatically be added. If you leave a social network URL blank, it will simply be ignored.

Finally, there are two versions of the social images for the footer. The first version is just the logos. The second version is circles with the logos cut out. There is a `use_circles` option in the config file as well. If you're only using a few social links, the original logos work best. However, if you have quite a few social networks to include, the logos begin to clash, and it looks better to use the circle versions.

<img src="http://assets.wildbit.com/postmark/templates/docs/social_icons.png">

Since the images have to be generated in advance, there's a limit to the social networks with built-in support. Right now, the following social networks are available:

* Twitter
* Facebook
* Pinterest
* Instagram
* dribbble
* Google+
* YouTube
* LinkedIn