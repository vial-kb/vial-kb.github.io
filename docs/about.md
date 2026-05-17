---
layout: page
title: About
permalink: /about/
nav_order: 6
---

## Contributing to Vial

Vial is a fully open source project and open to contributions. Different aspects of the project are distributed across three repos:

* [vial-kb/vial-qmk](https://github.com/vial-kb/vial-qmk): Vial keyboard firmware, fork of [qmk/qmk\_firmware](https://github.com/qmk/qmk_firmware). Note that vial-qmk tracks the mainline QMK repo. To avoid merge conflicts, changes to core QMK code are kept to a minimum.

* [vial-kb/vial-gui](https://github.com/vial-kb/vial-gui): Vial desktop application and the web app UI, written in Python with the [fbs GUI framework](https://build-system.fman.io/).

* [vial-kb/vial-kb.github.io](https://github.com/vial-kb/vial-kb.github.io): Vial documentation (this website). Follow the section below for details.


## Contributing to these docs

The git repository for these docs is located at [vial-kb/vial-kb.github.io](https://github.com/vial-kb/vial-kb.github.io). It is built using [Jekyll](https://jekyllrb.com/docs/) and based on the [Just the Docs](https://just-the-docs.com/) theme. To contribute, follow these guidelines for writing and testing your changes.

### Authoring content

Documentation sources are written in Markdown and parsed by Kramdown. Refer to the [Kramdown Syntax](https://kramdown.gettalong.org/syntax.html) guide for comprehensive documentation of supported features.

**YAML metadata:** Each documentation `.md` file begins with a triple-dash `---` enclosed YAML block, defining page metadata:
```yaml
---
layout: default
title: Page Title
parent: Parent Page Name
nav_order: 1
---
```
* `layout`: Typically `default` for standard content pages or `page` for standalone pages.
* `title`: The title displayed in the sidebar navigation and at the top of the page.
* `parent`: The title of the parent page for hierarchical navigation.
* `nav_order`: The sort order for the page within its parent section.

**Links:** For internal links, use [Jekyll's link syntax](https://jekyllrb.com/docs/liquid/tags/#links) to the target `.md` file. To link to a specific section, append `#` after the `%}` and followed by the section heading in lowercase, with spaces replaced by hyphens. For external links, use the complete URL, including the protocol. 

<!--We obfuscate the link syntax so that Liquid doesn't change it.-->
*Examples:*
<pre>
&lbrack;Internal page&rbrack;({&#37; link manual/first-use.md &#37;})
&lbrack;Internal section&rbrack;({&#37; link file.md &#37;}#section-heading)
&lbrack;External link&rbrack;(https://docs.qmk.fm/)
</pre>

**Images:** Images reside in the `docs/img/` directory. Reference them using relative paths:
```markdown
![Alt text describing the image](../img/image-name.png)
```
Ensure alt text is descriptive to maintain accessibility.

### Compiling the documentation

This site is built using Jekyll. To preview your changes locally, you must install Jekyll and serve the site.

1. **Install Jekyll**: Follow [Jekyll Installation](https://jekyllrb.com/docs/installation/).
2. **Install Dependencies**: Navigate to the `docs` directory and install the required gems:
   ```bash
   bundle config set --local path 'vendor/bundle'
   bundle update
   bundle install
   ```
3. **Serve the Site**: Run the following command to start a local development server:
   ```bash
   bundle exec jekyll serve
   ```

The site will be available at `http://localhost:4000`.


## Licenses

Vial is released under a [GPL-2.0 License](https://github.com/vial-kb/vial-gui/blob/main/COPYING).

This site is based on [Just the docs](https://just-the-docs.com/) theme running on [Jekyll](https://github.com/jekyll).

Icons used are from [Carbon Design System](https://github.com/carbon-design-system/carbon) under an Apache-2.0 License.
