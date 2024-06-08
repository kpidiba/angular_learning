## HTTP SERVER

If you need to debug the production build of your Angular app locally, you can use the `http-server` npm package. Here's how:

1. **Download the `http-server` npm package:** Install the package globally by running:
   
   ```bash
   npm install http-server -g
   ```

2. **Build Your Angular App with the Production Flag:** Generate the production build of your Angular project using:
   
   ```bash
   ng build --prod
   ```

3. **Serve Your Production App using `http-server`:** Serve your production files locally by running:
   
   ```bash
   http-server dist/`
   ```
   
   Or

```bash
cd dist/your-project-name
http-server -o
```

4. **Access Your Application Locally:** If successful, you'll see output similar to:
   
   ```console
   Starting up http-server, serving dist/
   Available on:
   http://10.0.0.3:8080
   http://127.0.0.1:8080
   Hit CTRL-C to stop the server
   ```

`Starting up http-server, serving dist/ Available on: http://10.0.0.3:8080 http://127.0.0.1:8080 Hit CTRL-C to stop the server`

Navigate to either `http://10.0.0.3:8080` or `http://127.0.0.1:8080` in your browser to access your production Angular application locally.

These steps should help you deploy and test your Angular application locally after building it for production. Let me know if you need further assistance!
