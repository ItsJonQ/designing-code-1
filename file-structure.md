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