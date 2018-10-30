### Étude de la consommation énergétique des Smart contracts dans la blockchain Ethereum
<br>
Jean-Patrick Gelas, Hayri Acar, Hind Benfenatki
<br>
Université Lyon 1/LIRIS/INRIA/ENS Lyon
<br>
<br>
Entretiens Jacques Cartier, 12-13 novembre 2018, ENS Lyon

---
@snap[north-west]
@size[2em]($ who am i)
@snapend

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
	"email" : "jean-patrick.gelas@univ-lyon1.fr",
	"hobbies" : [ "skydive", "wingsuit" ]
}
```

@snap[north-east ethermap]
![Avatar](images/avatar-jpgelas.png)
@snapend


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
   - génèrent de nouveaux *coins* (par rétribution), 
   - vérifient l’intégrité de la blockchain,
   - ajoutent de nouvelles liste de transaction (des blocs) à la chaine.

Note:
 - Mining ether = Securing the network = Verifying computation

---
@snap[north span-100]
@size[1.5em](L’infrastructure Ethereum)
@snapend

@snap[west ethermap]
![USA](images/eth1.png)
@snapend

@snap[east ethermap]
![Europe](images/eth2.png)
@snapend

@snap[south-west span-100]
@size[0.3em](Source: https://twitter.com/peter_szilagyi/status/887272506914213888 - 18/07/2017)
@snapend

Note:
  - 25000 nœuds contre 7000 pour Bitcoin (31/5/2017)


--- 

### Smart Contract

 - Un bout de code
 - Déployé/répliqué/distribué 
 - Non modifiable
 - Bien adapté pour gérer des transactions

Note: 
  - Déployé et répliqué sur la même infrastructure de calcul qui héberge et mine la blockchain Ethereum.
 
---

### Smart Contract @size[0.3em](_suite_)

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

### EVM

_Ethereum Virtual Machine_

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
 - La quantité de GAS requis est défini par la quantité d'instructions exécuté sur la blockchain.
 - Fixer un *GAS limit* trop petit a peu d'intérêt.

Note: 
 - https://kb.myetherwallet.com/gas/what-is-gas-ethereum.html   

---

### Coûts des instructions

 - Gas is an abstract number that represents the relative complexity of operations.
 - ADD = 3 gas ; MUL = 5 gas
 - Transaction simple : 21000 GWei
 - Nombre maximum de GAS qui peut être mis dans un bloc : 8 000 000 GAS

Note: 
 - Lu ailleur : 4700000 gas/block (28/juin/2017)

---

 - the total fee that they pay is equal to gas_price * gas_used.
 - Miners are paid out this fee and so they prioritize transactions with a higher gas price. 
 - The higher gas price you are willing to pay, the faster your transaction will be processed.
 
---?image=images/ethgasstation-10.2018.png&size=contain

---

### Conclusion

With the increased cost and inefficiencies of the blockchain, we gain guarantees of open, censorship resistant code execution and publicly available, immutable data.

Maximiser les calculs offchain


---

### Questions ?

Cette présentation est disponible sur https://gitpitch.com/jpgelas/EJC

@snap[south-east]
@size[0.5em](:wq!)
@snapend


---

### Liens utiles

 - https://hackernoon.com/ether-purchase-power-df40a38c5a2f
 - OPCODE list + GAS : https://docs.google.com/spreadsheets/d/1m89CVujrQe5LAFJ8-YAUCcNK950dUzMQPMJBxRtGCqs/edit#gid=0
 - Ethernodes (28/10/2018 -> 13320 nodes) : https://www.ethernodes.org/network/1
 - https://www.etherchain.org/charts/averageBlockUtilization


