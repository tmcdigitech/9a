---
title: Child templates
weight: 70
---
You can probably appreciate how nice it is to have a base template to do *most* of the template work to create a consistent look: importing style sheets, laying out the screen, handling menus and other site navigation, providing the header and footer. But within that broad structure there are other patterns across pages within this, so we need a template for them which will extend the base template. This is what child templates are for.

```
📂 flask_demo
 ├─📄 app.py
 └─📂 templates
    ├─📄 base.html
    ├─📄 index.html
    └─📄 page.html
```

