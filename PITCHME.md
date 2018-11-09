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
@size[2em](jp@ejc2018:~$ whoami)
@snapend

@snap[north-east ethermap]
![Avatar](images/avatar-jpgelas.png)
@snapend
<br><br>
```JSON
{
	"first_name" : "Jean-Patrick",
	"last_name" : "Gelas",
	"job" : "Assistant Professor",
	"locations" : [ "Université Claude Bernard - Lyon 1",
			"Avalon/INRIA/ENS Lyon" ],
	"url" : "https://perso.univ-lyon1.fr/jean-patrick.gelas",
	"email" : "jean-patrick.gelas@univ-lyon1.fr",
	"github" : "https://github.com/jpgelas",
	"hobbies" : [ "skydive", "wingsuit" ]
}
```
---

### Agenda

On ne parlera pas de ...

@ul
 - Algorithmes de consensus (PoW, PoS, DPoS,...)
 - Cryptographie, Hash, Merkle tree,...
 - Plateformes d'échange
 - Comment miner de la crypto monnaie	
 - Comment devenir un crypto millionaire ! :-)
@ulend
 
---

### Objectifs
 
 - Rappels (Blockchain, Mineurs, ...)
 - Introduction à la blockchain Ethereum
 - Les Smart Contracts 
   - Création, déploiement, fonctionnement.
 - Modélisation et maitrise de leur consommation

---

### Rappels : Blockchain

![blockchain](images/blockchain.png)
 - Blockchain : Structure de données simple 
 - La technologie Blockchain : « Base de données » sécurisées et décentralisées. 

Démo : https://anders.com/blockchain/

---

### Rappels : Les mineurs

  - Ajoutent de nouvelles liste de transactions (*i.e.* des blocs) à la chaine.
  - Vérifient l’intégrité de la blockchain
  - Génèrent de nouveaux *coins* (par rétribution) 

---

### Ethereum
@snap[north-east ethermap]
![LogoEthereum](images/logo-ethereum.png)
@snapend

@quote[Protocole d'échanges décentralisés permettant la création par les utilisateurs de contrats intelligents grâce à un langage Turing-complet.](Wikipedia)

  - Développée par Vitalik Buterin, lancée en juillet 2015.
  - Fréquence moyenne des blocs : 14-15 secondes
  - Symbole boursier : *ETH*
  - Quantité maximale : non limitée
  - Taille des blocs dynamique

---

@snap[north span-100]
@size[1.2em](L’infrastructure Ethereum)
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
  - green = @golang geth, 
  - orange = @rustlang parity, 
  - white = everything else.


---?image=images/Ethernodes.org.2018-10-28.png&size=contain
@title[Ethernodes (web)]

--- 

### Smart Contract

 - Programme autonome
 - Déployé et répliqué 
 - Non modifiable
 - Adapté pour gérer des transactions

Note: 
  - Programme autinime qui exécute automatiquement des conditions définies au
    préalable et inscrites dans la blockchain.
  - Déployé et répliqué sur la même infrastructure de calcul qui héberge et
    mine la blockchain Ethereum.
 
---

### Smart Contract @size[0.3em](_suite_)

 - Du *bytecode* stocké dans la blockchain
 - Rédigé dans un langage de haut niveau : *Solidity*
 - Compilé avec *solc*
 - Accessible via une adresse codé sur *160 bits*
 - Exécuté dans l'*Ethereum Virtual Machine* (EVM)
<br/>
0x9522618F9664b8d20324a892Cd4d1dBaC0A95fc5

Note:
 - ou rédigé en Serpent, Viper, LLL,...)

---

```
	"object":
"608060405234801561001057600080fd5b5060405160
208061048783398101604090815290516000805460016
0a060020a0319163317808255600160a060020a031681
52600160208190529290209190915560ff81166100606..."
	"opcodes": "PUSH1 0x80 PUSH1 0x40 MSTORE
CALLVALUE DUP1 ISZERO PUSH2 0x10 JUMPI PUSH1 0x0
DUP1 REVERT JUMPDEST POP PUSH1 0x40 MLOAD PUSH1 
0x20 DUP1 PUSH2 0x487 DUP4 CODECOPY DUP2 ADD 
PUSH1 0x40 SWAP1 DUP2 MSTORE SWAP1 MLOAD PUSH1..." 
```
---

### Le langage Solidity en bref

 - Langage de haut niveau
 - influencé par C++, Python et Javascript.
 - Typé statiquement.
 - Supporte l'héritage,
 - l'appel à des bibliothèques,
 - la définition de type complexe par les utilisateurs.

---

```
contract ZRXToken is UnlimitedAllowanceToken {

    uint8 constant public decimals = 18;
    uint public totalSupply = 10**27; // 1 billion tokens, 18 decimal places
    string constant public name = "0x Protocol Token";
    string constant public symbol = "ZRX";

    function ZRXToken() {
        balances[msg.sender] = totalSupply;
    }
}
```

---
 
```
contract Nexium { 
	...
	function Nexium() {
		initialSupply = 100000000000;
		balanceOf[msg.sender] = initialSupply;             // Give the creator all initial tokens                    
		name = 'Nexium';                                 // Set the name for display purposes     
		symbol = 'NxC';                               	 // Set the symbol for display purposes    
		decimals = 3;                          		 // Amount of decimals for display purposes
		burnAddress = 0x1b32000000000000000000000000000000000000;
	}
	function totalSupply() returns(uint){
		return initialSupply - balanceOf[burnAddress];
	}
	function transfer(address _to, uint256 _value) ...
	function transferFrom(address _from, ...
```
B2expand

### EVM

_Ethereum Virtual Machine_

 - (quasi-) Turing complete machine
 - Environnement d'exécution des Smart Contracts
 - Émule une machine 256 bits avec des pseudo-registres
 - Registres émulés par une *stack* virtuel

![EVM](images/compressed_evm.png)

Note:
  - In computing, a machine is said to be Turing complete if it can solve any
    problem that a Turing machine can, given an appropriate algorithm, the necessary time and memory.
  - Pour l'EVM le paramètre limitant est le GAS.
  - https://www.mayowatudonu.com/blockchain/deep-dive-into-evm-intro
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
### Coûts des instructions : Exemples

 - ADD = 3 GAS ; MUL = 5 GAS
 - MLOAD / MSTORE : 
 - SLOAD / SSTORE : 
 - Transaction simple : 21000 GAS
 - Limit de GAS par bloc : 8 000 000 GAS

Note: 
 - Lu ailleur : 4 700 000 gas/block (28/juin/2017)

---

 - the total fee that they pay is equal to gas_price * gas_used.
 - Miners are paid out this fee and so they prioritize transactions with a higher gas price. 
 - The higher gas price you are willing to pay, the faster your transaction will be processed.
 
---?image=images/ethgasstation-10.2018.png&size=contain
@title[EthGasStation (web)]

---


---

### Conclusion

 - Mining ether = Securing the network = Verifying computation

 - With the increased cost and inefficiencies of the blockchain, we gain guarantees of open, censorship resistant code execution and publicly available, immutable data.

 - Maximiser les calculs offchain


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
 - https://etherscan.io/

