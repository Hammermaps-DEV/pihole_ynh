Using Pi-hole as your DHCP server
==================

> **Be carreful, you should considering that playing with your DHCP may break your network.  
In case in your server become to be down, you're going to lose your dns resolution and your ip address.  
By this way, you'll losing any internet connection and even the connection to your router.**

> **If you encounter that kind of problem, please see "How to restore my network" at the end of this document.**

### How to configure Pi-hole

There two ways to configure Pi-hole to be used as your DHCP server.
- Either you can choose to use it when you're installing the app.
- Or you can activate the DHCP server after in the "Settings" tab, "Pi-hole DHCP Server" part.  
In this second case, it can be better to set the ip of the server to a static address

### How to configure my router

Your personnal router or the router of your ISP brings a DHCP server activate by default.  
If you keep this DHCP, at the same time of Pi-hole's one, you will encouter a transparent conflict between them.  
The first responding DHCP will distribute its own ip and parameters.  
So you have to turn off the DHCP of your router to let Pi-hole managed your network.

#### Why do I should use only the DHCP of Pi-hole ?

By using the DHCP of Pi-hole, you'll allow it to give at each of your client its dns configuration. Like that, each of your request will be filtering by Pi-hole.

An another use case of using Pi-hole's DHCP is if you have some hairpinning problems (You can't connect to your server because its IP is your public IP, and your router doesn't allow that).  
In this case, use the dns of Pi-hole will allow you to connect to your server by its local adress instead of its public one.

### How to restore my network

> Oh crap !  
Your Pi-hole is down, and you don't have a DHCP anymore.  
Don't panic, we can overcome it \o/

Use your favorite terminal on your desktop computer.  
And first, get your main interface (`eth0` in most cases).
``` bash
sudo ifconfig
```

Then, set your ip as a static ip.
``` bash
sudo ifconfig eth0 192.168.1.100
```

Now, you can connect to your router and turn on its DHCP server to reuse it.  
You can now reset your ip and get a dynamic address
``` bash
sudo ifconfig eth0 0.0.0.0 && sudo dhclient eth0
```

> Don't forget to turn off the DHCP of your router if your server is working again.

---

Faire de Pi-hole votre serveur DHCP
==================

> **Attention, vous devez savoir que toucher à votre DHCP pourrait casser votre réseau.  
Dans le cas où votre serveur serait inaccessible, vous perdriez votre résolution dns et votre adresse IP.  
Ainsi, vous perdriez toute connexion à internet et même la connexion à votre routeur.**

> **Si vous rencontrez ce genre de problèmes, merci de lire la section "Comment restaurer mon réseau" à la fin de ce document.**

### Comment configurer Pi-hole

Il y a 2 manière de configurer Pi-hole pour qu'il soit utilisé comme votre serveur DHCP.
- Soit vous pouvez choisir de l'utiliser lorsque vous installez l'application.
- Soit vous pouvez activer le serveur DHCP par la suite dans l'onglet "Settings", partie "Pi-hole DHCP Server".  
Dans ce second cas, il peut être préférable de forcer l'ip du serveur à une adresse statique.

### Comment configurer mon routeur

Votre routeur ou celui de votre FAI dispose d'un serveur DHCP activé par défaut.  
Si vous gardez ce DHCP, en même temps que celui de Pi-hole, vous allez avoir des conflits transparents entre eux.  
Le premier serveur DHCP à répondre va distribuer ses propres ip et paramètres.  
Donc vous devez éteindre le serveur DHCP de votre routeur et laisser Pi-hole gérer votre réseau.

#### Pourquoi je devrais utiliser le DHCP de Pi-hole ?

En utilisant le DHCP de Pi-hole, vous lui permettez de donner sa configuration dns à chacun de vos clients. De cette manière, chaque requête sera filtrée par Pi-hole.

Un autre cas d'usage du DHCP de Pi-hole est le cas où vous rencontrez des problèmes de hairpinning (Vous ne pouvez pas vous connecter à votre serveur parce que son ip est votre ip publique, et votre routeur n'autorise pas cela).  
Dans ce cas, utilisez le dns de Pi-hole va vous permettre de vous connecter à votre serveur par son adresse locale plutôt que son adresse publique.

### Comment restaurer mon réseau

> Oups !  
Votre serveur Pi-hole est tombé, et vous n'avez plus de DHCP.  
Ne paniquez pas, on va surmonter ça \o/

Utilisez votre terminal favori sur votre ordinateur de bureau.  
Et tout d'abord, récupérer votre interface réseau (Le plus souvent `eth0`).
``` bash
sudo ifconfig
```

Ensuite, changer votre ip pour une ip statique.
``` bash
sudo ifconfig eth0 192.168.1.100
```

Maintenant, vous pouvez vous connecter à votre routeur et rallumer son serveur DHCP pour l'utiliser à nouveau.  
Vous pouvez maintenant retirer votre ip statique et réobtenir une ip dynamique.
``` bash
sudo ifconfig eth0 0.0.0.0 && sudo dhclient eth0
```

> N'oubliez pas d'éteindre le DHCP de votre routeur si votre serveur fonctionne à nouveau.
