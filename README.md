# bwealthy-ancrage — ancrage externe du journal d'accès

Ce dépôt ne contient **aucune donnée client**. Il ne reçoit que des *relevés* :
la tête de chaîne du journal `staff_access_log` de bWealthy, datée et signée par
son propre hash, produite par `scripts/ancrageJournal.mjs` du dépôt `bwealthy`.

## À quoi il sert

Le journal d'accès est chaîné : chaque ligne porte le hash de la précédente. Ça
suffit à détecter une ligne retirée ou réécrite — mais pas à se prémunir de
quelqu'un qui peut réécrire **toute** la chaîne. Avec la main sur la base, on
recalcule les hash depuis la racine et le journal redevient cohérent : amputé,
mais cohérent.

Publier régulièrement la tête de chaîne **hors de portée de celui qui tient la
base** ferme ce trou. Un relevé publié ici hier ne peut plus être aligné sur un
journal réécrit aujourd'hui.

## La règle qui fait tout tenir

> Ce dépôt doit rester **append-only**, et sa clé de publication ne doit jamais
> être détenue par la personne — ou la machine — qui administre la base bWealthy.

Sinon l'ancrage n'a que l'apparence d'une preuve, ce qui est pire que pas
d'ancrage du tout : il inspire une confiance qu'il ne mérite pas.

Concrètement : force-push interdit, suppression de branche interdite, historique
jamais réécrit. Un relevé qui disparaît est en soi le signal d'alerte.
