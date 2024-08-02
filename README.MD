

## Table of Contents

- [Notarious Chrome Extension](#notarious-chrome-extension)
  - [Project Structure](#project-structure)
    - [I. `src` Folder: This is where all your extension's code resides. It contains:](#i-src-folder-this-is-where-all-your-extensions-code-resides-it-contains)
  - [Key Files and Folders](#key-files-and-folders)
    - [I. `manifest.json`](#i-manifestjson)
    - [II. `pages` Folder](#ii-pages-folder)
  - [Development Workflow](#development-workflow)
    - [Example Usage](#example-usage)
    - [Summary](#summary)



# Notarious Chrome Extension

This project uses the template provided by lxieyang which is located here: (https://github.com/lxieyang/chrome-extension-boilerplate-react)[https://github.com/lxieyang/chrome-extension-boilerplate-react]

## Project Structure

### I. `src` Folder: This is where all your extension's code resides. It contains:

- `assets`: Store your static assets like images, icons, and stylesheets here.
- `containers`: Typically used for higher-level components that manage state and logic.
- `pages`: Contains the different pages of your extension (e.g., Popup, Options, Background, Content Scripts, etc.).
- `manifest.json`: The configuration file for your Chrome extension.

## Key Files and Folders

### I. `manifest.json`

This file defines the structure and permissions of your Chrome extension. It includes information like the extension's name, version, icons, and the scripts it uses. For example:

```
{
  "manifest_version": 3,
  "name": "Notarious Chrome Extension",
  "description": "A chrome extension built with React 18, Webpack 5, and Webpack Dev Server 4",
  "options_page": "options.html",
  "background": { "service_worker": "background.bundle.js" },
  "action": {
    "default_popup": "popup.html",
    "default_icon": "icon-34.png"
  },
  "chrome_url_overrides": {
    "newtab": "newtab.html"
  },
  "icons": {
    "128": "icon-128.png"
  },
  "content_scripts": [
    {
      "matches": ["http://*/*", "https://*/*", "<all_urls>"],
      "js": ["contentScript.bundle.js"],
      "css": ["content.styles.css"]
    }
  ],
  "devtools_page": "devtools.html",
  "web_accessible_resources": [
    {
      "resources": ["content.styles.css", "icon-128.png", "icon-34.png"],
      "matches": []
    }
  ]
}
```

### II. `pages` Folder

This folder contains the different parts of your extension:

- `Background`: Contains the background script which runs in the background and can handle events like alarms, network requests, etc. 
  - Example: `src/pages/Background/index.js`.
- `Content`: Contains content scripts that run in the context of web pages. 
  - Example: `src/pages/Content/index.js`.
- `Devtools`: Contains the code for the DevTools page. 
  - Example: `src/pages/Devtools/index.js`.
- `Newtab`: Contains the code for the new tab page. 
  - Example: `src/pages/Newtab/index.jsx`.
- `Options`: Contains the options page where users can configure the extension. 
  - Example: `src/pages/Options/index.jsx`.
- `Panel`: Contains the code for the panel page. 
  - Example: `src/pages/Panel/index.jsx`.
- `Popup`: Contains the popup page that appears when the extension icon is clicked. 
  - Example: `src/pages/Popup/index.jsx`.

## Development Workflow

1. Install Dependencies: Run `npm install` to install all the necessary dependencies.

2. Start Development Server: Run `npm start` to start the Webpack development server. This will watch for changes and automatically reload the extension in your browser.

3. Load Extension in Chrome:
   - Go to chrome://extensions/.
   - Enable Developer mode.
   - Click on Load unpacked and select the build folder.

4. Build for Production: When you're ready to build the extension for production, run: `NODE_ENV=production npm run build`.  This will create a production-ready build in the `build` folder.

### Example Usage

Adding a New Content Script
1. Create a new file in `src/pages/Content/` (e.g., `myContentScript.js`).
2. Add your script to the `entry` in `webpack.config.js`: 
```
entry: {
  myContentScript: path.join(__dirname, 'src', 'pages', 'Content', 'myContentScript.js'),
  // other entries...
},
```
3. Update `manifest.json` to include your new content script:
```
"content_scripts": [
  {
    "matches": ["http://*/*", "https://*/*", "<all_urls>"],
    "js": ["myContentScript.bundle.js"],
    "css": ["content.styles.css"]
  }
]
```

### Summary

- `src` folder: Contains all your extension code.
- `manifest.json`: Configures your extension.
- `pages` folder: Contains different parts of your extension.
- Development: Use `npm start` to run the development server and `npm run build` to create a production build.

Feel free to explore the existing code in the `src/pages` folder to see how different parts of the extension are implemented. Happy coding!