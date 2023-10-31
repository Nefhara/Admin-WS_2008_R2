# -WS_2008_R2_Administration

# -How to launch it
This is a standard bash script, you need to run it with root account.

  `.\Linux_live_collector.sh`

  ![ALT](/Referentiel/launch_1.png)






### Cadre de travail ###
Nom du domaine : dc=test,dc=com
Windows Server 2008 R2 ver.6.1

	=> J'ai supprimé un objet de l'AD : computertest1
	=> Pas de corbeille AD activée
	=> Fonctionne avant / après redémarrage du serveur



### Procédure ###
Lancer ldp.exe en administrateur :
	=> options => Controls
		=> Load Predefined
		=> Return deleted objects
		=> Return recycled objects

	=> Connection => Bind
		=> lancer le bind avec le compte administrateur (compte courant)

	=> View => Tree
		=> BaseDN: dc=test,dc=com

	=> L'AD doit apparaitre
	=> Chercher "CN=Deleted Objects,DC=test,DC=com"
	=> Chercher l'objet en question
	=> Clic droit dessus => Modify

	=> Dans la partie "Edit Entry"
		=> Attribute : isDeleted
		=> Value : laisser vide
		=> Operation : Delete
		=> Enter

	=> La commande apparaît dans la "Entry List"

	=> Dans la partie "Edit Entry"
		=> Attribute : distinguishedName
		=> Value : cn=computer18,cn=Computers,dc=test,dc=com
		=> Operation : Replace
		=> case cochée : Synchronous et Extended
		=> Enter

	=> Faire "Run" et l'objet est restauré dans l'AD
