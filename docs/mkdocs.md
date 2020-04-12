## Tabs in the navigation

With the material theme, sub-navigation items can be used to add horizontal tabs to the navigation. This may be useful if the documentation gets large or extends beyond code, but is not currently implemented

```yaml
nav: 
  - Code:
    - R: R.md
    - Matlab: matlab.md
  - New tab: 
    - Mkdocs: mkdocs.md
theme:
  name: 'material'
  feature:
    tabs: true
```

## Table of Contents


To change table of contents, updated options in the following code in the `.yaml` file:

```
markdown_extensions:
  - toc:
      toc_depth: 3
```

- `toc_depth` changes the lowest heading that will be shown in the table of contents


## Collapsible section in Markdown

See [https://gist.github.com/pierrejoubert73/902cc94d79424356a8d20be2b382e1ab](https://gist.github.com/pierrejoubert73/902cc94d79424356a8d20be2b382e1ab) for more details


    # A collapsible section with markdown
    <details>
      <summary>Click to expand!</summary>
      
      ## Heading
      1. A numbered
      2. list
        * With some
        * Sub bullets
    </details>
