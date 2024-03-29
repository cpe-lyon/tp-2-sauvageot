# Compte rendu TP2  <img src="https://image.flaticon.com/icons/svg/518/518713.svg" height="50" alt="Zozor" /> | Geoffrey Sauvageot-Berland 

## Exercice 1 

### **1. Dans quels dossiers bash trouve-t-il les commandes tapées par l’utilisateur ?**

<code> printenv PATH </code>

### **2. Quelle variable d’environnement permet à la commande cd tapée sans argument de vous ramener dans votre répertoire personnel ?**

<code> printenv HOME</code> <br>
<code> /home/brlndtech </code> <br>

### **3. Explicitez le rôle des variables LANG, PWD, OLDPWD, SHELL et _.**

<code> printenv LANG  : fr_FR.UTF-8 </code> <br> 
<code> La variable d'environement LANG : La variable d'environnement « LANG » détermine la langue que les logiciels utilisent pour communiquer avec l'utilisateur </code> <br> <br>

<code> printenv PWD </code> <br>
<code> PWD : cette variable d'environement contient le chemin du répertoire courant. </code> <br> <br>

<code> printenv OLDPWD </code> <br>
<code> La variable d'envirronement $OLDPWD contient le chemin absolu vers le répertoire courant précédament visité </code><br>
<br>

<code> printenv SHELL : /bin/bash</code> <br>
<code> la variable d'environnement SHELL permet d'afficher le chemin du programme /bin/bash </code>


### **4. Créez une variable locale MY_VAR (le contenu n’a pas d’importance). Vérifiez que la variable existe**

<code> MY_VAR=" je suis une variable local"; </code> <br>
<code>
    echo $MY_VAR ; <br>
    "je suis une variable local" 
</code> <br>

### **5. Tapez ensuite la commande bash. Que fait-elle ? La variable MY_VAR existe-t-elle ? Expliquez. A la fin de cette question, tapez la commande exit pour revenir dans votre session initiale.**

<code> bash </code> <br>
<code> echo $MY_VAR (ne retourne rien) </code>

La variable MY_VAR n'éxiste plus, car elle à été "éffacée". La commande bash permet de relancer la consol du shell, et donc la variable local a été éliminé. 


### **6. Transformez MY_VAR en une variable d’environnement et recommencez la question précédente. Expliquez**

``` 
export MY_VAR="coudcoud"
bash
echo $MY_VAR ;
" coudcoud "
``` 

le fait d'utiliser export MY_VAR (...) ne crée pas une variable LOCAL, mais une variable GLOBAL. Elle reste donc dans le shell de manière permanente 

### **7.Créer la variable d’environnement NOMS ayant pour contenu vos noms de binômes séparés par un espace Afficher la valeur de NOMS pour vérifier que l’affectation est correcte**

``` bash
export NOMS="geoffrey bezet" 
printenv NOMS
``` 

### **8. Ecrivez une commande qui affiche ”Bonjour à vous deux, binôme1 binôme2 !” (où binôme1 et binôme2 sont vos deux noms) en utilisant la variable NOMS**

<code> echo "bonjour a vosu deux, $NOMS" </code> 

Pour rappel, NOM est une variable global édité juste avant 

### **9. Quelle différence y a-t-il entre donner une valeur vide à une variable et l’utilisation de la commande unset ?** 

<code> unset NOM <br> </code>
-> la variable qui a une valeur vide est toujours utilisable alors que grâce à la commande unset -> permet d'enlever la variable d'environnement NOM crée en amont. (On ne  pourrat plus l'afficher vu qu'elle n'éxiste plus )

### **10 Utilisez la commande echo pour écrire exactement la phrase : $HOME = chemin (où chemin est votre dossier personnel d’après bash)**

<code> echo "$HOME = chemin (où chemin est votre dossier personnel d’après bash)" </code> 

## Exercice 2 Programmation Bash

### **Vous enregistrerez vos scripts dans un dossier script que vous créerez dans votre répertoire personnel. Tous les scripts sont bien entendu à tester. Ajoutez le chemin vers script à votre PATH de manière permanente** 
```
cd ~  
mkdir script  
cd script 
touch testpasswd.sh 
nano testpasswd.sh 
chmod 700 testpasswd.sh 

```

```
#!/bin/bash 
defaultPassword="coud"; 
passwordASaisir=""; 
read -p  "Saisissez votre mdp :  " -s passwordASaisir # -p  
# -p pour afficher du texte "" -s = naffiche pas la saisie de user 
if [ $passwordASaisir = $defaultPassword ]; then 
       echo -e "\n C'esttttttttt biiien ! password accepted :) " 
else 
        echo -e "\n wrong password" 
fi  

```


## Exercice 3. Expressions rationnelles


```
#!/bin/bash
function is_number() # fonction qui permet de savoir si un nombre est de type réel ou non 
{
  re='^[+-]?[0-9]+([.][0-9]+)?$'
  if ! [[ $1 =~ $re ]] ; then
          return 1
  else
          return 0
  fi
}
is_number $1
  if [ $? = 0 ]; then
          echo "Le nombre est de type réel (double)"
  else
          echo "Le nombre n'est pas de type réel (Vous avez entré une char) "
  fi 
```
## Exercice 4. Contrôle d’utilisateur 
### Écrivez un script qui vérifie l’existence d’un utilisateur dont le nom est donné en paramètre du script. Si le script est appelé sans nom d’utilisateur, il affiche le message : ”Utilisation : nom_du_script nom_utilisateur”, où nom_du_script est le nom de votre script récupéré automatiquement (si vous changez le nom de votre script, le message doit changer automatiquement) 

```
#/bin/bash
# ./script <username>
if [ $(id -u $1) ]; then
   echo -e "L'utilisateur est reconnu \n";
   echo -e "Information Complémentaire : `id $1`"
else
  echo "L'utilisateur n'est pas reconnu";
fi
```

## Exercice 5. Factoriel   
```
#!/bin/sh
# pour éxécuter ./pgm.sh <parametre int>
fact() {
        nombreParametre=$1
        if [ $nombreParametre -eq 0 ]; then # si nombreParametre est = 0
          echo 1
        elif [ $nombreParametre -lt 0 ]; then # sinon si nombreParametre est < 0 
          echo "Erreur Votre nom doit être > 0"
        else sinon si nombreParametre est > 0 
                echo $(( nombreParametre * `fact $(( nombreParametre - 1 ))` ))
        fi
}
echo "Resultat : $(fact $1)"
```


## Exercice 6. Le juste prix
```

#!/bin/sh
nombreAleatoire=$((1 + RANDOM % 1000))
# nombreASaisir="";
echo $nombreAleatoire;
  read -p  "Saisissez un nombre entre 1 et 1000 : "  nombreASaisir # -p
  while [  $nombreASaisir -ne $nombreAleatoire ]
  do                
      if [ $nombreASaisir -gt $nombreAleatoire ]; then  
            echo -e "\n Trop grand !! "
            read -p  "saisi à nouveau : "  nombreASaisir # -p affiche un
      elif [ $nombreASaisir -lt $nombreAleatoire ]; then
            echo -e "\nTrop petit !"
            read -p  "saisi à nouveau : "  nombreASaisir # -p affiche un
      fi
  done
echo "gagné !!! Le nombre était : " $nombreAleatoire 
```
## Exercice 7. Statistiques

```
function is_number()
{
        re='^[+-]?[0-9]+([.][0-9]+)?$'
        if ! [[ $1 =~ $re ]] ; then
                return 1
        else
                return 0
        fi
}

min=$1
max=$1
moy=$1
somme=0
while (("$#"));
do
        is_number $1
        if [ $? = 0 ]; then
                if [ $1 -lt -100 ] || [ $1 -gt 100 ]; then
                        echo "$1 est un nb qui est < -100 > 100, (ne va pas"
                else
                        if [ $1 -gt $max ]; then
                                max=$1
                        fi

                        if [ $1 -lt $min ]; then
                                min=$1
                        fi

                        somme=$(($somme+$1))
                        ((i++))
                fi
        else
                echo "$1 !!! ce n'est pas un nombre"
        fi
        shift #!
done
moy=$(($somme/$i))

echo "La moyenne =  $moy"
echo "Le nombre max = $max"
echo "Le nombre < =  $min"

```






