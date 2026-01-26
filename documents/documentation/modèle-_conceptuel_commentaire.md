# Commentaire du modèle conceptuel

PERSON représente les individus (ici, linguistes). Contient nom, nationalité, genre, langue, field of study et la date de mort.
Elle se situe au centre de mon modèle car plusieurs relations partent d'elle ou y reviennent. 

ORGANISATION représente les institutions (ici principalement des universités). Elle contient un nom et une définition. Elle est liée aux personnes par la relation member of, qui permet de modéliser l'appartenance institutionnelle. (dans mon cas regroupe formation et enseignement)

BIRTH représente la naissance des personne. Elle contient la date de naissance ainsi que le lieu de naissance.

RELATION MEMBERSHIP relie une personne à une organisation. Elle permet de modéliser l'appartenance institutionnelle : une personne peut être membre de plusieurs organisations et une organisation peut accueillir plusieurs personnes. (relation n-n, ce qui justifie l'existance d'une table membership).

RELATION BIRTH relie une personne à un lieu de naissance et une date de naissance. Cela permet de décrire l'origine géographique et temporelle de chaque individu.

