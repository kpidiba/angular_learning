Dans le monde interconnecté d'aujourd'hui, où l'accès à Internet est devenu essentiel pour les entreprises et les particuliers, il est impératif **d'assurer la sécurité, la performance et la gestion efficace du trafic réseau**. C'est ici que les serveurs web et les proxys font leur entrée : ce sont des **pièces maîtresses de l'architecture réseau** qui agissent comme des intermédiaires intelligents, fournissant une série d'avantages cruciaux pour les environnements en ligne.

Parmi les serveurs web les plus populaires, nous retrouvons notamment Nginx : en quelques années, il s'est rapidement imposé comme **la référence pour exécuter des serveurs web** en raison de ses performances élevées et de ses nombreuses fonctionnalités. Aujourd'hui, les sites web les plus fréquentés comme Netflix, la NASA ou encore WordPress utilisent Nginx pour ses capacités hors normes.

Dans cet article, nous allons étudier le fonctionnement de Nginx, comment il peut être utilisé en tant que serveur web ou reverse proxy (proxy inverse), et un exemple de configuration de serveur web avec Nginx sera proposé.

## Nginx

**Nginx** (prononcé *Engine X*) est un serveur web open source et un reverse proxy reconnu pour sa haute performance, sa stabilité et sa capacité à gérer de grandes quantités de trafic web. Créé par Igor Sysoev en 2004, Nginx est devenu l'un des serveurs web les plus populaires et est largement utilisé pour optimiser la livraison web, équilibrer la charge des serveurs et gérer efficacement le trafic réseau.

![](https://blent-static-media.s3.eu-west-3.amazonaws.com/photos/blog/nginx_logo.png)

Nginx dispose d'un large éventail de fonctionnalités et de caractéristiques.

- **Serveur Web** : Nginx est capable de traiter des fichiers statiques tels que HTML, CSS, JavaScript et images, ainsi que de gérer des requêtes HTTP/HTTPS. Il est célèbre pour sa rapidité et son efficacité dans la gestion simultanée de plusieurs connexions.
- **Reverse Proxy** : Nginx peut être configuré en tant que proxy inverse afin de rediriger le trafic HTTP/HTTPS vers des serveurs d'application ou des serveurs web backend. Cela facilite la répartition du trafic, la gestion de la mise en cache et l'amélioration de la sécurité.
- **Équilibrage de charge** : [l'équilibrage de charge](https://blent.ai/blog/a/load-balancing-definitions-exemples) peut être effectué par Nginx en répartissant les requêtes entre plusieurs serveurs backend. Cela permet de répartir la charge sur plusieurs serveurs, ce qui augmente la disponibilité et les performances.
- **Gestion des certificats SSL/TLS** : Nginx prend en charge le chiffrement SSL/TLS, ce qui permet aux clients et aux serveurs web de sécuriser les communications. Il est également possible de configurer des certificats SSL, tels que Let's Encrypt, avec cet outil.
- **Redirections et gestion des connexions** : Nginx est un excellent choix pour les sites web avec beaucoup de connexions simultanées. Il est également capable de configurer des redirections HTTP, y compris les redirections permanentes (301) et temporaires (302).
- **Règles de routage URL** : la configuration de règles de routage basées sur les URL permet de diriger les requêtes vers différents endroits en fonction des chemins d'URL.

## L'histoire de Nginx

La toute première version officielle de Nginx a été créé par Igor Sysoev, un ingénieur russe, en 2004. Cet ingénieur a commencé à développer Nginx en 2002 pour résoudre les problèmes de montée en charge et de performances qu'il rencontrait avec les serveurs web existants à l'époque. Il visait à développer un serveur web rapide, léger et capable de gérer un grand nombre de connexions simultanées.

---

**À lire** : [découvrez notre formation DevOps Engineer](https://blent.ai/formation/cloud-devops)

---

Nginx a rapidement **gagné en popularité grâce à ses performances élevées, sa stabilité et sa capacité à gérer efficacement plusieurs connexions** à la fois. Il est devenu un choix populaire pour les équilibreurs de charge, les serveurs proxy inverses et les sites web à fort trafic.

Les fonctionnalités se sont élargies au fil du temps pour inclure la gestion des certificats SSL/TLS, la prise en charge de modules tiers et d'autres fonctionnalités avancées de sécurité. Il est devenu une partie importante de l'infrastructure web de nombreuses entreprises et sites web célèbres.

De nos jours, Nginx surpasse les autres serveurs web présents sur le marché avec **35% de part de marché**, là où Apache HTTP Server possède 30% de part de marché et les 35% restant distribués pour plusieurs alternatives.

### Utilisation de Nginx

De manière générale, Nginx est principalement utilisé dans deux cas de figure.

- Nginx peut être utilisé **en tant que serveur web** pour servir de manière statique (HTML, images, fichiers) et dynamique (via des modules ou des langages de programmation comme PHP, Python, etc). Sa structure légère lui permet de gérer efficacement un grand nombre de connexions simultanées, ce qui en fait un excellent choix pour les sites à forte fréquentation.
- Là où Nginx excelle également, c'est dans sa **capacité à agir comme un reverse proxy** (*proxy inverse*). Il dispose notamment de nombreuses fonctionnalités permettant de gérer la répartition du trafic selon des règles dynamiques, la mise en mémoire cache et les règles d'accès. On le retrouve d'ailleurs fréquemment sur des outils comme [Kubernetes](https://blent.ai/blog/a/tutoriel-kubernetes-introduction) pour gérer le trafic entrant sur un ou plusieurs services.

On retrouve notamment Nginx lorsque des applications sont déployées dans des serveurs : en général, ces applications ne disposent pas des droits administrateurs et doivent donc écouter un port supérieur à 1024 du serveur hôte (8080 par exemple). Ainsi, si l'on souhaite exposer sur le port 80 (HTTP) l'application, Nginx peut faire office d'intermédiaire avec la capacité de mettre en cache les réponses ou de gérer les certificats SSL (HTTPS).

![](https://blent-learning-user-ressources.s3.eu-west-3.amazonaws.com/training/devops/img/nginx-proxy.png)

### Reverse Proxy

Un **Reverse Proxy** agit comme un gardien entre les utilisateurs externes et les serveurs internes. Lorsqu'un utilisateur envoie une demande, le reverse proxy redirige cette demande vers le serveur interne approprié. Les utilisateurs externes **ne voient que le reverse proxy**, ce qui cache la structure et la disposition des serveurs internes, améliorant ainsi la sécurité.

![](https://blent-learning-user-ressources.s3.eu-west-3.amazonaws.com/training/devops/img/reverse-proxy.png)

Un des principaux cas d'utilisation du reverse proxy concerne **l'équilibrage de charge** : les reverse proxys **répartissent le trafic entre plusieurs serveurs internes**, garantissant une répartition équitable de la charge et une performance optimale. Cela apporte également un autre avantage concernant la sécurité renforcée, car les serveurs internes sont protégés, puisque **seuls les reverse proxys sont exposés aux utilisateurs externes**, minimisant les risques d'attaques directes.

Enfin, les reverse proxy peuvent mettre en place des mécanismes de gestion du trafic (comme les redirections adaptées selon l'origine de la requête), les techniques de mise en cache des réponses serveurs interne (réduisant ainsi la demande sur ces serveurs et améliorant la vitesse de chargement) et de compression de données. Dans un contexte DevOps, **ce sont plus régulièrement les reverse proxys qui interviennent**.

---

**Pour en savoir plus** : [notre formation DevOps Engineer](https://blent.ai/formation/cloud-devops)

---

En se positionnant devant un serveur web, un reverse proxy **assure qu'aucun client ne communique directement avec le serveur**. Un forward proxy se place devant les points de terminaison des clients pour **intercepter les requêtes entrantes** et s'assurer qu'aucun serveur ne communique directement avec un client tel qu'un navigateur web. Ces types de proxy semblent fonctionnellement similaires, mais les forward proxys dépendent généralement d'un agent logiciel installé sur les points de terminaison pour transmettre le trafic, tandis que les reverse proxys ne le font pas.

## Installer Nginx

Puisque Nginx est à destination de serveurs Linux, il n'est pas possible de l'installer sur Windows, bien qu'il existe une version de développement pour pouvoir tester les fonctionnalités.

Pour installer Nginx sur une distribution Linux, cela peut se faire facilement via les dépôts officiels de paquets Linux.

```bash
sudo apt update
sudo apt install nginx -y
```

Une fois installé, le service Nginx se lance automatiquement, comme nous pouvons le voir en affichant le status du service `nginx`.

```bash
sudo systemctl status nginx
```

```plaintext
● nginx.service - A high performance web server and a reverse proxy server
   Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
   Active: active (running) since Thu 2023-10-05 10:31:59 UTC; 1s ago
     Docs: man:nginx(8)
  Process: 1953 ExecStartPre=/usr/sbin/nginx -t -q -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
  Process: 1954 ExecStart=/usr/sbin/nginx -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
 Main PID: 1955 (nginx)
    Tasks: 3 (limit: 4645)
   Memory: 6.1M
   CGroup: /system.slice/nginx.service
           ├─1955 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
           ├─1956 nginx: worker process
           └─1957 nginx: worker process

Oct 05 10:31:58 ip-172-31-35-145 systemd[1]: Starting A high performance web server and a reverse proxy server...
Oct 05 10:31:59 ip-172-31-35-145 systemd[1]: Started A high performance web server and a reverse proxy server.
```

Cela signifie que l'on peut d'ores et déjà visiter l'URL du serveur où Nginx est installé et la page d'accueil suivante devrait s'afficher.

![](https://blent-learning-user-ressources.s3.eu-west-3.amazonaws.com/training/devops/img/welcome-nginx.png)

## Configurer Nginx

L'ensemble des fichiers de configuration Nginx sont accessibles dans le dossier `/etc/nginx`.

```plaintext
total 64
drwxr-xr-x 2 root root 4096 Nov 22  2022 conf.d
-rw-r--r-- 1 root root 1077 Nov 22  2022 fastcgi.conf
-rw-r--r-- 1 root root 1007 Nov 22  2022 fastcgi_params
-rw-r--r-- 1 root root 2837 Nov 22  2022 koi-utf
-rw-r--r-- 1 root root 2223 Nov 22  2022 koi-win
-rw-r--r-- 1 root root 3957 Nov 22  2022 mime.types
drwxr-xr-x 2 root root 4096 Nov 22  2022 modules-available
drwxr-xr-x 2 root root 4096 Oct  5 10:31 modules-enabled
-rw-r--r-- 1 root root 1482 Nov 22  2022 nginx.conf
-rw-r--r-- 1 root root  180 Nov 22  2022 proxy_params
-rw-r--r-- 1 root root  636 Nov 22  2022 scgi_params
drwxr-xr-x 2 root root 4096 Oct  5 10:31 sites-available
drwxr-xr-x 2 root root 4096 Oct  5 10:31 sites-enabled
drwxr-xr-x 2 root root 4096 Oct  5 10:31 snippets
-rw-r--r-- 1 root root  664 Nov 22  2022 uwsgi_params
-rw-r--r-- 1 root root 3071 Nov 22  2022 win-utf
```

Avant de rentrer dans le détail des configurations, nous voyons notamment les dossiers `sites-available` et `sites-enabled`.

Le dossier `sites-available` contient les fichiers de configuration pour tous les sites que vous souhaitez pouvoir héberger avec Nginx, qu'ils soient actuellement actifs ou non. Le dossier `sites-enabled` contient des liens symboliques vers les fichiers de configuration dans le dossier `sites-available` pour les sites que vous souhaitez actuellement activer et servir avec Nginx.

Avec cette architecture, **Nginx peut à la fois servir des sites et agir sous forme de plusieurs reverse proxys**, le tout en même temps. Justement, pour gérer l'ensemble de ces sites, Nginx utilise la notion **d'hôte virtuel** (*virtual hosts*).

Un **hôte virtuel** permet à un serveur Nginx de gérer plusieurs domaines ou sous-domaines à partir d'un seul serveur. Chaque domaine ou sous-domaine est considéré comme un hôte virtuel, c'est-à-dire comme s'il s'agissait d'un serveur *à part*. Les configurations des hôtes virtuels sont stockées dans des fichiers de configuration individuels, généralement situés dans les dossiers `sites-available` et `sites-enabled`, comme mentionné précédemment.

Le fichier principal de configuration sur Nginx est `/etc/nginx/nginx.conf`. Il est recommandé de créer des fichiers de configuration séparés pour chaque hôte virtuel. Le fichier `/etc/nginx/nginx.conf` peut être modifié et utilisé s'il n'existe qu'un seul hôte virtuel par exemple.

Pour créer un hôte virtuel, nous pouvons créer un nouveau fichier de configuration dans le répertoire `/etc/nginx/sites-available/` avec une extension .`conf`.

Nginx peut servir des fichiers HTML statiques de manière efficace en utilisant les directives de configuration appropriées. Tout d'abord, créons le dossier `/var/www/website` et ajoutons-y le contenu HTML suivant dans le fichier `/var/www/website/index.html`.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Nginx</title>
  </head>
  <body>
    <p>Hello Blent !</p>
  </body>
</html>
```

Maintenant, nous allons créer un hôte virtuel sur Nginx afin de lui indique que le dossier `/var/www/website` va servir de contenu statique.

Créons le fichier `/etc/nginx/sites-available/website.conf` avec le contenu suivant.

```plaintext
server {
    listen 80;
    server_name website.com www.website.com;
    location / {
        root /var/www/website;
        index index.html;
    }
}
```

Détaillons les directives présentes.

- La première directive `server` commence et termine un bloc de configuration pour un hôte virtuel. Tout ce qui est entre les accolades `{}` fait partie de la configuration de cet hôte virtuel.
- `server_name` spécifie les noms de domaine pour lesquels cet hôte virtuel est responsable. Ici, il est configuré pour répondre aux requêtes destinées à `website.com` et `www.website.com`.
- Le bloc `location` définit la configuration pour une certaine partie de l'hôte virtuel, dans ce cas, la racine du site (`/`). Avec `root`, nous indiquons le chemin du système de fichiers où Nginx peut trouver les fichiers pour servir ce site web et avec `index`, le fichier à servir lorsqu'une requête est faite pour ce répertoire.

Une fois le fichier créé, vérifions que notre configuration Nginx ne comporte pas d'erreur.

```bash
nginx -t
```

```plaintext
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

Il est important de vérifier que tous les fichiers de configuration sont valides, car si un seul n'est pas valide, le service Nginx **pourrait ne pas redémarrer et tous les autres hôtes virtuels en seraient impactés**.

Maintenant, il est nécessaire de créer un lien symbolique de `/etc/nginx/sites-enabled/website` vers `/etc/nginx/sites-available/website.conf`, car cela permet d'indiquer que notre site `website` est actif. Cela permet par d'exemple d'active ou de désactiver certains hôtes virtuels dans devoir supprimer le fichier de configuration.

Créons un lien symbolique avec la commande `ln -s`.

```bash
ln -s /etc/nginx/sites-available/website.conf /etc/nginx/sites-enabled/
```

Dans le même temps, nous devons **supprimer le fichier `rm /etc/nginx/sites-enabled/default`** afin de ne pas le prendre en compte au prochain redémarrage de Nginx, car ce dernier contient la fameuse page par défaut vue plus haut.

```bash
rm /etc/nginx/sites-enabled/default
```

Maintenant que tout est prêt, il ne suffit plus qu'à redémarrer Nginx.

```bash
systemctl restart nginx
```

Si l'on recharge la page d'URL du serveur, nous devrions voir seulement apparaître le message `Hello Blent !`.

## Avantages de Nginx

L'un des principaux avantages en faveur de Nginx concerne **ses hautes performances pour les applications web**, ce qui constitue la première raison de son utilisation aussi massive. Ces performances sont également liées à l'économie de ressources : Nginx **utilise moins de ressources système par rapport à d'autres serveurs web**, ce qui permet de réduire la consommation de mémoire et de CPU.

De plus, ses **capacités de configurations variées rendent l'utilisation de Nginx adaptée à de nombreuses situations** : proxy inverse, équilibrage de charge ou encore mise en cache de données. Ainsi, il n'est pas nécessaire de changer d'environnement si l'on souhaite exécuter une autre typologie de serveur Web.

Enfin, d'un point de vue optimisation et sécurité, **Nginx offre un large éventail de configuration** pour le support de certificats SSL/TLS, la compression Gzip de données, mais aussi avec l'utilisation de modules permettant d'étendre son usage avec pour des situations bien spécifiques.

## Conclusion

Au final, Nginx a réussi à se faire une place de choix comme **l'un des serveurs web et des serveurs proxy inverses les plus efficaces et les plus adaptables** actuellement présents. Son développement depuis ses débuts modestes en tant que projet open source jusqu'à sa généralisation dans les infrastructures web du monde entier démontre sa qualité et son efficacité.

Nginx est un **choix incontournable pour les entreprises cherchant à optimiser leurs sites web** et leurs applications en raison de ses performances élevées, de sa faible consommation de ressources, de son équilibrage de charge, de sa gestion avancée de la mise en cache et de ses fonctionnalités de sécurité robustes.

Pour en apprendre plus sur Nginx et les outils liés au DevOps, [découvrez notre formation DevOps Engineer](https://blent.ai/formation/cloud-devops) qui permet de maîtriser l'ensemble des connaissances et compétences pour appliquer l'approche DevOps en entreprise.
