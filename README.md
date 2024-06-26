## Credits

This website theme is based on the Hugo framework which is made with the templates [PaperMod](https://github.com/adityatelange/hugo-PaperMod) and [hugo-paper](https://github.com/nanxiaobei/hugo-paper). \
Design from charlola:
[LinkedIn](https://www.linkedin.com/in/heycharlola/) &
[GitHub](https://github.com/charlola/hugo-theme-charlolamode) 

## Quick Start

1. Install [Hugo](https://gohugo.io/installation/)
2. Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)


**Open your terminal or command line**

1. Create a new folder 'quickstart'

```console
hugo new site quickstart
```

2. Go into this folder 
```console
cd quickstart
```

3. Initialize an empty Git repository in the current directory
```console
git init
```

4. Clone this repository into your folder
```console
git submodule add https://github.com/charlola/hugo-theme-charlolamode.git themes/charlolamode
```

5. Delete the config.toml
```console
rm config.toml
```

6. Add theme in a new config.yml file
```console
echo "theme: charlolamode" >> config.yml
```

7. Start Hugo's development server to view the site locally.
```console
hugo server
```

Once the local server starts, you can see your site. If your webbrowser does not automatically pop up, open your browser and enter http://localhost:1313. Now you can start to modify this page in the directory. If you save new changes, this site will automatically refresh and render the modification.


## Open Visual Studio Code to edit your Blog

3. Open your favorite Editor like [Visual Studio Code](https://code.visualstudio.com/download)
### Basic Configuration

The config.yml is your best friend. You can modify and add information, such as ...
- Title of the page
- Your Name
- Description
- Social Icons
- Buttons

Have a look at the charlolamode/config.yml for reference. There are commented examples which show you how to easily add tabs and social icons like LinkedIn, Twitter, Youtube, Instagram. Copy the content in your config.yml which will overwrite the config.yml of the theme. 

### Change Profile Image

To add your profile pic, replace ***profile.png*** in the folder ***static/images***. Make sure you take an image with a happy face :)

### Add tabs

In the config.yml you can add new tabs next to 'Articles' and 'Contact'. Uncomment 'Category' to check it out.

***Note***
If you add a new tab in the config.yml, you have to do the following:
1. Add new folder in the directory 'content' with the ***same name*** as the new tab.
2. Copy ***_index.md*** from articles into new folder.

### Add new content

If you like to push new content, create a new Markdown file in the new folder. Find an example in ***content/articles/article.md***.


### Change colors

Have a look at assets/css/core/theme-vars.css to play around with colors.

### Disable 'Profile Mode'

To display Article content on the home page, rather than profile information, set the following under params: in ***config.yml***
```
profileMode: 
    enabled: false
```

With the Article content moved to the home page, removing the main menu entry for ***Articles*** may be desirable:
```
menu:
    main:
        - name: Contact
          url: contact/
          weight: 30
        # - name: Articles
        #   url: articles/
        #   weight: 20
        - name: Projects
          url: projects
          weight: 15
```

### Publish Online Website via GitHub Pages

To push your website online, refer to this [blog](https://gohugo.io/hosting-and-deployment/hosting-on-github/) to deploy the Hugo site via GitHub pages.

### Add images to content:

In the blog - add the following block of code in the .md file of an article/blog to display an image in the blog.

```{{< figure src="/images/myimage.png" title="" >}}```

In the preview of a blog - add the following in the metadata section of a markdown file and ensure that the image location correct and accessible. Else, the image won't load.

```image: images/myimage.jpg```

Note: In this case, a sub folder with the name "images" was created in the articles folder.

Note: Update the image path as per your requirement.

### Add fonts to the site

- Update the layouts/partials/header.html file and add the following code at the top:
```
<head>
    <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Font_Name">
    {{ template "_internal/google_analytics.html" . }}
</head>

```
Note: Add the desired font in the place of "Font_Name"

- Add the desired Google font in the file assets/css/core/reset.css and comment out the original font-family line.
```
font-family: '<Font_Name>', sans-serif;
```

### Fix the date formatting and spacing in HTML by adding the following in themes/charlolamode/layouts/partials/post_meta.html:

```
{{- with ($scratch.Get "meta") }}
  {{- delimit . "&nbsp;·&nbsp;" | safeHTML -}}
{{- end -}}

```

Note - replace the delimit block with the block of code shown above.

### Old config.yml file content

```theme: charlolamode```

### Issues encountered

- A browser tab showed the website URL instead of the author name. Fix this issue by adding ```<title>Author Name</title>``` as the first line in themes/charlolamode/layouts/partials/head.html. The issue with this is it sets the author name as the site name for all website pages. Ensure that the .yml file is updated correctly to ensure that the website pages load correctly.

