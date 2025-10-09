Mission 1

objectif allé au donjon
j'ai utilisé la commande cd (pour change directory) o, l'utilise de cette façon "cd /(pour la racin)(nom dossier)"
et ls (pour liste) permet de listé tout les dossier et fichier dans le dossier dans le quelle on ce trouve actuellement

![mission 1 complet](https://github.com/poketoto45/eval_linux/blob/main/image/mission1.png)


Mission 2 

objectif allé dans la cave du donjon

utilisé cd .. environ 5 fois pour revenir dans le chateau (cd .. permet de redessande dans l'aboressance) et fais un cd Cave

![mission 2 complet](https://github.com/poketoto45/eval_linux/blob/main/image/mission2.png)


Mission 3

objectif allé a la racin et allé dans la salle du trone en 2 commande

on comance par fais un cd qui permet d'allé au dossier mère (dossier d'orrigine en général home) puis cd /Chateau/Batiment_principal/Salle_du_trone (permet de dire d'allé dans un dossier a plusieur dossier d'ecarre )

![mission 3 complet](https://github.com/poketoto45/eval_linux/blob/main/image/mission3.png)

Mission 4
objectif créé une hutte et créé un coffre 

on utilise la commande mkdir pour créé un dossier (donc hutte) puis allé dans le dossier et créé un dossier coffre dans le dossier hutte

![mission 4 complet](https://github.com/poketoto45/eval_linux/blob/main/image/mission4.png)

mission 5
objectif supprimé les araigné de la cave

il suffi d'allé dans la cave et de faire rm(permet de suprimé un fichier ou un dossier) araigné_1 araigné_2 araigné_3

![mission 5 complet](https://github.com/poketoto45/eval_linux/blob/main/image/mission5.png)

mission 6
objectif recuppéré tout les piece dans le jardin et les mettre dans le coffre

utilisé la commande mv(permet de deplacé un fichier/dossier) vers un lieux dit dons ce cas la commande "mv piece_1 piece_2 piece_3 ~/Foret/Hutte/Coffre/"

![mission 6 complet](https://github.com/poketoto45/eval_linux/blob/main/image/mission6.png)

mission 7
objectif recupéré les piece caché

pour ce on peux utilisé la commande ls -a (le -a veux dire all donc l'integralité des fichier)
puis a nouveau la commande mv

![mission 7 complet](https://github.com/poketoto45/eval_linux/blob/main/image/mission7.png)

mission 8
objectif supprimé tout les araignee en une commande

pour ce faire on doit utlise le joker * a l'avant et a l'arrier du term araignee qui est commun a chaque fichier (l'asterisque permet de suprimé tout les fichier qui contien le term araignee)

![mission 8 complet](https://github.com/poketoto45/eval_linux/blob/main/image/mission8.png)

mission 9
l'objectif et le meme que le 8 mais avec des araignee caché

il faut juste rajouté un point devant le premier asterisque "rm .*araignee*"

![mission 9 complet](https://github.com/poketoto45/eval_linux/blob/main/image/mission9.png)

mission 10
objectif il faut copier les etandare de la grande salle du chateau

utilise la commande cp (copy) qui permet de copier un fichier/dossier a l'idantique la commande est 
cp etendard* ~/Foret/Hutte/Coffre/

![mission 10 complet](https://github.com/poketoto45/eval_linux/blob/main/image/mission10.png)

mission 11
objectif faire des copi des etandare de la grande salle du chateau

utilise la meme commande l'exercice precedant mais avec *tapicerie* a la place d'"etendard*"

![mission 11 complet](https://github.com/poketoto45/eval_linux/blob/main/image/mission11.png)

mission 12
objectif fais un copi du plus vieux tableau

pour ce il faut utilisé la commande ls -l qui permet de vois les dossier/fichier de voire qui a les droit du se dosier/fichier et de voir ça date de création

![mission 12 complet](https://github.com/poketoto45/eval_linux/blob/main/image/mission12.png)

mission 13
objectif trouve le jour de la conjonction

il faut utilise la commande cal "année" poura affiché un calendrie assez peux lisible

![mission 13 complet](https://github.com/poketoto45/eval_linux/blob/main/image/mission13.png)

mission 14
objectif créé un alias pour la commande ls -a
il faut utilise la commande alias la='ls -A'
la (le alias) le 'ls -A' (la commande a mettre dans le alias)

![mission 14 complet](https://github.com/poketoto45/eval_linux/blob/main/image/mission14.png)

mission 15
objectif fair un journal avec l'editeur nano

il faut utilise la commande nano dans le coffre et ecrire un petit texte dans le fichier jounal.txt créé par la commande
nano journal.txt

![mission 15 complet](https://github.com/poketoto45/eval_linux/blob/main/image/mission15.png)