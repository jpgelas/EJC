### Étude de la consommation énergétique des Smart contracts dans la blockchain Ethereum
<br>
Jean-Patrick Gelas, Hayri Acar, Hind Benfenatki
<br>
Université Lyon 1/LIRIS/INRIA/ENS Lyon
<br>
<br>
@size[1em](Entretiens Jacques Cartier, 12-13 novembre 2018, ENS Lyon)

---
@snap[north-west span-50]
jp@ejc2018:~$ @color[red](whoami)
@snapend

@snap[north-east logo]
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
 - Cryptographie, Hash, Merkle tree,...
 - Algorithmes de consensus (PoW, PoS, DPoS,...)
 - Plateformes d'échanges
 - Comment miner de la crypto monnaie	
 - Comment devenir @color[#e49436](crypto millionaire) ! @fa[smile-o fa-1x]
@ulend
 
---

### Objectifs
 
 - Rappels (Blockchain, Mineurs, ...)
 - Introduction à la blockchain *Ethereum*
 - Les Smart Contracts : Création, déploiement, fonctionnement.
 - Modélisation et maitrise de leur consommation.
 

---

### Rappels : Blockchain

![blockchain](images/blockchain.png)
 - Blockchain : Structure de données simple 
 - La technologie Blockchain : « Base de données » sécurisées et décentralisées. 

@snap[south-west]
@size[0.5em](Démo : https://anders.com/blockchain/)
@snapend



---

### Rappels : Les mineurs

@snap[north-east ethermap]
![8xrig](images/8xgpu-mining-rig-open-air-frame.png)
@snapend

  - Héberge une copie de la blockchain
  - Ajoutent de nouvelles liste de transactions (*i.e.* des blocs) à la chaine.
  - Vérifient l’intégrité de la blockchain
  - Génèrent de nouveaux *coins* (par rétribution)
  - (Exécutent les Smart Contracts) 

---

### Ethereum
@snap[north-east logo]
![LogoEthereum](images/logo-ethereum.png)
@snapend

@quote[Protocole d'échanges décentralisés permettant la création par les utilisateurs de contrats intelligents grâce à un langage Turing-complet.](Wikipedia)

@size[0.5em](
  - Blockchain de *seconde génération*
  - Développée par *Vitalik Buterin*, lancée en juillet 2015.
  - Fréquence moyenne des blocs : 14-15 secondes
  - Symbole boursier : *ETH*
  - Quantité maximale : non limitée
  - Taille des blocs : dynamique
)
Note:
  - Vitalin et aussi Gavin Wood, Joseph Lubin

---
@snap[west span-100]
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

@snap[south-east span-40]
@size[0.3em](https://www.ethernodes.org)
@snapend

--- 

### Smart Contract

@snap[north-east logo]
![LogoSmartContract](images/smartcontract.png)
@snapend


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
 - Compilé (*solc*)
 - Accessible via une adresse codé sur *160 bits*
 - Exécuté dans l'*Ethereum Virtual Machine* (EVM)
<br/>
<br/>
0x71c7656ec7ab88b098defb751b7401b5f6d8976f

Note:
 - ou rédigé en Serpent, Viper, LLL,...)

---
### Code Machine 

```
"opcodes": "PUSH1 0x80 PUSH1 0x40 MSTORE
CALLVALUE DUP1 ISZERO PUSH2 0x10 JUMPI PUSH1 0x0
DUP1 REVERT JUMPDEST POP PUSH1 0x40 MLOAD PUSH1 
0x20 DUP1 PUSH2 0x487 DUP4 CODECOPY DUP2 ADD 
PUSH1 0x40 SWAP1 DUP2 MSTORE SWAP1 MLOAD PUSH1..." 
"object":
"608060405234801561001057600080fd5b5060405160
208061048783398101604090815290516000805460016
0a060020a0319163317808255600160a060020a031681
52600160208190529290209190915560ff81166100606..."
```
---

### Le langage Solidity en bref

@snap[north-east logo]
![LogoSolidity](images/logo-solidity.jpg)
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

    function getMessage () public view returns (string) {
        return message;
    }
    function setMessage (string _message) public payable {
        message = _message;
    }
}
```


---
### 0x (ZRX) token (ERC-20)
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
### Nexium (NXC) token (ERC-20)
```
contract Nexium { 
	...
	function Nexium() {
		initialSupply = 100000000000;
		balanceOf[msg.sender] = initialSupply;
		name = 'Nexium';
		symbol = 'NxC';
		decimals = 3;
		burnAddress = 0x1b32000000000000000000000000000000000000;
	}
	function totalSupply() returns(uint){
		return initialSupply - balanceOf[burnAddress];
	}
	function transfer(address _to, uint256 _value) ...
	function transferFrom(address _from, ...
```
@snap[south-east span-40]
@size[0.3em](http://b2expand.com/nexium-token)
@snapend

---

### EVM

_Ethereum Virtual Machine_

![EVM](images/compressed_evm.png)

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

 - **Ether** (ETH) : le nom de la crypto monnaie
 - **Wei** : une fraction d'Ether (1 ETH = 10^18 Wei)
 - **GAS** : unité de mesure en terme de quantité de calcul 
 - **GAS price** : défini le prix (en Wei) que vous êtes prêt a payer au mineur.
 - **GAS limit** : Quantité maximum de gas que vous êtes prêt à payer pour une transaction.
 
---

### Analogie

  - *GAS limit* : capacité du réservoir d'une voiture en litre. 
  - *GAS price* le prix du litre de carburant.
    - Voiture : 1,50 EUR (prix) par litre (unité)
    - Ethereum : 20 GWei (prix) par GAS (unité)

  - Pour remplir le réservoir il faut :
    - 50 litres à 1,50 EUR = 75 EUR
    - 21000 unités de GAS à 20 GWei = 0.00042 ETH 

---

### En résumé...

 - Fixer un *GAS limit* évite de dépenser une fortune en cas de problème dans un Smart Contract (ex: boucle infinie).
 - La quantité de GAS requis est défini par la quantité d'instructions exécuté sur la blockchain.
 - Fixer un *GAS limit* trop petit a peu d'intérêt.

Note: 
 - https://kb.myetherwallet.com/gas/what-is-gas-ethereum.html   

---

### Coûts des instructions : Exemples

![GasCost1](images/evm-opcode-gas-cost-1.png)
![GasCost2](images/evm-opcode-gas-cost-2.png)

Note: 
 - Limite de GAS par bloc : 8 000 000 GAS
 - Lu ailleur : 4 700 000 gas/block (28/juin/2017)
 - Transaction simple : 21000 GAS

---

### Coûts d'une transaction

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

 - **block time 15 sec**, blocks/min 4
 - block/day 5959, block/year 2 174 897
 - **Block Gas limit 8 000 000**
 - Daily Gas cap 47 668 965 517
 - avg gas/tx 76 364
 - tx/day cap 624 236
 - tx/min 433
 - **tx/sec 7**

Note:
  - VISA annonce 24000 tx/sec -> 1700 en réalité
  - Shasper annonce 13410 tx/sec !!! (Casper + Sharding)

---

### En résumé : Pour le calcul...

  - L'infrastructure Ethereum est un énorme ordinateur Turing complet distribué
  - Ultra tolérant aux pannes
  - Trés mal exploité car tous les noeuds exécutent les mêmes instructions avec les même données.

---

### En résumé : Pour le stockage...

  Par conception on est limité par :  
  - la capacité de stockage des noeuds
  - le débit (90 kB / 15 sec => 50 kbits/s)
  - le prix du GAS qui fluctue en fonction de l'Ether
  - *SSTORE* : 20.000 GAS/Word -> 640.000 GAS/KB
    - 3,5 GWei / GAS -> 0,00224 ETH/KB
    - 200 $/ETH -> 0,448 $/KB

Note:
 - On y stock le hash du fichier seulement (Proof-of-existence)
---

### 448.000 USD / GBytes

(novembre 2018)

---?image=images/clark-howard-253013121&size=contain
@title[90's phones]

---

### Ganache

![GanacheUI](images/ganache-snapshot.png)

---
### Metamask
@snap[west ethermap]
![Metamask](images/metamask-snapshot.png)
@snapend

@snap[east ethermap]
![Metamask-Tx](images/metamask-transaction-snapshot.png)
@snapend

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
 - Par conception la blockchain Ethereum garantie :
   - l'immutabilité des données,
   - l'exécution et l'accès sans censure possible. 
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
 - https://medium.com/coinmonks/storing-on-ethereum-analyzing-the-costs-922d41d6b316

