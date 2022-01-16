# Search Engine Optimization in Hugo

Add automatically generated Search Engine Optimization to your Website

## Install

1. Add this code to your `<head></head>` structure (e.g in `layouts/_default/baseof.html`):
   
   ```html
   <!-- 
    Site Indexing toggled by key value of `private` in Page/Post Settings 
    404.html and 404.php are noindex, nofollow by default
    -->
    <meta name="robots" content=
    {{- if or (.Params.private) (in (string .Permalink) "404.html") (in (string .Permalink) "404.php") -}}
        "noindex, nofollow"
    {{- else -}}
        "index, follow"
    {{ end }} />

    <!-- Meta Keywords/Tags for Users to search for in Search Engines -->
    <meta name="keywords" content="
    {{- with .Params.tags }}
        {{- range . -}}
            {{ with $.Site.GetPage (printf "/%s/%s" "tags" . ) }}
                {{- .Title -}},
            {{- end }}
            {{- end }}
        {{- else -}}
            Tutorials, Tips, Linux, Bash, Docker
    {{- end }}" />    

    <!-- Canonical URLs -->
    <link rel="canonical" href="{{ .Permalink }}" />
    <link rel="alternate" href="{{ .Permalink }}" hreflang="{{ .Site.LanguageCode }}" />

    <!-- Links to RSS Feed -->
    {{ range .AlternativeOutputFormats -}}
        {{ printf `<link rel="%s" type="%s" href="%s" title="%s" />` .Rel .MediaType.Type .Permalink $.Site.Title | safeHTML }}
    {{ end -}}
   ```

2. Add the default key/value `private = true` to `/archetypes/default.md`
   
   ```yaml
    ---
    title: "{{ replace .Name "-" " " | title }}"
    date: {{ .Date }}
    draft: true

    ## Add this key with value 'false' for indexing by search engines enabled by default
    private: false
    ---
   ```

## Usage

Add these keys and values to any page's settings:


```toml
+++
...
tags = ["fruit", "apple", "health"] # Fitting keywords that describe your post/page
private = true # true if you want it private/unlisted
+++
```

## Preview

### Public

### Example Post

```html
<meta name="keywords" content="Tag1, Tag2, Tag3" />
<meta name="robots" content="index, follow" />
<link rel="canonical" href="http://localhost:1313/" />
<link rel="alternate" href="http://localhost:1313/" hreflang="en-us" />
<link rel="alternate" type="application/rss+xml" href="http://localhost:1313/index.xml" title="Example Blog" />
```

#### Index

```html
<meta name="keywords" content="default-tag1, default-tag2, default-tag3" />
<meta name="robots" content="index, follow" />
<link rel="canonical" href="http://localhost:1313/posts/example-post" />
<link rel="alternate" href="http://localhost:1313/posts/example-post" hreflang="en-us" />
<link rel="alternate" type="application/rss+xml" href="http://localhost:1313/index.xml" title="Example Blog" />
```

### Private

> 404 Page is private by default

```html
<meta name="keywords" content="Tag1, Tag2, Tag3" />
<meta name="robots" content="noindex, nofollow" />
<link rel="canonical" href="http://localhost:1313/404.html" />
<link rel="alternate" href="http://localhost:1313/404.html" hreflang="en-us" />
```