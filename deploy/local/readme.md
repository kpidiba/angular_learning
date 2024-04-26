# LOCAL DEPLOY



Pour déployer une application Angular qui consomme des API Spring Boot sur un serveur local dans votre entreprise, vous pouvez suivre ces étapes :

1. **Préparer votre application Angular :**
   
   - Assurez-vous que votre application Angular est prête à être déployée. Vous devez avoir généré les fichiers de production en exécutant la commande `ng build --prod`. Cela générera un dossier `dist` contenant les fichiers statiques de votre application Angular.

2. **Choisir un serveur HTTP :**
   
   - Vous aurez besoin d'un serveur HTTP pour servir les fichiers statiques de votre application Angular. Vous pouvez utiliser des serveurs comme Apache HTTP Server, Nginx, ou même le serveur intégré fourni par Angular (bien que cela soit plus adapté au développement qu'à la production).

3. **Configurer le serveur HTTP :**
   
   - Configurez le serveur HTTP pour servir les fichiers statiques à partir du dossier `dist` généré par Angular. Assurez-vous que les règles de routage sont correctement définies pour diriger le trafic vers votre application Angular.

4. **Déployer votre application Angular :**
   
   - Transférez les fichiers de production générés (`index.html`, `main.js`, etc.) du dossier `dist` vers le répertoire de votre serveur HTTP.

5. **Configurer les URL des API :**
   
   - Si votre application Angular consomme des API Spring Boot, assurez-vous que les URL utilisées pour appeler ces API sont correctement configurées dans votre application Angular. Ces URL devraient correspondre aux endpoints exposés par votre application Spring Boot.

6. **Déployer votre application Spring Boot :**
   
   - Si ce n'est pas déjà fait, suivez les étapes mentionnées précédemment pour déployer votre application Spring Boot sur le même serveur ou sur un autre serveur local. Assurez-vous que votre application Spring Boot est accessible depuis l'URL configurée dans votre application Angular.

7. **Tester votre application :**
   
   - Une fois que les deux applications sont déployées, testez l'ensemble du système en accédant à votre application Angular depuis un navigateur. Assurez-vous que les appels API fonctionnent comme prévu et que votre application Angular se comporte comme attendu.

8. **Gérer les problèmes de CORS :**
   
   - Si votre application Angular et votre application Spring Boot sont déployées sur des domaines différents (par exemple, si elles s'exécutent sur des ports différents), vous pourriez rencontrer des problèmes de CORS (Cross-Origin Resource Sharing). Assurez-vous que votre serveur Spring Boot est configuré pour autoriser les requêtes CORS provenant du domaine où est déployée votre application Angular.

## HTTP SERVER

So you are trying to debug the production build of your Angular app, you've run `ng build --prod` and you have your production files in your `/dist` folder but you can't quite seem to run the files locally.

Unfortunately there is no way to run `ng serve --prod` and serve the production build of your app locally. Here to save the day, the npm package: `http-server`.

> [http-server](https://www.npmjs.com/package/http-server) 
> is a simple, zero-configuration command-line http server. It is powerful
>  enough for production usage, but it's simple and hackable enough to be 
> used for testing, local development, and learning.
> 
> When I last checked today (4/5/2021), the package had 3.1 million weekly downloads. This is a very popular npm package.

## Download the `http-server` npm package

In the root directory of your Angular project, run the following command to download the `http-server` package:

`npm install http-server -g`

## Build Your Angular App with the Production flag

Once the package downloads successfully, build your Angular project with the production flag using the following command:

`ng build --prod`

Your output/deployable files should now be in the `/dist` folder of your application. Your files may be outputted to a different folder depending on the value of the `outputPath` property in the `angular.json` file for your Angular app.

## Serve Your Production App using the `http-server` Command

Serve your newly outputted production files locally using the following command: `http-server dist/`

Keep in mind that you may have to substitute `dist/` with a different directory if the `outputPath` property in the `angular.json` file is different than the default of `dist`.

## The Production App Locally

If your `http-server dist/` command was successful, you will see an output in your command line similar to this:

```console
Starting up http-server, serving dist/
Available on:
  http://10.0.0.3:8080
  http://127.0.0.1:8080
Hit CTRL-C to stop the server
```

Navigate to either *10.0.0.3:8080* or *127.0.0.1:8080*.

> The production version of your Angular application will now be accessible on your local machine!
