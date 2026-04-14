#uni 
Se voglio minimizzare il blocco complessi che utilizzo devo procedere in maniera strettamente decrescente di dimensione dei blocchi assegnati.

| subnet | needed    | allocated | address      | mask | dec mask        | assignable range            | broadcast    |
| ------ | --------- | --------- | ------------ | ---- | --------------- | --------------------------- | ------------ |
| LanC   | 400 hosts | 510       | 172.16.0.0   | /23  | 255.255.254.0   | 172.16.0.1 - 172.16.1.254   | 172.16.1.255 |
| LanA   | 110       | 126       | 172.16.2.0   | /25  | 255.255.255.128 | 172.16.2.1 - 172.16.2.126   | 172.16.2.127 |
| LanD   | 90        | 126       | 172.16.2.128 | /25  | 255.255.255.128 | 172.16.2.129 - 172.16.2.254 | 172.16.2.255 |
# Route Summarization
Qui l'obiettivo è favorire la summarization e quindi il routing.