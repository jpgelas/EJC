### Étude de la consommation énergétique des Smart contracts dans la blockchain Ethereum
<br>
##### Jean-Patrick Gelas, Hayri Acar, Hind Benfenatki
##### Université Lyon 1/LIRIS/INRIA/ENS Lyon
<br>
##### Entretiens Jacques Cartier, 12-13 novembre 2018, ENS Lyon

---

### $ who am i
<br><br>
```JSON
{
	"first_name" : "Jean-Patrick",
	"last_name" : "Gelas",
	"job" : "Assistant Professor",
	"locations" : [ "Université Claude Bernard - Lyon 1",
			"Avalon/INRIA/ENS Lyon" ],
	"github" : "https://github.com/jpgelas",
	"url" : "https://perso.univ-lyon1.fr/jean-patrick.gelas",
	"email" : "jean-patrick.gelas@univ-lyon1.fr"
}
```

---

### Agenda

On ne parlera pas de ...

@ul
 - Algorithmes de consensus (PoW, PoS, ...)
 - Minage	
 - Merkle trees
 - Comment devenir un crypto millionaire ! :-)
@ulend
 
---

### Objectifs
 
 - Bref rappels (Blochain, Mineurs, ...)
 - Introduction aux Smart Contracts de la blockchain Ethereum : 
   - Création, déploiement, usage, fonctionnement.
 

---

### Rappels

 - Blockchain : Structure de données simple 
 - La technologie Blockchain : « Base de données » sécurisées et décentralisées. 
 - Les mineurs :  
   - génèrent de nouveaux coins (par rétribution), 
   - vérifient l’intégrité de la blockchain,
   - ajoutent de nouvelles liste de transaction (des blocs) à la chaine.

 - Mining ether = Securing the network = Verifying computation

---
### L’infrastructure Ethereum
25000 nœuds contre 7000 pour Bitcoin (31/5/2017)

@snap[west ethermap]
![USA](images/eth1.jpg)
<br>
USA
@snapend

@snap[east ethermap]
![Europe](images/eth2.jpg)
<br>
Europe
@snapend

@snap[south-west span-100]
@size[0.3em](Source: https://twitter.com/peter_szilagyi/status/887272506914213888 - 18/07/2017)
@snapend

--- 

### Smart Contract

 - Un bout de code
 - Déployé/répliqué/distribué 
 - Non modifiable
 - Bien adapté pour gérer des transactions

Note: 
  - Déployé et répliqué sur la même infrastructure de calcul qui héberge et mine la blockchain Ethereum.
 
---

### Smart Contract (suite)

 - Du *bytecode* stocké dans la blockchain
 - Rédigé dans un langage de haut niveau : *Solidity*
 - Compilé avec *solc*
 - Accessible via une adresse codé sur *160 bits*
 - Exécuté dans l'*Ethereum Virtual Machine* (EVM)

Note:
 - ou rédigé en Serpent, Viper, LLL,...)

---

### Le langage Solidity en bref

 - Langage de haut niveau
 - influencé par C++, Python et Javascript
 - Typé statiquement
 - Supporte l'héritage
 - L'appel a des bibliothèques
 - La définition de type complexe par les utilisateurs

---

### EVM <br> Ethereum Virtual Machine

 - Émule une machine 256 bits avec des pseudo-registres
 - Les registres sont émulés par une *stack* virtuel

---

### Ethereum et unités de mesure

 - Ether (ETH) : le nom de la crypto monnaie
 - Wei : une fraction d'Ether (1 ETH = 10^18 Wei)
 
 - GAS : unité de mesure en terme de quantité de calcul 
 - *GAS price* : défini le prix (en Wei) que vous êtes prêt a payer au mineur.
 - *GAS limit* : Quantité maximum de gas que vous êtes prêt à payer pour une transaction.
 
Note:
 - ex: quantité de calcul pour émettre une transaction, 
 - exécuter un smart contract.
 - gas price : prix que vous êtes prêt à payer en tant qu’initiateur d’une transaction.

---

### Analogie

 *GAS limit* est la capacité du réservoir d'une voiture en litre. *GAS price* le prix du litre de carburant.

 - Voiture : 1,50 EUR (prix) par litre (unité)
 - Ethereum : 20 GWei (prix) par GAS (unité)

Pour remplir le réservoir il faut :

 - 50 litres à 1,50 EUR = 75 EUR
 - 21000 unité de GAS à 20 GWei = 0.00042 ETH 

---

 - Fixer un *GAS limit* évite de dépenser une fortune en cas de problème dans un Smart Contract (ex: boucle infinie).
 - Fixer un *GAS limit* trop petit a peu d'intérêt. La quantité de GAS requis est défini par la quantité d'instructions exécuté sur la blockchain.

Note: 
 - https://kb.myetherwallet.com/gas/what-is-gas-ethereum.html   


---

### Questions ?

Cette présentation est disponible sur https://gitpitch.com/jpgelas/EJC







