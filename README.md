# TP1 - JPA / Hibernate avec Base de Données H2

Ce projet est une application Java utilisant **JPA** et **Hibernate** connectée à une base de données en mémoire **H2 Database**, avec visualisation et gestion via la **console Web H2**.

---

## 📌 Fonctionnalités

- Configuration JPA / Hibernate (`persistence.xml`) avec stratégie de schéma `update`.
- Modélisation de l'entité `Produit` avec mapping JPA (`@Entity`, `@Id`, `@GeneratedValue`, etc.).
- Opérations CRUD avec `EntityManager` :
  - Insertion de produits (`em.persist()`)
  - Récupération de tous les produits via requêtes JPQL (`em.createQuery()`)
  - Recherche d'un produit par son identifiant (`em.find()`)
- Intégration et démarrage de la **console Web H2** (`Server.createWebServer`) pour inspecter les tables et exécuter des requêtes SQL interactives.

---

## 🛠️ Technologies Utilisées

- **Java** 8+ / JDK 23
- **Maven** (Gestionnaire de dépendances)
- **JPA 2.2** (`javax.persistence-api`)
- **Hibernate Core 5.6.5.Final**
- **H2 Database 2.1.214**
- **SLF4J**

---

## 🚀 Configuration et Exécution

### 1. Configuration `persistence.xml`

```xml
<persistence-unit name="hibernate-demo" transaction-type="RESOURCE_LOCAL">
    <provider>org.hibernate.jpa.HibernatePersistenceProvider</provider>
    <properties>
        <!-- Connexion H2 -->
        <property name="javax.persistence.jdbc.driver" value="org.h2.Driver"/>
        <property name="javax.persistence.jdbc.url" value="jdbc:h2:mem:testdb;DB_CLOSE_DELAY=-1"/>
        <property name="javax.persistence.jdbc.user" value="sa"/>
        <property name="javax.persistence.jdbc.password" value=""/>

        <!-- Configuration Hibernate -->
        <property name="hibernate.dialect" value="org.hibernate.dialect.H2Dialect"/>
        <property name="hibernate.hbm2ddl.auto" value="update"/>
        <property name="hibernate.show_sql" value="true"/>
        <property name="hibernate.format_sql" value="true"/>
    </properties>
</persistence-unit>
```

### 2. Démarrage de la Console H2

Dans la classe principale `App.java` :
```java
Server.createWebServer("-web", "-webPort", "8082").start();
System.out.println("Console H2 disponible sur : http://localhost:8082");
```

---

## 📊 Résultats d'Exécution

### 1. Sortie Console (Logs Hibernate & Affichage)

```text
Produits insérés avec succès !

Liste des produits :
Produit{id=1, nom='Laptop', prix=999.99, quantite=10, categorie='Informatique', marque='HP'}
Produit{id=2, nom='Smartphone', prix=499.99, quantite=20, categorie='Téléphonie', marque='Samsung'}
Produit{id=3, nom='Tablette', prix=299.99, quantite=15, categorie='Informatique', marque='Lenovo'}

Recherche du produit avec ID=2 :
Produit{id=2, nom='Smartphone', prix=499.99, quantite=20, categorie='Téléphonie', marque='Samsung'}
```

### 2. Accès à la Console Web H2

Ouvrir le navigateur à l'adresse : **[http://localhost:8082](http://localhost:8082)**

- **Driver Class** : `org.h2.Driver`
- **JDBC URL** : `jdbc:h2:mem:testdb`
- **User Name** : `sa`
- **Password** : *(vide)*

### 3. Requêtes SQL de Test

```sql
SELECT * FROM PRODUIT;
```
