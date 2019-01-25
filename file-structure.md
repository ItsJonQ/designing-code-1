# File Structure

Having a well organized file structure makes it easier to follow/trace dependencies, and most importantly, locate files!

## File vs Folder

It is usually recommended that you create a **folder** for brand new code. This allows you to contain related files such as tests, examples, stories, or documentation.

**Example**

```
Homer/
  | __tests__/
  |   \ Homer.test.js
  | Homer.js
  | Homer.css.js
  | Homer.utils.js
  \ index.js
```

In this scenario, treat your code like a module (because it is 🤓), not unlike what you'd find under `node_modules`.

If your code doesn't require any of the above, then a simple file will do.

## Folders

The following are guides if you need to create a folder for your code.

### Entry Point

Your folder should have a single entry point - the `index.js` file. This file is responsible for exporting modules for consumption.

**Example**

```js
// Homer/index.js
import Homer from './Homer'

export default Homer
```

The benefit of having the `index.js` act as an entry point vs. being the actual module is to make files easier to find. For example, it's much easier fuzzy finding and identifying `Homer.js` in your code editor vs. `index.js`.

### Namespacing

Adding a namespace to sub files (like `Homer.css.js`) makes it easier to see it's relationship to the module.

#### Verboseness

If your module has many (many) sub files or sub modules, namespacing can get a little ridiculous:

**Example**

```
Homer/
  | ...
  | Homer.Shirt.js
  | Homer.Shirt.css.js
  | Homer.Shirt.Pocket.js
  | Homer.Shirt.Pocket.css.js
  | ...
  \ index.js
```

In this case, dropping the module name might work out better:

```
Homer/
  | ...
  | Shirt.js
  | Shirt.css.js
  | Pocket.js
  | Pocket.css.js
  | ...
  \ index.js
```

You still have context clarity since these files live under the primary `Homer` directory.