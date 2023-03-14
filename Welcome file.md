Par les temps qui courent, le télétravail est de mise, mais tout le monde n'est pas placé à la même enseigne. Il y a les grandes entreprises ou les cadres sont équipées d'ordinateurs portables et ou les infrastructures de sécurité existent et ou il suffit juste d'extrapoler pour las salariés qui ne sont pas équipés. Et puis il y a les petites entreprises, voire très petites ou rien n'existe et ou bien souvent le salarié sera contraint de travailler sur son **ordinateur personnel**.
Et dans ce cas on peu se retrouver dans des situations très précaires en termes de sécurité ou de praticité car l'ordinateur familial est généralement utilisé par d'autres personnes, souvent les enfants, ce qui peut rapidement poser des problèmes. On pourrait bien sur isoler une session, mais c'est ingérable et par définition l'intervention sur le PC personnel doit se limiter au strict nécessaire.
La solution bien souvent utilisée conste à permettre au télétravailleur de travailler distance sur son ordinateur de bureau et ainsi conserver son environnement habituel. Pour ce faire on pense d'abord au solutions de type AnyDesk, Team Viewer, voire VNC, solutions simple à mettre en œuvre mais qui offrent peu de confort à l'usage. La seule vrai solution confortable est le RDP. Le problème du RDP c'est sa sécurisation car ce protocole directement exposé sur internet est une véritable passoire dont les méchants hackers sont friands. Micro**soft ne s'est jamais occupé de ce pro**blème pour cet usage, la seule solution proposée est RDS (Remote Desktop Services), une usine à gaz certes efficace mais totalement inadaptée aux TPE. [Royal TS Gateway](https://www.royalapps.com/server/main/features) peut constituer une alternative (il y en a d'autres), mais pas pour de très petites entreprises. 

```yaml
        - conditions: "{{ trigger.id in ['Remote or Keypad'] and is_state('alarm_control_panel.alarmo', 'armed_away') or is_state('alarm_control_panel.alarmo', 'arming') }}"
          sequence:              
            - service: alarm_control_panel.alarm_disarm
              data:
                code: !secret alarm_code
              entity_id:  
                - alarm_control_panel.alarmo
                - alarm_control_panel.visonic_alarm
```

L'autre alternative reste l'utilisation d'un VPN en équipant les postes clients. Il y a plusieurs façons de faire, mais je voulais quelque chose de transparent, facilement administrable et ne m'imposant pas d'intervention ultérieure sur le poste client et ne nécessitant pas l'installation d'un serveur. Je vais donc une fois de plus utiliser Zerotier qui répond à mon besoin.

![vlan-Domain (1)](images/vlan-Domain (1).PNG)!](../../../Downloads/vlan-Domain (1).PNG)

* Pas de serveur à déployer
* Installation minimale sur le poste client
* Gestion des ACL centralisée

Ce n'est pas la façon la plus sécurisée (le port RDP est ouvert entre le client et son PC de bureau), mais on va limiter le risque avec un bon équilibre risque / cout / praticité. 

![](C:\Users\Lionel.SUPTEL\Downloads\ezgif.com-gif-maker (2).png)

### Zerotier
Je vais faire l'impasse sur la mise en œuvre, j'en ai déjà parlé. Ici on va installer le client sur les deux postes à associer et leur figer une IP sur la console d'admin (Zerotier supporte Windows, MacOS, Linux et même Android et IOS).
Ensuite on va s'assurer que seul le trafic RDP du poste client soit autorisé à se connecter au PC de bureau en utilisant les règles dans la console : 
RULES
Ensuite on autorise RDP (le bureau à distance) sur le poste de travail du bureau. Pour ça il faut un Windows Pro (mise à niveau à envisager parfois car les TPE qui vont acheter leur PC à la Fnac ou sur Amazon se retrouvent soue=vent avec une édition Famille de Windows).

Client RDP
ms1 ms2 rts
securisation, pw, no record
Client RDP Mac
pront

