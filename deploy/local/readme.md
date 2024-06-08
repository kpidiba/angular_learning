# LOCAL DEPLOY

## CONTENT

- ### [HTTP SERVER](./http_server/readme.md)
- ### [NGINX](nginx/readme.md)

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
