Ce fichier contient des exemples de reequetes de fichiers sql:

# 1. Requêtes simples, un seul tableau

```sql
-- Obtenir le tableau complet de livres
SELECT * FROM livre;

--Obtenir de titre et le nombre de pages de tous les livres
SELECT titre, nombre_pages FROM livre;
```
# 2. Requêtes avec un filtre WHERE, un seul tableau

```sql
-- obtenir les livres de plus de 150 pages
SELECT id, titre, nombre_pages FROM livre WHERE nombres_pages>150;

-- obtenir les livres edités à partir de 2021 trié du plus petit au plus grand (ORDER BY ... ASC)
SELECT * FROM livre WHERE date_publication >= '2021-1-1' ORDER BY date_publication ASC;
```

# 3. Requêtes avec un filtre WHERE multiple (plusieurs conditions), un seul tableau
```sql
-- obtenir les livres de plus de 150 pages qui coutent moins de 50 euros

SELECT * FROM livre WHERE nombre_page >= 150 AND prix <= 50;

-- obtenir les livres dequi coutent entre 20 et 80 euros et qui ont plus de 200 pages

SELECT * FROM livre WHERE prix >= 20 AND prix <= 80 AND nombre_pages > 100 ORDER BY prix ASC;

--AUteurs dont le nom commence par J (LIKE)
SELECT * FROM auteur WHERE nom LIKE "J%";

--AUteurs dont le nom finit par s (LIKE)
SELECT * FROM auteur WHERE nom LIKE "%a" ORDER BY nom ASC;

--AUteurs dont le nom contient s (LIKE)
SELECT * FROM auteur WHERE nom LIKE "%s%" ORDER BY nom ASC;

--obtenir les livres dont le prix est inférieur à 20 euros et les livres dont les prix sont supérieur à 40
SELECT * FROM livre WHERE prix prix < 20 OR prix > 40 ORDER BY prix ASC;
```


# 4. Requêtes multi-table simple (INNER JOIN)


```sql
-- obtenir tous les exemplaires des livres et leur état
SELECT livre.id AS livreID, livre.titre, exemplaire.id AS exemplaireID, exemplaire.etat 
FROM livre
INNER JOIN exemplaire
ON livre.id = exemplaire.livre_id
ORDER BY livre.id ASC

```

```sql
-- livres publiés entre 2 dates dont l'auteur est de nationalité x

SELECT livre.id AS livreID, livre.titre, auteur.id AS auteurID, auteur.nom, auteur.nationalite, livre.date_publication 
FROM livre
INNER JOIN auteur_livre
INNER JOIN auteur
ON livre.id = auteur_livre.livre_id AND auteur.id = auteur_livre.auteur_id
WHERE livre.date_publication 
BETWEEN '2000-1-1' AND '2022-1-1'
AND auteur.nationalite = 'Japan'
```









