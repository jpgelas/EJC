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

  - Héberge une copie de la blockchain
  - Ajoutent de nouvelles liste de transactions (*i.e.* des blocs) à la chaine.
  - Vérifient l’intégrité de la blockchain
  - Génèrent de nouveaux *coins* (par rétribution)
  - (Exécutent les Smart Contracts) 

---

### Ethereum
@snap[north-east ethermap]
![LogoEthereum](images/logo-ethereum.png)
@snapend

@quote[Protocole d'échanges décentralisés permettant la création par les utilisateurs de contrats intelligents grâce à un langage Turing-complet.](Wikipedia)

  - Blockchain de *seconde génération*
  - Développée par Vitalik Buterin, lancée en juillet 2015.
  - Fréquence moyenne des blocs : 14-15 secondes
  - Symbole boursier : *ETH*
  - Quantité maximale : non limitée
  - Taille des blocs dynamique

Note:
  - Vitalin et aussi Gavin Wood, Joseph Lubin

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
  - 27500 nœuds contre 7000 pour Bitcoin (31/5/2017)
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
  - Programme autonome qui exécute automatiquement des conditions définies au
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

@snap[north-east ethermap]
![LogoSolidity](images/logo-solidity.png)
@snapend

 - Langage de haut niveau
 - influencé par C++, Python et Javascript.
 - Typé statiquement.
 - Supporte l'héritage,
 - l'appel à des bibliothèques,
 - la définition de type complexe par les utilisateurs.

---
### Hello world

```
pragma solidity ^0.4.18;
contract Hello {
    string message = "Default message";
    function setMessage (string _message) public payable {
        message = _message;
    }
    function getMessage () public view returns (string) {
        return message;
    }
}
```


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
http://b2expand.com/nexium-token

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

### En résumé...

 - Fixer un *GAS limit* évite de dépenser une fortune en cas de problème dans un Smart Contract (ex: boucle infinie).
 - La quantité de GAS requis est défini par la quantité d'instructions exécuté sur la blockchain.
 - Fixer un *GAS limit* trop petit a peu d'intérêt.

Note: 
 - https://kb.myetherwallet.com/gas/what-is-gas-ethereum.html   

---

### Coûts des instructions : Exemples

![GasCost1](images/evm-opcode-gas-1.png)
![GasCost2](images/evm-opcode-gas-2.png)

Note: 
 - Lu ailleur : 4 700 000 gas/block (28/juin/2017)
 - ADD = 3 GAS ; MUL = 5 GAS
 - MLOAD / MSTORE : TODO
 - SLOAD / SSTORE : TODO
 - Transaction simple : 21000 GAS
 - Limite de GAS par bloc : 8 000 000 GAS


---

 - Le coût total d'une transaction = *GAS_price x GAS_used* 
 - Les mineurs donne priorité aux transactions avec un *GAS_price* élevé.
 - Plus l'utilisateur est prêt à payer, plus vite la transaction sera traitée.
 
---?image=images/tx_pool_infographic.png&size=contain
@title[MyEtherWallet]

---?image=images/ethgasstation-10.2018.png&size=contain
@title[EthGasStation (web)]

---?image=images/chart.png&size=contain
@title[Ethereum blocks usage]
---

### Performances actuelles

 - block (slot) time  15 sec, blocks/min 4
 - block/day 5959, block/year 2 174 897
 - Block Gas limit 8 000 000
 - Daily Gas cap 47 668 965 517
 - avg gas/tx 76 364
 - tx/day cap 624 236
 - tx/min 433
 - tx/sec 7

Note:
  - VISA annonce 24000 tx/sec -> 1700 en réalité
  - Shasper annonce 13410 tx/sec !!! (Casper + Sharding)

---

### En résumé pour le calcul...

  - L'infrastructure Ethereum est un énorme ordinateur Turing complet distribué
  - Ultra tolérant aux pannes
  - Trés mal exploité car tous les noeuds exécutent les mêmes instructions avec les même données.

---

### En résumé pour le stockage...

  Par conception on est limité par 
  - la capacité de stockage des noeuds
  - le débit limité (90 kB / 15 sec => 50 kbits/s)
  - le prix du GAS qui fluctue en fonction de l'Ether
  - ~200.000 EUR / GBytes

Note:
 - On y stock le hash du fichier seulement (Proof-of-existence)
 

---?image=images/clark-howard-253013121&size=contain
@title[90's phones]


### Ganache

![GanacheUI](images/ganache-snapshot.png)

---
### Metamask

![Metamask](images/metamask-snapshot.png)
![Metamask-Tx](images/metamask-transaction-snapshot.png)

---
### Transaction

![GanacheTX](images/ganache-transaction.png)

---

### Transaction (détail)
![GanacheTX-detail](images/ganache-transaction-detail.png)

---?image=images/remix-snapshot.png&size=contain
@title[Remix snapshot]



---

### Conclusion

 - Miner de l'ether = Sécuriser le réseau = Vérifier les traitements
 - Par conception la blockchain Ethereum garantie l'immutabilité des données,
   l'exécution et l'accès sans censure possible. 
 - Important d'analyser un Smart Contract en terme de consommation de GAS pour maitriser le coût operationnel.

 - Maximiser les calculs et le sockage *offchain*.


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

