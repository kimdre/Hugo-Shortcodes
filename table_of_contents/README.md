# Table of Contents in Hugo

Add a automatically generated Table of Contents to any Page/Post on your Website 

## Install

1. Add the following to the content container (here it is `post-content`) in your `single.html` before `{{ .Content }}`:

    ```html
    <div class="post-content">
        {{ if .Params.toc }}

        <div class="toc"> 
            <h2>Table Of Contents</h2>
            {{ .Page.TableOfContents }}
        </div>

        {{ end }}

        {{ .Content }}
    </div>
    ```

2. Add the default key/value to your `archetypes/default.md`
   ```yaml
   toc: false # Table of Contents disabled by default
   ```

3. Add to your project config file:
   ```toml
   [markup]
        [markup.tableOfContents]
            startLevel = 2
            endLevel = 5
            ordered = true
   ```

## Usage

```yaml
+++
title = "Simple SSH Pipeline with Drone CI"
tags = ["Tutorial", "Drone-CI", "Docker", "Linux"]
summary = "This Step-by-Step Tutorial will show you how to make a SSH Pipeline with Drone CI."
date = "2021-07-30"
lastmod = "2021-11-15"
draft = false
toc = true # Add 'toc' with a value of true
+++

```

You can also use the shortcode (see in shortcodes subdirectory) to insert a ToC somewhere in a text:
```hugo
{{< toc >}}
```


## Preview

![Highlight Boxes in Hugo](table_of_contents.png)
