# DevOps Examen 2017

Het doel van het examen is een opzetten van een multi  instances website met een
loadbalancer. De Loadbalancer draait op een virtuele machine. De provisioning
hiervan word uitgevoerd door Ansible. De website word op dezelfde manier
opgezet en geconfigureerd. Er worden 4 instances opgezet van de website.  Vagrant
configureert de virtuele machines.

## Projectstructuur

We hanteren volgende projectstructuur voor het examen.

***Belangrijke Opmerkingen***
* *Sommige files zijn leeg en placeholders*
* *Voor Ansible maken gebruik van de roles structuur* 
* *Je mag files bijaanmaken*
```
dops_examen_start
├── group_vars            
│   └── all               
├── roles                 
│   └── lb                
│       └── files         
│           └── lb_config 
├── web                   
│   ├── static            
│   │   ├── css           
│   │   │   ├── main.addc2cf1.css                    
│   │   │   └── main.addc2cf1.css.map                
│   │   └── js            
│   │       ├── main.6d07ca0a.js                     
│   │       └── main.6d07ca0a.js.map                 
│   ├── asset-manifest.json                          
│   ├── Dockerfile        
│   ├── favicon.ico       
│   ├── index.html        
│   ├── manifest.json     
│   └── service-worker.js 
├── bootstrap.sh          
├── docker-compose.yml    
├── hosts                 
├── lb.yml                
├── README.md             
└── Vagrantfile  
```

## Requirements
### Virtuele Machines
Vagrant configureert de virtuele machines die nodig zijn. De mgr node (Ansible
client) is al voorzien. Hierop draait ook de loadbalancer haproxy. Voorziet ook een virtuele machine die dient als docker host. Zorg er voor
dat beide machines met elkaar communiceren. **Haal de configuratie voor het
toewijzen van IPs en het openzetten van de juiste poorten uit de configuratie
van de loadbalancer.**

* Toevoegen van extra virtuele machine als docker host
* Opzetten van communicatie tussen beiden machines
  * Alle machines zijn te bereiken op een `private_network`
  * Loadbalancer is vanuit host omgeving bereikbaar op poort `8000`dd

### Loadbalancer

Maak een ansible playbook die de manager node provisiont als Loadbalancer. Er
is al een gedeelte aanwezig vul de rest aan. De configuratie file kan 'as is'
gebruikt worden. Er moeten geen aanpassing worden gemaakt zolang het de rest
conform is met de configuratie. 

* Ansible kan zonder paswoord verbinden met target machine
* Vervolledig de `lb` rol
* Maak een playbook aan voor het oproepen van de rol

### Loadbalancer

Maak een ansible playbook die de web nodes provisiont met nginx en de web
folder gebruikt als www root. Er is al een gedeelte aanwezig vul de rest aan.
De configuratie file van de standaard nginx installatie kan 'as is' gebruikt
worden. Er moeten geen aanpassing worden gemaakt zolang het de rest conform is
met de configuratie. Vergeet niet de www root juist in te stellen. 

* Ansible kan zonder paswoord verbinden met target machine
* Vervolledig de `web` rol
* Maak een playbook aan voor het oproepen van de rol

## Verbetersleutel 

1. `vagrant up`
2. `vagrant ssh mgr`
    1. `ansible-playbook -i /vagrant/hosts /vagrant/lb.yml`
    1. `ansible-playbook -i /vagrant/hosts /vagrant/web.yml`
4. Surf naar `http://192.168.50.19`
5. Surf naar `http://192.168.50.19/haproxy?stats`
6. Refresh website
7. Refresh stats

Lukt dit dan kan u 80% van de punten behalen,  De laatste 20% kan u verdienen
door stap 2 overbodig te maken.




