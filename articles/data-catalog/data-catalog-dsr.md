<properties
   pageTitle="Sources de données prises en charge par Azure Data Catalog | Microsoft Azure"
   description="Spécification des sources de données actuellement prises en charge."
   services="data-catalog"
   documentationCenter=""
   authors="trhabe"
   manager="jstrauss"
   editor=""
   tags=""/>
<tags
   ms.service="data-catalog"
   ms.devlang="NA"
   ms.topic="article"
   ms.tgt_pltfrm="NA"
   ms.workload="data-catalog"
   ms.date="01/15/2016"
   ms.author="trhabe"/>

# Sources de données prises en charge par Azure Data Catalog

Les utilisateurs d’Azure Data Catalog peuvent publier des métadonnées à l’aide d’une API publique, en utilisant un outil d’inscription par simple clic, ou en entrant manuellement les informations directement dans le portail Web de Data Catalog. Le tableau ci-dessous résume toutes les sources actuellement prises en charge par le catalogue ainsi que les fonctionnalités de publication disponibles pour chacune d’elles. Sont également répertoriés les outils de données externes que chaque source peut initier à partir du portail. Le deuxième tableau ci-dessous spécifie les propriétés de connexion de chaque source de données sous un angle plus technique.


## Liste des sources de données prises en charge

<table>

    <tr>
       <td><b>Objet de la source de données</b></td>
       <td><b>API</b></td>
       <td><b>Saisie manuelle</b></td>
       <td><b>Outil d’inscription</b></td>
       <td><b>Outils d’ouverture intégrés</b></td>
       <td><b>Remarques</b></td>
    </tr>

    <tr>
      <td>Répertoire Azure Data Lake Store</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Fichier Azure Data Lake Store</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Azure Storage Blob</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td><font size=2>PowerBI</font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Répertoire de stockage Azure</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td><font size=2>PowerBI</font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Répertoire HDFS</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Fichier HDFS</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Table Hive</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td><font size=2>Excel</font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Affichage Hive</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td><font size=2>Excel</font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Table MySQL</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td><font size=2>Excel, Power BI</font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Vue MySQL</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td><font size=2>Excel, Power BI</font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Table de base de données Oracle</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td><font size=2>Excel, Power BI</font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Vue de base de données Oracle</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td><font size=2>Excel, Power BI</font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Autre (élément multimédia générique)</td>
      <td>✓</td>
      <td>✓</td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Table SQL&#160;Data&#160;Warehouse</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td><font size=2>Excel, Power BI</font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Vue SQL&#160;Data&#160;Warehouse</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td><font size=2>Excel, Power BI</font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Dimension SQL&#160;Server Analysis&#160;Services</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td><font size=2>Excel, Power BI</font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Indicateur de performance clé de SQL&#160;Server Analysis&#160;Services</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td><font size=2>Excel, Power BI</font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Mesure SQL&#160;Server Analysis&#160;Services</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td><font size=2>Excel, Power BI</font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Table SQL&#160;Server Analysis&#160;Services</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td><font size=2>Excel, Power BI</font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Rapport SQL&#160;Server&#160;Reporting&#160;Services</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td><font size=2>Browser</font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Table SQL&#160;Server</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td><font size=2>Excel, Power BI</font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Vue SQL&#160;Server</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td><font size=2>Excel, Power BI</font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Table Teradata</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td><font size=2>Excel</font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Vue Teradata</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td><font size=2>Excel</font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Vue SAP Hana</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Table DB2</td>
      <td>✓</td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Vue DB2</td>
      <td>✓</td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Fichier du système de fichiers</td>
      <td>✓</td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Répertoire FTP</td>
      <td>✓</td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Fichier FTP</td>
      <td>✓</td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Rapport HTTP</td>
      <td>✓</td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Point de terminaison HTTP</td>
      <td>✓</td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Fichier HTTP</td>
      <td>✓</td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Jeu d’entités OData</td>
      <td>✓</td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Fonction OData</td>
      <td>✓</td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Table Postgresql</td>
      <td>✓</td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Vue Postgresql</td>
      <td>✓</td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Vue SAP Hana</td>
      <td>✓</td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td> Objet Salesforce</td>
      <td>✓</td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td>Liste SharePoint </td>
      <td>✓</td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

</table>


<br> <br>
## Spécification de référence de la source de données

<table>
    <tr>
       <td><b>Type de source</b></td>
       <td><b>Type racine</b></td>
       <td><b>Type d'objet</b></td>
       <td><b>Contenue dans le type d’objet</b></td>
       <td><b>Structure DSR<b></td>
    </tr>


    <tr>
      <td>Azure Data Lake Store</td>
      <td>Table</td>
      <td>Répertoire</td>
      <td>Data Lake</td>
      <td>
        <font size=2> protocole&#160;: webhdfs
            <br>authentification&#160;: {base, oauth}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; url </font>
      </td>
    </tr>

    <tr>
      <td>Azure Data Lake Store</td>
      <td>Table</td>
      <td>Fichier</td>
      <td>Data Lake</td>
      <td>
        <font size=2> protocole&#160;: webhdfs}
            <br>authentification&#160;: {base, oauth}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; url </font>
      </td>
    </tr>

    <tr>
      <td>Cosmos</td>
      <td>Conteneur</td>
      <td>Cluster virtuel</td>
      <td>N/A</td>
      <td>
        <font size=2> protocole&#160;: cosmos
            <br>authentification&#160;: {base, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; url </font>
      </td>
    </tr>

    <tr>
      <td>SQL&#160;Server&#160;Reporting&#160;Services</td>
      <td>Conteneur</td>
      <td>Serveur</td>
      <td>N/A</td>
      <td>
        <font size=2> protocole&#160;: reporting-services
            <br>authentification&#160;: {windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; version {ReportingService2010} </font>
      </td>
    </tr>

    <tr>
      <td>Azure Storage</td>
      <td>Table</td>
      <td>Blob</td>
      <td>Conteneur</td>
      <td>
        <font size=2> protocole&#160;: azure-blobs
            <br>authentification&#160;: {azure-access-key}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; domain
            <br>&#160;&#160;&#160;&#160;&#160; account
            <br>&#160;&#160;&#160;&#160;&#160; container
            <br>&#160;&#160;&#160;&#160;&#160; name </font>
      </td>
    </tr>

    <tr>
      <td>Azure Storage</td>
      <td>Table</td>
      <td>Répertoire</td>
      <td>Conteneur</td>
      <td>
        <font size=2> protocole&#160;: azure-blobs
            <br>authentification&#160;: {azure-access-key}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; domain
            <br>&#160;&#160;&#160;&#160;&#160; account
            <br>&#160;&#160;&#160;&#160;&#160; container
            <br>&#160;&#160;&#160;&#160;&#160; name </font>
      </td>
    </tr>

    <tr>
      <td>Azure Storage</td>
      <td>Table</td>
      <td>Table</td>
      <td>Azure Storage</td>
      <td>
        <font size=2> protocole&#160;: azure-tables
            <br>authentification&#160;: {azure-access-key}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; domain
            <br>&#160;&#160;&#160;&#160;&#160; account
            <br>&#160;&#160;&#160;&#160;&#160; name </font>
      </td>
    </tr>

    <tr>
      <td>SQL Server Analysis Services</td>
      <td>Conteneur</td>
      <td>Modèle</td>
      <td>N/A</td>
      <td>
        <font size=2> protocole&#160;: analysis-services
            <br>authentification&#160;: {windows, base, anonyme}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database
            <br>&#160;&#160;&#160;&#160;&#160; modèle
            <br>
            <br>*base ou anonyme disponible uniquement via https </font>
      </td>
    </tr>

    <tr>
      <td>Cosmos</td>
      <td>Table</td>
      <td>Stream</td>
      <td>Cluster virtuel</td>
      <td>
        <font size=2> protocole&#160;: cosmos
            <br>authentification&#160;: {base, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; url </font>
      </td>
    </tr>

    <tr>
      <td>Cosmos</td>
      <td>Table</td>
      <td>Ensemble de flux</td>
      <td>Cluster virtuel</td>
      <td>
        <font size=2> protocole&#160;: cosmos
            <br>authentification&#160;: {base, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; url </font>
      </td>
    </tr>

    <tr>
      <td>Cosmos</td>
      <td>Table</td>
      <td>Affichage</td>
      <td>Cluster virtuel</td>
      <td>
        <font size=2> protocole&#160;: cosmos
            <br>authentification&#160;: {base, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; url </font>
      </td>
    </tr>

    <tr>
      <td>Db2</td>
      <td>Conteneur</td>
      <td>Base de données</td>
      <td>N/A</td>
      <td>
        <font size=2> protocole&#160;: db2
            <br>authentification&#160;: {base, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database </font>
      </td>
    </tr>

    <tr>
      <td>Db2</td>
      <td>Table</td>
      <td>Table</td>
      <td>Base de données</td>
      <td>
        <font size=2> protocole&#160;: db2
            <br>authentification&#160;: {base, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database
            <br>&#160;&#160;&#160;&#160;&#160; schema
            <br>&#160;&#160;&#160;&#160;&#160; object </font>
      </td>
    </tr>

    <tr>
      <td>Db2</td>
      <td>Table</td>
      <td>Affichage</td>
      <td>Base de données</td>
      <td>
        <font size=2> protocole&#160;: db2
            <br>authentification&#160;: {base, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database
            <br>&#160;&#160;&#160;&#160;&#160; schema
            <br>&#160;&#160;&#160;&#160;&#160; object </font>
      </td>
    </tr>

    <tr>
      <td>Système de fichiers</td>
      <td>Table</td>
      <td>Fichier</td>
      <td>Serveur</td>
      <td>
        <font size=2> protocole&#160;: file
            <br>authentification&#160;: {aucune, base, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; path </font>
      </td>
    </tr>

    <tr>
      <td>FTP</td>
      <td>Table</td>
      <td>Répertoire</td>
      <td>Serveur</td>
      <td>
        <font size=2> protocol&#160;: ftp
            <br>authentification&#160;: {aucune, base, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; url </font>
      </td>
    </tr>

    <tr>
      <td>FTP</td>
      <td>Table</td>
      <td>Fichier</td>
      <td>Serveur</td>
      <td>
        <font size=2> protocol&#160;: ftp
            <br>authentification&#160;: {aucune, base, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; url </font>
      </td>
    </tr>

    <tr>
      <td>Table SQL&#160;Server Analysis&#160;Services</td>
      <td>Conteneur</td>
      <td>Modèle</td>
      <td>N/A</td>
      <td>
        <font size=2> protocole&#160;: analysis-services
            <br>authentification&#160;: {windows, base, anonyme}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database
            <br>&#160;&#160;&#160;&#160;&#160; modèle
            <br>
            <br>*base ou anonyme disponible uniquement via https </font>
      </td>
    </tr>

    <tr>
      <td>Hadoop Distributed File System</td>
      <td>Table</td>
      <td>Répertoire</td>
      <td>Cluster</td>
      <td>
        <font size=2> protocole&#160;: webhdfs
            <br>authentification&#160;: {base, oauth}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; url </font>
      </td>
    </tr>

    <tr>
      <td>Hadoop Distributed File System</td>
      <td>Table</td>
      <td>Fichier</td>
      <td>Cluster</td>
      <td>
        <font size=2> protocole&#160;: webhdfs
            <br>authentification&#160;: {base, oauth}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; url </font>
      </td>
    </tr>

    <tr>
      <td>Azure Data Lake Store</td>
      <td>Conteneur</td>
      <td>Data Lake</td>
      <td>N/A</td>
      <td>
        <font size=2> protocole&#160;: webhdfs
            <br>authentification&#160;: {base, oauth}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; url </font>
      </td>
    </tr>

    <tr>
      <td>Hive</td>
      <td>Table</td>
      <td>Table</td>
      <td>Base de données</td>
      <td>
        <font size=2> protocole&#160;: hive
            <br>authentification&#160;: {hdinsight, base, nom d’utilisateur}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database
            <br>&#160;&#160;&#160;&#160;&#160; objet
            <br>&#160;&#160;&#160;&#160;&#160; connectionProperties
            <br>&#160;&#160;&#160;&#160;&#160; serverprotocol&#160;: {hive2} </font>
      </td>
    </tr>

    <tr>
      <td>Hive</td>
      <td>Table</td>
      <td>Affichage</td>
      <td>Base de données</td>
      <td>
        <font size=2> protocole&#160;: hive
            <br>authentification&#160;: {hdinsight, base, nom d’utilisateur}
            <br>adresse&#160;: server
            <br>&#160;&#160;&#160;&#160;&#160; database
            <br>&#160;&#160;&#160;&#160;&#160; objet
            <br>&#160;&#160;&#160;&#160;&#160; connectionProperties
            <br>&#160;&#160;&#160;&#160;&#160; serverprotocol&#160;: {hive2} </font>
      </td>
    </tr>

    <tr>
      <td>Azure Storage</td>
      <td>Conteneur</td>
      <td>Azure Storage</td>
      <td>N/A</td>
      <td>
        <font size=2> protocole&#160;: azure-tables
            <br>authentification&#160;: {azure-access-key}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; domain
            <br>&#160;&#160;&#160;&#160;&#160; account </font>
      </td>
    </tr>

    <tr>
      <td>Http</td>
      <td>Conteneur</td>
      <td>Site</td>
      <td>N/A</td>
      <td>
        <font size=2> protocole&#160;: http
            <br>authentification&#160;: {aucune, base, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; url </font>
      </td>
    </tr>

    <tr>
      <td>Http</td>
      <td>Rapport</td>
      <td>Rapport</td>
      <td>Site</td>
      <td>
        <font size=2> protocole&#160;: http
            <br>authentification&#160;: {aucune, base, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; url </font>
      </td>
    </tr>

    <tr>
      <td>Http</td>
      <td>Table</td>
      <td>Point de terminaison</td>
      <td>Site</td>
      <td>
        <font size=2> protocole&#160;: http
            <br>authentification&#160;: {aucune, base, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; url </font>
      </td>
    </tr>

    <tr>
      <td>Azure Storage</td>
      <td>Conteneur</td>
      <td>Conteneur</td>
      <td>N/A</td>
      <td>
        <font size=2> protocole&#160;: azure-blobs
            <br>authentification&#160;: {Azure-Access-Key}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; domain
            <br>&#160;&#160;&#160;&#160;&#160; account
            <br>&#160;&#160;&#160;&#160;&#160; container </font>
      </td>
    </tr>

    <tr>
      <td>MySQL</td>
      <td>Table</td>
      <td>Table</td>
      <td>Base de données</td>
      <td>
        <font size=2> protocole&#160;: mysql
            <br>authentification&#160;: {protocole, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database
            <br>&#160;&#160;&#160;&#160;&#160; object </font>
      </td>
    </tr>

    <tr>
      <td>MySQL</td>
      <td>Table</td>
      <td>Affichage</td>
      <td>Base de données</td>
      <td>
        <font size=2> protocole&#160;: mysql
            <br>authentification&#160;: {protocole, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database
            <br>&#160;&#160;&#160;&#160;&#160; object </font>
      </td>
    </tr>

    <tr>
      <td>Hadoop Distributed File System</td>
      <td>Conteneur</td>
      <td>Cluster</td>
      <td>N/A</td>
      <td>
        <font size=2> protocole&#160;: webhdfs
            <br>authentification&#160;: {base, oauth}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; url </font>
      </td>
    </tr>

    <tr>
      <td>Http</td>
      <td>Table</td>
      <td>Fichier</td>
      <td>Site</td>
      <td>
        <font size=2> protocole&#160;: http
            <br>authentification&#160;: {aucune, base, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; url </font>
      </td>
    </tr>

    <tr>
      <td>Odata</td>
      <td>Conteneur</td>
      <td>Conteneur d’entités</td>
      <td>N/A</td>
      <td>
        <font size=2> protocole&#160;: odata
            <br>authentification&#160;: {aucune, base, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; url </font>
      </td>
    </tr>

    <tr>
      <td>Hive</td>
      <td>Conteneur</td>
      <td>Base de données</td>
      <td>N/A</td>
      <td>
        <font size=2> protocole&#160;: hiveserver2
            <br>authentification&#160;: {hdinsight, base, nom d’utilisateur, aucune}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; port
            <br>&#160;&#160;&#160;&#160;&#160; database </font>
      </td>
    </tr>

    <tr>
      <td>Odata</td>
      <td>Table</td>
      <td>Jeu d’entités</td>
      <td>Conteneur d’entités</td>
      <td>
        <font size=2> protocole&#160;: odata
            <br>authentification&#160;: {aucune, base, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; url
            <br>&#160;&#160;&#160;&#160;&#160; resource </font>
      </td>
    </tr>

    <tr>
      <td>Oracle Database</td>
      <td>Table</td>
      <td>Table</td>
      <td>Base de données</td>
      <td>
        <font size=2> protocole&#160;: oracle
            <br>authentification&#160;: {protocole, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database
            <br>&#160;&#160;&#160;&#160;&#160; schema
            <br>&#160;&#160;&#160;&#160;&#160; object </font>
      </td>
    </tr>

    <tr>
      <td>Oracle Database</td>
      <td>Table</td>
      <td>Affichage</td>
      <td>Base de données</td>
      <td>
        <font size=2> protocole&#160;: oracle
            <br>authentification&#160;: {protocole, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database
            <br>&#160;&#160;&#160;&#160;&#160; schema
            <br>&#160;&#160;&#160;&#160;&#160; object </font>
      </td>
    </tr>

    <tr>
      <td>Odata</td>
      <td>Table</td>
      <td>Fonction</td>
      <td>Conteneur d’entités</td>
      <td>
        <font size=2> protocole&#160;: odata
            <br>authentification&#160;: {aucune, base, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; url
            <br>&#160;&#160;&#160;&#160;&#160; resource </font>
      </td>
    </tr>

    <tr>
      <td>Autres</td>
      <td>Table</td>
      <td>Autres</td>
      <td>N/A</td>
      <td>
        <font size=2> protocole&#160;: generic-asset
            <br>authentification&#160;: {aucune, base, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; assetId </font>
      </td>
    </tr>

    <tr>
      <td>Postgresql</td>
      <td>Conteneur</td>
      <td>Base de données</td>
      <td>N/A</td>
      <td>
        <font size=2> protocole&#160;: postgresql
            <br>authentification&#160;: {base, windows}
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database </font>
      </td>
    </tr>

    <tr>
      <td>Postgresql</td>
      <td>Table</td>
      <td>Table</td>
      <td>Base de données</td>
      <td>
        <font size=2> protocole&#160;: postgresql
            <br>authentification&#160;: {base, windows}
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database
            <br>&#160;&#160;&#160;&#160;&#160; schema
            <br>&#160;&#160;&#160;&#160;&#160; object </font>
      </td>
    </tr>

    <tr>
      <td>Postgresql</td>
      <td>Table</td>
      <td>Affichage</td>
      <td>Base de données</td>
      <td>
        <font size=2> protocole&#160;: postgresql
            <br>authentification&#160;: {base, windows}
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database
            <br>&#160;&#160;&#160;&#160;&#160; schema
            <br>&#160;&#160;&#160;&#160;&#160; object </font>
      </td>
    </tr>

    <tr>
      <td>MySQL</td>
      <td>Conteneur</td>
      <td>Base de données</td>
      <td>N/A</td>
      <td>
        <font size=2> protocole&#160;: mysql
            <br>authentification&#160;: {protocole, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database </font>
      </td>
    </tr>
    <tr>
      <td>SAP Hana</td>
      <td>Table</td>
      <td>Affichage</td>
      <td>Serveur</td>
      <td>
        <font size=2> protocole&#160;: sap hana-sql
            <br>authentification&#160;: {protocole, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; schema
            <br>&#160;&#160;&#160;&#160;&#160; object </font>
      </td>
    </tr>

    <tr>
      <td>Salesforce</td>
      <td>Table</td>
      <td>Object</td>
      <td>N/A</td>
      <td>
        <font size=2> protocole&#160;: salesforce-com
            <br>authentification&#160;: {base, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; loginServer
            <br>&#160;&#160;&#160;&#160;&#160; class
            <br>&#160;&#160;&#160;&#160;&#160; itemName </font>
      </td>
    </tr>

    <tr>
      <td>SharePoint</td>
      <td>Table</td>
      <td>Énumérer</td>
      <td>Site</td>
      <td>
        <font size=2> protocole&#160;: sharepoint-list
            <br>authentification&#160;: {base, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; url </font>
      </td>
    </tr>

    <tr>
      <td>SQL&#160;Data&#160;Warehouse</td>
      <td>Table</td>
      <td>Table</td>
      <td>Base de données</td>
      <td>
        <font size=2> protocole&#160;: tds
            <br>authentification&#160;: {sql, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database
            <br>&#160;&#160;&#160;&#160;&#160; schema
            <br>&#160;&#160;&#160;&#160;&#160; object </font>
      </td>
    </tr>

    <tr>
      <td>SQL&#160;Data&#160;Warehouse</td>
      <td>Table</td>
      <td>Affichage</td>
      <td>Base de données</td>
      <td>
        <font size=2> protocole&#160;: tds
            <br>authentification&#160;: {sql, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database
            <br>&#160;&#160;&#160;&#160;&#160; schema
            <br>&#160;&#160;&#160;&#160;&#160; object </font>
      </td>
    </tr>

    <tr>
      <td>SQL Server</td>
      <td>Table</td>
      <td>Table</td>
      <td>Base de données</td>
      <td>
        <font size=2> protocole&#160;: tds
            <br>authentification&#160;: {sql, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database
            <br>&#160;&#160;&#160;&#160;&#160; schema
            <br>&#160;&#160;&#160;&#160;&#160; object </font>
      </td>
    </tr>

    <tr>
      <td>SQL Server</td>
      <td>Table</td>
      <td>Fonction table</td>
      <td>Base de données</td>
      <td>
        <font size=2> protocole&#160;: tds
            <br>authentification&#160;: {sql, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database
            <br>&#160;&#160;&#160;&#160;&#160; schema
            <br>&#160;&#160;&#160;&#160;&#160; object </font>
      </td>
    </tr>

    <tr>
      <td>SQL Server</td>
      <td>Table</td>
      <td>Affichage</td>
      <td>Base de données</td>
      <td>
        <font size=2> protocole&#160;: tds
            <br>authentification&#160;: {sql, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database
            <br>&#160;&#160;&#160;&#160;&#160; schema
            <br>&#160;&#160;&#160;&#160;&#160; object </font>
      </td>
    </tr>

    <tr>
      <td>Oracle Database</td>
      <td>Conteneur</td>
      <td>Base de données</td>
      <td>N/A</td>
      <td>
        <font size=2> protocole&#160;: oracle
            <br>authentification&#160;: {protocole, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database </font>
      </td>
    </tr>

    <tr>
      <td>SQL Server Analysis Services</td>
      <td>KPI</td>
      <td>KPI</td>
      <td>Modèle</td>
      <td>
        <font size=2> protocole&#160;: analysis-services
            <br>authentification&#160;: {windows, base, anonyme}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database
            <br>&#160;&#160;&#160;&#160;&#160; modèle
            <br>&#160;&#160;&#160;&#160;&#160; objet
            <br>&#160;&#160;&#160;&#160;&#160; objectType&#160;: {Kpi}
            <br>
            <br>*base ou anonyme disponible uniquement via https </font>
      </td>
    </tr>

    <tr>
      <td>SQL Server Analysis Services</td>
      <td>Measure</td>
      <td>Measure</td>
      <td>Modèle</td>
      <td>
        <font size=2> protocole&#160;: analysis-services
            <br>authentification&#160;: {windows, base, anonyme}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database
            <br>&#160;&#160;&#160;&#160;&#160; modèle
            <br>&#160;&#160;&#160;&#160;&#160; objet
            <br>&#160;&#160;&#160;&#160;&#160; objectType&#160;: {Measure} </font>
      </td>
    </tr>

    <tr>
      <td>SQL Server Analysis Services</td>
      <td>Table</td>
      <td>Dimension</td>
      <td>Modèle</td>
      <td>
        <font size=2> protocole&#160;: analysis-services
            <br>authentification&#160;: {windows, base, anonyme}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database
            <br>&#160;&#160;&#160;&#160;&#160; modèle
            <br>&#160;&#160;&#160;&#160;&#160; objet
            <br>&#160;&#160;&#160;&#160;&#160; objectType&#160;: {Dimension} </font>
      </td>
    </tr>

    <tr>
      <td>SAP Hana</td>
      <td>Conteneur</td>
      <td>Serveur</td>
      <td>N/A</td>
      <td>
        <font size=2> protocole&#160;: sap hana-sql
            <br>authentification&#160;: {protocole, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server </font>
      </td>
    </tr>

    <tr>
      <td>Table SQL&#160;Server Analysis&#160;Services</td>
      <td>Table</td>
      <td>Table</td>
      <td>Modèle</td>
      <td>
        <font size=2> protocole&#160;: analysis-services
            <br>authentification&#160;: {windows, base, anonyme}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database
            <br>&#160;&#160;&#160;&#160;&#160; modèle
            <br>&#160;&#160;&#160;&#160;&#160; objet
            <br>&#160;&#160;&#160;&#160;&#160; objectType&#160;: {Table}
            <br>
            <br>*base ou anonyme disponible uniquement via https </font>
      </td>
    </tr>

    <tr>
      <td>SQL&#160;Data&#160;Warehouse</td>
      <td>Conteneur</td>
      <td>Base de données</td>
      <td>N/A</td>
      <td>
        <font size=2> protocole&#160;: tds
            <br>authentification&#160;: {sql, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database </font>
      </td>
    </tr>

    <tr>
      <td>SQL Server</td>
      <td>Conteneur</td>
      <td>Base de données</td>
      <td>N/A</td>
      <td>
        <font size=2> protocole&#160;: tds
            <br>authentification&#160;: {sql, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database </font>
      </td>
    </tr>

    <tr>
      <td>SQL&#160;Server&#160;Reporting&#160;Services</td>
      <td>Rapport</td>
      <td>Rapport</td>
      <td>Serveur</td>
      <td>
        <font size=2> protocole&#160;: reporting-services
            <br>authentification&#160;: {windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; path
            <br>&#160;&#160;&#160;&#160;&#160; version {ReportingService2010} </font>
      </td>
    </tr>

    <tr>
      <td>Teradata</td>
      <td>Conteneur</td>
      <td>Base de données</td>
      <td>N/A</td>
      <td>
        <font size=2> protocole&#160;: teradata
            <br>authentification&#160;: {protocole, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database </font>
      </td>
    </tr>

    <tr>
      <td>Teradata</td>
      <td>Table</td>
      <td>Table</td>
      <td>Base de données</td>
      <td>
        <font size=2> protocole&#160;: teradata
            <br>authentification&#160;: {protocole, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database
            <br>&#160;&#160;&#160;&#160;&#160; object </font>
      </td>
    </tr>

    <tr>
      <td>Teradata</td>
      <td>Table</td>
      <td>Affichage</td>
      <td>Base de données</td>
      <td>
        <font size=2> protocole&#160;: teradata
            <br>authentification&#160;: {protocole, windows}
            <br>adresse&#160;:
            <br>&#160;&#160;&#160;&#160;&#160; server
            <br>&#160;&#160;&#160;&#160;&#160; database
            <br>&#160;&#160;&#160;&#160;&#160; object </font>
      </td>
    </tr>



</table>

<!---HONumber=AcomDC_0121_2016-->