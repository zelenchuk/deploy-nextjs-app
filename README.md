# deploy-nextjs-app

First Next.js app with server-side rendering:

1. Install Node.js and NPM: Before you start building your Next.js app, you will need to have Node.js and NPM installed
   on your machine. You can download and install the latest version of Node.js from the official website.

2. Install the Next.js CLI: Once you have Node.js and NPM installed, you can install the Next.js CLI by running the
   following command in your terminal:

   ```shell
   npm install -g create-next-app
   ```   

3. Create a new Next.js app: Use the Next.js CLI to create a new app by running the following command in your terminal:

   ```shell
   create-next-app my-app
   ```

   This will create a new Next.js app in a folder named my-app.



4. Add server-side rendering: Next.js supports server-side rendering out of the box, so you don't need to do any
   additional setup. However, you will need to create a custom server to handle server-side rendering. Create a new file
   named server.js in the root of your project with the following contents:

   ```javascript
      const { createServer } = require('http')
      const { parse } = require('url')
      const next = require('next')
      
      const dev = process.env.NODE_ENV !== 'production'
      const app = next({ dev })
      const handle = app.getRequestHandler()
      
      app.prepare().then(() => {
        createServer((req, res) => {
          const parsedUrl = parse(req.url, true)
          const { pathname, query } = parsedUrl
      
          if (pathname === '/a') {
            app.render(req, res, '/a', query)
          } else if (pathname === '/b') {
            app.render(req, res, '/b', query)
          } else {
            handle(req, res, parsedUrl)
          }
        }).listen(3000, (err) => {
          if (err) throw err
          console.log('> Ready on http://localhost:3000')
        })
      })
   ```

5. Update the scripts in package.json: In your package.json file, update the scripts section to include a new script
   named dev:

    ```json
   "scripts": {
     "dev": "node server.js"
   }
   
   ```
6. Start the development server: Start the development server by running the following command in your terminal:

   ```shell
   npm run dev
   ```
   This will start the custom server and open your Next.js app in a web browser at http://localhost:3000.

7. Test server-side rendering: To test that server-side rendering is working correctly, open a new tab in your web
   browser and navigate to http://localhost:3000/a. You should see the /a page rendered with server-side rendering.

