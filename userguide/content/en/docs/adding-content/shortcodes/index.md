---
title: Docsy Shortcodes
linkTitle: Shortcodes
date: 2017-01-05
weight: 5
description: Use Docsy's Hugo shortcodes to quickly build site pages.
resources:
  - src: '**spruce*.jpg'
    params:
      byline: '*Photo*: Bjørn Erik Pedersen / CC-BY-SA'
params:
  message: Some _message_.
cSpell:ignore: imgproc pageinfo Bjørn Pedersen
---

Rather than writing all your site pages from scratch, Hugo lets you define and
use [shortcodes](https://gohugo.io/content-management/shortcodes/). These are
reusable snippets of content that you can include in your pages, often using
HTML to create effects that are difficult or impossible to do in simple
Markdown. Shortcodes can also have parameters that let you, for example, add
your own text to a fancy shortcode text box. As well as Hugo's
[built-in shortcodes](https://gohugo.io/content-management/shortcodes/), Docsy
provides some shortcodes of its own to help you build your pages.

## Shortcode delimiters

As illustrated below, using the bracket styled [shortcode delimiter][],
`{{</*...*/>}}`, tells Hugo that the inner content is HTML/plain text and needs
no further processing. By using the delimiter `{{%/*...*/%}}`, Hugo will treat
the shortcode body as Markdown. You can use both styles in your pages.

## Shortcode blocks

The theme comes with a set of custom **Page Block** shortcodes that can be used
to compose landing pages, about pages, and similar.

These blocks share some common parameters:

- **height**: A pre-defined height of the block container. One of `min`, `med`,
  `max`, `full`, or `auto`. Setting it to `full` will fill the Viewport Height,
  which can be useful for landing pages.
- **color**: The block will be assigned a color from the theme palette if not
  provided, but you can set your own if needed. You can use all of Bootstrap's
  color names, theme color names or a grayscale shade. Some examples would be
  `primary`, `white`, `dark`, `warning`, `light`, `success`, `300`, `blue`,
  `orange`. This will become the **background color** of the block, but text
  colors will adapt to get proper contrast.

### blocks/cover

The **blocks/cover** shortcode creates a landing page type of block that fills
the top of the page.

```html
{{</* blocks/cover title="Welcome!" image_anchor="center" height="full" color="primary" */>}}
<div class="mx-auto">
	<a class="btn btn-lg btn-primary me-3 mb-4" href="{{</* relref "/docs" */>}}">
		Learn More <i class="fa-solid fa-circle-right ms-2"></i>
	</a>
	<a class="btn btn-lg btn-secondary me-3 mb-4" href="https://example.org">
		Download <i class="fa-brands fa-github ms-2"></i>
	</a>
	<p class="lead mt-5">This program is now available in <a href="#">AppStore!</a></p>
	<div class="mx-auto mt-5">
		{{</* blocks/link-down color="info" */>}}
	</div>
</div>
{{</* /blocks/cover */>}}
```

Note that the relevant shortcode parameters above will have sensible defaults,
but is included here for completeness.

| Parameter    | Default                        | Description                           |
| ------------ | ------------------------------ | ------------------------------------- |
| title        |                                | The main display title for the block. |
| image_anchor |                                |
| height       |                                | See above.                            |
| color        |                                | See above.                            |
| byline       | Byline text on featured image. |

To set the background image, place an image with the word "background" in the
name in the page's [Page Bundle](/docs/adding-content/content/#page-bundles).
For example, in our the example site the background image in the home page's
cover block is
[`featured-background.jpg`](https://github.com/google/docsy-example/tree/main/content/en),
in the same directory.

{{% alert title="Tip" %}} If you also include the word **featured** in the image
name, e.g. `my-featured-background.jpg`, it will also be used as the Twitter
Card image when shared. {{% /alert %}}

For available icons, see
[Font Awesome](https://fontawesome.com/icons?d=gallery&m=free).

### blocks/lead

The **blocks/lead** block shortcode is a simple lead/title block with centred
text and an arrow down pointing to the next section.

```go-html-template
{{%/* blocks/lead color="dark" */%}}
TechOS is the OS of the future.

Runs on **bare metal** in the **cloud**!
{{%/* /blocks/lead */%}}
```

| Parameter | Default  | Description                               |
| --------- | -------- | ----------------------------------------- |
| height    | `auto`   | See [Shortcode blocks](#shortcode-blocks) |
| color     | .Ordinal | See [Shortcode blocks](#shortcode-blocks) |

### blocks/section

The **blocks/section** shortcode is meant as a general-purpose content
container. It comes in two "flavors", one for general content and one with
styling more suitable for wrapping a horizontal row of feature sections.

The example below shows a section wrapping 3 feature sections.

```go-html-template
{{</* blocks/section color="dark" type="row" */>}}
{{%/* blocks/feature icon="fa-lightbulb" title="Fastest OS **on the planet**!" */%}}
The new **TechOS** operating system is an open source project. It is a new project, but with grand ambitions.
Please follow this space for updates!
{{%/* /blocks/feature */%}}
{{%/* blocks/feature icon="fa-brands fa-github" title="Contributions welcome!" url="https://github.com/gohugoio/hugo" */%}}
We do a [Pull Request](https://github.com/gohugoio/hugo/pulls) contributions workflow on **GitHub**. New users are always welcome!
{{%/* /blocks/feature */%}}
{{%/* blocks/feature icon="fa-brands fa-x-twitter" title="Follow us on Twitter!" url="https://twitter.com/GoHugoIO" */%}}
For announcement of latest features etc.
{{%/* /blocks/feature */%}}
{{</* /blocks/section */>}}
```

| Parameter | Default | Description                                                                                                                                          |
| --------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| `height`  |         | See above.                                                                                                                                           |
| `color`   |         | See above.                                                                                                                                           |
| `type`    |         | Specify "container" (the default) if you want a general container, or "row" if the section will contain columns -- which must be immediate children. |

### blocks/feature

```go-html-template
{{%/* blocks/feature icon="fa-brands fa-github" title="Contributions welcome!" url="https://github.com/gohugoio/hugo" */%}}
We do a [Pull Request](https://github.com/gohugoio/hugo/pulls) contributions workflow on **GitHub**. New users are always welcome!
{{%/* /blocks/feature */%}}
```

| Parameter | Default                                                                                                                                                  | Description            |
| --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| title     |                                                                                                                                                          | The title to use.      |
| url       |                                                                                                                                                          | The URL to link to.    |
| url_text  | The [language parameter](/docs/language/#internationalization-bundles) value of [`ui_read_more`](https://github.com/google/docsy/blob/main/i18n/en.toml) | The link text to use.  |
| icon      |                                                                                                                                                          | The icon class to use. |

### blocks/link-down

The **blocks/link-down** shortcode creates a navigation link down to the next
section. It's meant to be used in combination with the other blocks shortcodes.

```go-html-template
<div class="mx-auto mt-5">
	{{</* blocks/link-down color="info" */>}}
</div>
```

| Parameter | Default | Description |
| --------- | ------- | ----------- |
| color     | info    | See above.  |

## Shortcode helpers

### alert

Use the **alert** shortcode to display notices and warnings. The shortcode
renders a [Bootstrap alert component][bs-alert]. It can be used with Markdown
content and contain other shortcodes. For example:

```go-template
{{%/* alert title="Welcome" */%}} **Hello**, world! {{%/* /alert */%}}
```

Renders as:

{{% alert title="Welcome" %}} **Hello**, world! {{% /alert %}}

Parameters:

- `title` (optional): Use this to specify a title for your alert. The title
  renders as a Bootstrap [alert heading][bs-alert], at heading level 4, using
  the `h4` Bootstrap class over a `<div>` element. This prevents the title from
  appearing in a page's table of contents.
- `color` (optional): Use this parameter to specify one of Bootstrap's
  predefined [alert variants][bs-alert], each of which has their own color.
  These include `primary`, `info`, and `warning`.

#### Alerts and indentation

When the `alert` shortcode is used in a Markdown context that requires
indentation, such as a list, then the alert _content_ (whether specified as
text/Markdown or a shortcode) must be indented accordingly. For example:

```go-template
- The following note is part of this list item:
  {{%/* alert title="Celebrate!" color=success */%}}
  This alert content is properly rendered.

  > {{%/* param message */%}}
  {{%/* /alert */%}}
  The first list item continues.

- **Don't put content on the same line** as the opening tag, it breaks rendering:
  {{%/* alert title="Misformed alert!" color=warning */%}} **This content appears outside of
  the list!** {{%/* /alert */%}}
```

This renders as:

{{< comment >}}

<!--
IMPORTANT: the following lone opening div tag prevents the mis-formatted alert example below from breaking all the rest of the page. DO NOT remove it.
-->

{{< /comment >}}

<div class="td-max-width-on-larger-screens">

<!-- prettier-ignore -->
- The following note is part of this list item:
  {{% alert title="Celebrate!" color=success %}}
  This alert content is properly rendered.

  > {{% param message %}}
  {{% /alert %}}
  The first list item continues.

- **Don't put content on the same line** as the opening tag, it breaks rendering:
  {{% alert title="Misformed alert!" color=warning %}} **This alert content appears outside of
  the list!** {{% /alert %}}

[bs-alert]: https://getbootstrap.com/docs/5.3/components/alerts/

### pageinfo

The **pageinfo** shortcode creates a text box that you can use to add banner
information for a page: for example, letting users know that the page contains
placeholder content, that the content is deprecated, or that it documents a beta
feature.

```go-template
{{%/* pageinfo color="info" */%}}
This is placeholder content.
{{%/* /pageinfo */%}}
```

Renders to:

{{% pageinfo color="info" %}}

This is placeholder content

{{% /pageinfo %}}

| Parameter | Default | Description                                                   |
| --------- | ------- | ------------------------------------------------------------- |
| color     | primary | One of the theme colors, eg `primary`, `info`, `warning` etc. |

### imgproc

The **imgproc** shortcode finds an image in the current
[Page Bundle](/docs/adding-content/content/#page-bundles) and scales it given a
set of processing instructions.

```go-template
{{%/* imgproc spruce Fill "400x450" */%}}
Norway Spruce *Picea abies* shoot with foliage buds.
{{%/* /imgproc */%}}
```

Use the syntax above if the inner content and/or the `byline` parameter of your
shortcode is authored in markdown. In case of HTML content, use `<>` as
innermost delimiters: `{{</* imgproc >}}<b>HTML</b> content{{< /imgproc */>}}`.

{{% imgproc spruce Fill "400x450" %}} Norway Spruce _Picea abies_ shoot with
foliage buds. {{% /imgproc %}}

The example above has also a byline with photo attribution added. When using
illustrations with a free license from
[WikiMedia](https://commons.wikimedia.org/) and similar, you will in most
situations need a way to attribute the author or licensor. You can add metadata
to your page resources in the page front matter. The `byline` param is used by
convention in this theme:

<!-- prettier-ignore-start -->
{{< tabpane >}}
{{< tab header="Front matter:" disabled=true />}}
{{< tab header="toml" lang="toml" >}}
+++
[[resources]]
src = "**spruce*.jpg"

  [resources.params]
  byline = "*Photo*: Bjørn Erik Pedersen / CC-BY-SA"
+++
{{< /tab >}}
{{< tab header="yaml" lang="yaml" >}}
---
resources:
- src: "**spruce*.jpg"
  params:
    byline: "*Photo*: Bjørn Erik Pedersen / CC-BY-SA"
---
{{< /tab >}}
{{< tab header="json" lang="json" >}}
{
  "resources": [
    {
      "src": "**spruce*.jpg",
      "params": {
        "byline": "*Photo*: Bjørn Erik Pedersen / CC-BY-SA"
      }
    }
  ]
}
{{< /tab >}}
{{< /tabpane >}}
<!-- prettier-ignore-end -->

| Parameter | Description                                                                                                                                                         |
| --------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|         1 | The image filename or enough of it to identify it (we do Glob matching)                                                                                             |
|         2 | Command. One of `Fit`, `Resize`, `Fill` or `Crop`. See [Image Processing Methods](https://gohugo.io/content-management/image-processing/#image-processing-methods). |
|         3 | Processing options, e.g. `400x450 r180`. See [Image Processing Options](https://gohugo.io/content-management/image-processing/#image-processing-options).           |

### swaggerui

You can place the `swaggerui` shortcode anywhere inside a page with the
[`swagger` layout](https://github.com/google/docsy/tree/main/layouts/swagger);
it renders [Swagger UI](https://swagger.io/tools/swagger-ui/) using any OpenAPI
YAML or JSON file as source. This file can be hosted anywhere you like, for
example in your site's root
[`/static` folder](/docs/adding-content/content/#adding-static-content).

<!-- prettier-ignore-start -->
{{< tabpane >}}
{{< tab header="Front matter:" disabled=true />}}
{{< tab header="toml" lang="toml" >}}
+++
title = "Pet Store API"
type = "swagger"
weight = 1
description = "Reference for the Pet Store API"
+++

{{</* swaggerui src="/openapi/petstore.yaml" */>}}
{{< /tab >}}
{{< tab header="yaml" lang="yaml" >}}
---
title: "Pet Store API"
type: swagger
weight: 1
description: Reference for the Pet Store API
---

{{</* swaggerui src="/openapi/petstore.yaml" */>}}
{{< /tab >}}
{{< tab header="json" lang="json" >}}
{
  "title": "Pet Store API",
  "type": "swagger",
  "weight": 1,
  "description": "Reference for the Pet Store API"
}

{{</* swaggerui src="/openapi/petstore.yaml" */>}}
{{< /tab >}}
{{< /tabpane >}}
<!-- prettier-ignore-end -->

You can customize Swagger UI's look and feel by overriding Swagger's CSS in
`themes/docsy/assets/scss/_swagger.scss`.

{{% alert title="Warning" color="warning" %}} This shortcode relies on
JavaScript libraries hosted on unpkg. Make sure that you can access unpkg from
your network when building or loading your site. {{% /alert %}}

### redoc

The `redoc` shortcode uses the open-source
[Redoc](https://github.com/Redocly/redoc) tool to render reference API
documentation from an OpenAPI YAML or JSON file. This can be hosted anywhere you
like, for example in your site's root
[`/static` folder](/docs/adding-content/content/#adding-static-content), but you
can use a URL as well, for example:

```yaml
---
title: 'Pet Store API'
type: docs
weight: 1
description: Reference for the Pet Store API
---
{
  {
    </* redoc
    "https://raw.githubusercontent.com/OAI/OpenAPI-Specification/main/examples/v2.0/yaml/petstore.yaml"
    */>,
  },
}
```

### iframe

With this shortcode you can embed external content into a Docsy page as an
inline frame (`iframe`) - see: https://www.w3schools.com/tags/tag_iframe.asp

| Parameter     | Default                                                                                               | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| ------------- | ----------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| src           |                                                                                                       | URL of external content                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| width         | 100%                                                                                                  | Width of iframe                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| tryautoheight | true                                                                                                  | If true the shortcode tries to calculate the needed height for the embedded content using JavaScript, see [details](https://stackoverflow.com/questions/9162933?no-link-check). This is only possible if the embedded content is [on the same domain](https://stackoverflow.com/questions/22086722/resize-cross-domain-iframe-height?no-link-check). Note that even if the embedded content is on the same domain, it depends on the structure of the content if the height can be calculated correctly. |
| style         | min-height:98vh; border:none;                                                                         | CSS styles for the iframe. `min-height:98vh;` is a backup if `tryautoheight` doesn't work. `border:none;` removes the border from the iframe - this is useful if you want the embedded content to look more like internal content from your page.                                                                                                                                                                                                                                                        |
| sandbox       | false                                                                                                 | You can switch the sandbox completely on by setting `sandbox = true` or allow specific functionality with the common values for the iframe parameter `sandbox` defined in the [HTML standard](https://www.w3schools.com/tags/att_iframe_sandbox.asp).                                                                                                                                                                                                                                                    |
| name          | iframe-name                                                                                           | Specify the [name of the iframe](https://www.w3schools.com/tags/att_iframe_name.asp).                                                                                                                                                                                                                                                                                                                                                                                                                    |
| id            | iframe-id                                                                                             | Sets the ID of the iframe.                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| class         |                                                                                                       | Optional parameter to set the classes of the iframe.                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| sub           | Your browser cannot display embedded frames. You can access the embedded page via the following link: | The text displayed (in addition to the embedded URL) if the user's browser can't display embedded frames.                                                                                                                                                                                                                                                                                                                                                                                                |

{{% alert title="Warning" color="warning" %}} You can only embed external
content from a server when its `X-Frame-Options` is not set or if it
specifically allows embedding for your site. See
https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options for
details.

There are several tools you can use to check if a website can be embedded via
iframe - e.g.: https://gf.dev/x-frame-options-test. Be aware that when this test
says "Couldn’t find the X-Frame-Options header in the response headers." you
**CAN** embed it, but when the test says "Great! X-Frame-Options header was
found in the HTTP response headers as highlighted below.", you **CANNOT** -
unless it has been explicitly enabled for your site. {{% /alert %}}

### comment

Use the `comment` shortcode to add internal notes or comment out large blocks of Markdown or HTML that won't be rendered on the page.

```go-template
{{< comment >}}
This comment will not be visible in the rendered page.
{{< /comment >}}
```

## Tabbed panes

Sometimes it's very useful to have tabbed panes when authoring content. One
common use-case is to show multiple syntax highlighted code blocks that showcase
the same problem, and how to solve it in different programming languages. As an
example, the tabbed pane below shows the language-specific variants of the
famous `Hello world!` program one usually writes first when learning a new
programming language:

<!-- prettier-ignore-start -->
{{< tabpane langEqualsHeader=true >}}
{{< tab "C" >}}
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
  puts("Hello World!");
  return EXIT_SUCCESS;
}
{{< /tab >}}
{{< tab "C++" >}}
#include <iostream>

int main()
{
  std::cout << "Hello World!" << std::endl;
}
{{< /tab >}}
{{< tab "Go" >}}
package main
import "fmt"
func main() {
  fmt.Printf("Hello World!\n")
}
{{< /tab >}}
{{< tab "Java" >}}
class HelloWorld {
  static public void main( String args[] ) {
    System.out.println( "Hello World!" );
  }
}
{{< /tab >}}
{{< tab "Kotlin" >}}
fun main(args : Array<String>) {
    println("Hello, world!")
}
{{< /tab >}}
{{< tab "Lua" >}}
print "Hello world"
{{< /tab >}}
{{< tab PHP >}}
<?php
echo 'Hello World!';
?>
{{< /tab >}}
{{< tab "Python" >}}
print("Hello World!")
{{< /tab >}}
{{< tab "Ruby" >}}
puts "Hello World!"
{{< /tab >}}
{{< tab header="Scala" >}}
object HelloWorld extends App {
  println("Hello world!")
}
{{< /tab >}}
{{< /tabpane >}}
<!-- prettier-ignore-end -->

The Docsy template provides two shortcodes `tabpane` and `tab` that let you
easily create tabbed panes. To see how to use them, have a look at the following
code block, which renders to a right aligned pane with one disabled and three
active tabs:

```go-html-template
{{</* tabpane text=true right=true */>}}
  {{%/* tab header="**Languages**:" disabled=true /*/%}}
  {{%/* tab header="English" lang="en" */%}}
  ![Flag United Kingdom](flags/uk.png)
  Welcome!
  {{%/* /tab */%}}
  {{</* tab header="German" lang="de" */>}}
    <b>Herzlich willkommen!</b>
    <img src="flags/de.png" alt="Flag Germany" style="float: right; padding: 0 0 0 0px">
  {{</* /tab */>}}
  {{%/* tab header="Swahili" lang="sw" */%}}
  ![Flag Tanzania](flags/tz.png)
  **Karibu sana!**
  {{%/* /tab */%}}
{{</* /tabpane */>}}
```

This code translates to the right aligned tabbed pane below, showing a
`Welcome!` greeting in English, German or Swahili:

<!-- prettier-ignore-start -->
{{< tabpane text=true right=true >}}
  {{% tab header="**Languages**:" disabled=true /%}}
  {{% tab header="English" lang="en" %}}
  ![Flag United Kingdom](flags/uk.png)
  **Welcome!**
  {{% /tab %}}
  {{< tab header="German" lang="de" >}}
    <b>Herzlich willkommen!</b>
    <img src="flags/de.png" alt="Flag Germany" style="float: right; padding: 0 0 0 0px">
  {{< /tab >}}
  {{% tab header="Swahili" lang="sw" %}}
  ![Flag Tanzania](flags/tz.png)
  **Karibu sana!**
  {{% /tab %}}
{{< /tabpane >}}
<!-- prettier-ignore-end -->

### Shortcode details

Tabbed panes are implemented using two shortcodes: `tabpane` containing two or
more nested `tab`s.

#### `tabpane`

The `tabpane` shortcode, which is the container element for the tabs, supports
the following named parameters, all of which are optional:

- **`lang`**: the default code-block language to use for all contained tabs
- **`highlight`**: parameter passed on to the code-block [highlight] function,
  as described below
- **`langEqualsHeader`**: set to `true` when header text matches the tab
  language.
- **`persist`**: one of `header`, `lang`, or `disabled`
- **`persistLang`**: deprecated, use `persist` instead
- **`right`**: set to `true` if you want right-aligned tabs
- **`text`**: set to `true` if the content of all contained tabs are text.
  Default is `false` and assumes the content is code.

The value of the optional parameters `lang` and `highlight` are passed on as
second `LANG` and third `OPTIONS` arguments to Hugo's built-in [highlight]
function, which is used to render the code blocks of the individual tabs.

Tab selection is persisted by default. When unspecified, `persist` defaults to
`header` when `text=true` or `lang` is set; otherwise `persist` defaults to
`lang`. To disable tab persistence, set `persist=disable`.

[highlight]: https://gohugo.io/functions/highlight/

#### `tab`

The `tab` shortcode represent the tabs you want to show. It supports the
following named parameters, all of which are optional:

- **`header`**: defines the tab's header text. When omitted it defaults to text
  of the form "Tab _n_". You can omit the parameter name if it is the only tab
  parameter:
  ```
  {{</* tab "My tab header" */>}} … {{</* /tab */>}}
  ```
- **`lang`**: code-block language for code tabs
- **`highlight`**: parameter passed on to the code-block [highlight] function
- **`right`**: set to `true` in order to split tab panes into a left aligned and
  a right aligned tab groups. Specify `right=true` in the dividing tab. By using
  `right=true` more than once, you can even render multiple tab groups.
- **`disabled`**: set to `true` to disable a tab.
- **`text`**: set to `true` for text tabs. By default tabs are assumed to
  contain code.

For enabled tabs, there are two modes for content display, `code` representation
and _textual_ representation:

- By default, the tab's content is rendered as a code block. In order to get
  proper syntax highlighting, specify the named parameter `lang` --and
  optionally the parameter `highlight`-- for each tab. Parameters set in the
  parent `tabpane` shortcode will be overwritten.
- If the contents of your tabs should be rendered as text with different styles
  and optional images, specify `text=true` as parameter of your `tab`:

> **Reminder**: If your content is markdown, use the percent sign `%` as
> delimiter for your `tab` shortcode, like this:
>
> ```
> {{%/* tab */%}} Your \*\*markdown\*\* content {{%/* /tab */%}}
> ```

## Card panes

When authoring content, it's sometimes very useful to put similar text blocks or
code fragments on card like elements, which can be optionally presented side by
side. Let's showcase this feature with the following sample card group which
shows the first four Presidents of the United States:

{{% cardpane %}}
{{% card header="**George Washington**" title="\*1732 &nbsp;&nbsp;&nbsp; †1799" subtitle="**President:** 1789 – 1797" footer="![SignatureGeorgeWashington](https://upload.wikimedia.org/wikipedia/commons/thumb/2/2e/George_Washington_signature.svg/320px-George_Washington_signature.svg.png 'Signature George Washington')" %}}
![PortraitGeorgeWashington](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b6/Gilbert_Stuart_Williamstown_Portrait_of_George_Washington.jpg/633px-Gilbert_Stuart_Williamstown_Portrait_of_George_Washington.jpg 'Portrait George Washington')
{{% /card %}}
{{% card header="**John Adams**" title="\* 1735 &nbsp;&nbsp;&nbsp; † 1826" subtitle="**President:** 1797 – 1801" footer="![SignatureJohnAdams](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e8/John_Adams_Sig_2.svg/320px-John_Adams_Sig_2.svg.png 'Signature John Adams')" %}}
![PortraitJohnAdams](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Gilbert_Stuart%2C_John_Adams%2C_c._1800-1815%2C_NGA_42933.jpg/633px-Gilbert_Stuart%2C_John_Adams%2C_c._1800-1815%2C_NGA_42933.jpg 'Portrait John Adams')
{{% /card %}}
{{% card header="**Thomas Jefferson**" title="\* 1743 &nbsp;&nbsp;&nbsp; † 1826" subtitle="**President:** 1801 – 1809" footer="![SignatureThomasJefferson](https://upload.wikimedia.org/wikipedia/commons/thumb/0/0d/Thomas_Jefferson_Signature.svg/320px-Thomas_Jefferson_Signature.svg.png 'Signature Thomas Jefferson')" %}}
![PortraitThomasJefferson](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b1/Official_Presidential_portrait_of_Thomas_Jefferson_%28by_Rembrandt_Peale%2C_1800%29%28cropped%29.jpg/390px-Official_Presidential_portrait_of_Thomas_Jefferson_%28by_Rembrandt_Peale%2C_1800%29%28cropped%29.jpg 'Portrait Thomas Jefferson')
{{% /card %}}
{{% card header="**James Madison**" title="\* 1751 &nbsp;&nbsp;&nbsp; † 1836" subtitle="**President:** 1809 – 1817" footer="![SignatureJamesMadison](https://upload.wikimedia.org/wikipedia/commons/thumb/3/39/James_Madison_sig.svg/320px-James_Madison_sig.svg.png 'Signature James Madison')" %}}
![PortraitJamesMadison](https://upload.wikimedia.org/wikipedia/commons/thumb/2/20/James_Madison%28cropped%29%28c%29.jpg/393px-James_Madison%28cropped%29%28c%29.jpg 'Portrait James Madison')
{{% /card %}} {{% /cardpane %}}

Docsy supports creating such card panes via different shortcodes:

- The `cardpane` shortcode which is the container element for the various cards
  to be presented.
- The `card` shortcodes, with each shortcode representing an individual card.
  While cards are often presented inside a card group, a single card may stand
  on its own, too. A `card` shortcode can hold programming code, text, images or
  any other arbitrary kind of markdown or HTML markup as content. In case of
  programming code, cards provide automatic code-highlighting and other optional
  features like line numbers, highlighting of certain lines, ….

### Shortcode `card`: textual content

Make use of the `card` shortcode to display a card. The following code sample
demonstrates how to code a card element:

```go-html-template
{{</* card header="**Imagine**" title="Artist and songwriter: John Lennon" subtitle="Co-writer: Yoko Ono"
          footer="![SignatureJohnLennon](https://server.tld/…/signature.png 'Signature John Lennon')"*/>}}
Imagine there's no heaven, It's easy if you try<br/>
No hell below us, above us only sky<br/>
Imagine all the people living for today…

…
{{</* /card */>}}
```

This code translates to the left card shown below, showing the lyrics of John
Lennon's famous song `Imagine`. A second explanatory card element to the right
indicates and explains the individual components of a card:

{{% cardpane %}}
{{< card header="**Imagine**" title="Artist and songwriter: John Lennon" subtitle="Co-writer: Yoko Ono" footer="![SignatureJohnLennon](https://upload.wikimedia.org/wikipedia/commons/thumb/5/51/Firma_de_John_Lennon.svg/320px-Firma_de_John_Lennon.svg.png 'Signature John Lennon')" >}}
Imagine there's no heaven, It's easy if you try<br/> No hell below us, above us
only sky<br/> Imagine all the people living for today…

Imagine there's no countries, it isn't hard to do<br/> Nothing to kill or die
for, and no religion too<br/> Imagine all the people living life in peace…

Imagine no possessions, I wonder if you can<br/> No need for greed or hunger - a
brotherhood of man<br/> Imagine all the people sharing all the world…

You may say I'm a dreamer, but I'm not the only one<br/> I hope someday you'll
join us and the world will live as one {{< /card >}}
{{% card header="**Header**: specified via named parameter `Header`" title="**Card title**: specified via named parameter `title`" subtitle="**Card subtitle**: specified via named parameter `subtitle`" footer="**Footer**: specified via named parameter `footer`" %}}
**Content**: inner content of the shortcode, this may be plain text or formatted
text, images, videos, … . If your content is markdown, use the percent sign `%`
as outermost delimiter of your `card` shortcode, your markup should look like
`{{%/* card */%}}Your **markdown** content{{%/* /card */%}}`. In case of HTML
content, use square brackets `<>` as outermost delimiters:
`{{</* card */>}}Your <b>HTML</b> content{{</* /card */>}}` {{% /card %}}
{{% /cardpane %}}

While the main content of the card is taken from the inner markup of the `card`
shortcode, the optional elements `footer`, `header`, `title`, and `subtitle` are
all specified as named parameters of the shortcode.

### Shortcode `card`: programming code

If you want to display programming code on your card, set the named parameter
`code` of the card to `true`. The following sample demonstrates how to code a
card element with the famous `Hello world!` application coded in C:

```go-html-template
{{</* card code=true header="**C**" lang="C" */>}}
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
  puts("Hello World!");
  return EXIT_SUCCESS;
}
{{</* /card */>}}
```

This code translates to the card shown below:

<!-- prettier-ignore-start -->
{{< card code=true header="**C**" lang="C" highlight="" >}}
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
  puts("Hello World!");
  return EXIT_SUCCESS;
}
{{< /card >}}
<!-- prettier-ignore-end -->

<br/>If called with parameter `code=true`, the `card` shortcode can optionally
hold the named parameters `lang` and/or `highlight`. The values of these
optional parameters are passed on as second `LANG` and third `OPTIONS` arguments
to Hugo's built-in [`highlight`](https://gohugo.io/functions/highlight/)
function which is used to render the code block presented on the card.

### Card groups

Displaying two ore more cards side by side can be easily achieved by putting
them between the opening and closing elements of a `cardpane` shortcode. The
general markup of a card group resembles closely the markup of a tabbed pane:

```go-html-template
{{</* cardpane */>}}
  {{</* card header="Header card 1" */>}}
    Content card 1
  {{</* /card */>}}
  {{</* card header="Header card 2" */>}}
    Content card 2
  {{</* /card */>}}
  {{</* card header="Header card 3" */>}}
    Content card 3
  {{</* /card */>}}
{{</* /cardpane */>}}
```

Contrary to tabs, cards are presented side by side, however. This is especially
useful it you want to compare different programming techniques (traditional vs.
modern) on two cards, like demonstrated in the example above:

{{< cardpane >}} {{< card code=true header="**Java 5**" >}} File[] hiddenFiles =
new File("directory_name") .listFiles(new FileFilter() { public boolean
accept(File file) { return file.isHidden(); } }); {{< /card >}}
{{< card code=true header="**Java 8, Lambda expression**" >}} File[] hiddenFiles
= new File("directory_name") .listFiles(File::isHidden); {{< /card >}}
{{< /cardpane >}}

## Include external files

Sometimes there's content that is relevant for several documents, or that is
maintained in a file that is not necessarily a document. For situations like
these, the `readfile` shortcode allows you to import the contents of an external
file into a document.

### Reuse documentation

In case you want to reuse some content in several documents, you can write said
content in a separate file and include it wherever you need it.

For example, suppose you have a file called `installation.md` with the following
contents:

```go-html-template
## Installation

{{%/* alert title="Note" color="primary" */%}}
Check system compatibility before proceeding.
{{%/* /alert */%}}

1.  Download the installation files.

1.  Run the installation script

    `sudo sh install.sh`

1.  Test that your installation was successfully completed.
```

You can import this section into another document:

```go-html-template
The following section explains how to install the database:

{{%/* readfile "installation.md" */%}}
```

This is rendered as if the instructions were in the parent document. Hugo
v0.101.0+ is required for imported files containing shortcodes to be rendered
correctly.

---

The following section explains how to install the database:

{{% readfile "includes/installation.md" %}}

---

The parameter is the relative path to the file. Only relative paths under the
parent file's working directory are supported.

For files outside the current working directory you can use an absolute path
starting with `/`. The root directory is the `/content` folder.

### Include code files

Suppose you have an `includes` folder containing several code samples you want
to use as part of your documentation. You can use `readfile` with some
additional parameters:

```go-html-template
To create a new pipeline, follow the next steps:

1.  Create a configuration file `config.yaml`:

    {{</* readfile file="includes/config.yaml" code="true" lang="yaml" */>}}

1.  Apply the file to your cluster `kubectl apply config.yaml`
```

This code automatically reads the content of `includes/config.yaml` and inserts
it into the document. The rendered text looks like this:

---

To create a new pipeline, follow the next steps:

1.  Create a configuration file `config.yaml`:

    {{< readfile file="includes/config.yaml" code="true" lang="yaml" >}}

1.  Apply the file to your cluster `kubectl apply config.yaml`

---

{{% alert title="Warning" color="warning" %}} You must use `{{</* */>}}`
delimiters for the code highlighting to work correctly. {{% /alert %}}

The `file` parameter is the relative path to the file. Only relative paths under
the parent file's working directory are supported.

For files outside the current working directory you can use an absolute path
starting with `/`. The root directory is the `/content` folder.

| Parameter | Default    | Description                                              |
| --------- | ---------- | -------------------------------------------------------- |
| file      |            | Path of external file                                    |
| code      | false      | Boolean value. If `true` the contents is treated as code |
| lang      | plain text | Programming language                                     |

### Error reporting

If the shortcode can't find the specified file, the shortcode throws a compile
error.

In the following example, Hugo throws a compile error if it can't find
`includes/deploy.yml`:

```go-html-template
{{</* readfile file="includes/deploy.yaml" code="true" lang="yaml" */>}}
```

Alternately, Hugo you can display a message on the rendered page instead of
throwing a compile error. Add `draft="true"` as a parameter. For example:

```go-html-template
{{</* readfile file="includes/deploy.yaml" code="true" lang="yaml" draft="true" */>}}
```

## Conditional text

The `conditional-text` shortcode allows you to show or hide parts of your
content depending on the value of the `buildCondition` parameter set in your
configuration file. This can be useful if you are generating different builds
from the same source, for example, using a different product name. This
shortcode helps you handle the minor differences between these builds.

```text
{{%/* conditional-text include-if="foo" */%}}
This text appears in the output only if `buildCondition = "foo" is set in your config file`.
{{%/* /conditional-text */%}}
{{%/* conditional-text exclude-if="bar" */%}}
This text does not appear in the output if `buildCondition = "bar" is set in your config file`.
{{%/* /conditional-text */%}}
```

If you are using this shortcode, note that when evaluating the conditions,
substring matches are matches as well. That means, if you set
`include-if="foobar"`, and `buildcondition = "foo"`, you have a match!

[shortcode delimiter]:
  https://gohugo.io/content-management/shortcodes/#use-shortcodes
