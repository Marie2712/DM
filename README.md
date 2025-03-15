# DM
DM de programmation objet


# class Carte


    class Carte:
        """Cette classe permet d'afficher de manière particulière les cartes du jeu 
        Parameters 
        ----------
    
        Valeur : __valeur
        Toutes les valeurs que les cartes peuvent prendre.
    
        Couleur : __couleur
        Tous les symboles que peuvent prendre les cartes.

        """
        __VALEURS = ('As', '2', '3', '4','5', '6', '7', '8', '9', '10', 'Valet', 'Dame', 'Roi')
        __COULEURS = ('Pique', 'Coeur', 'Carreau', 'Trêfle')
      
        def __init__(self, valeur, couleur):
            self.__couleur = couleur 
            self.__valeur = valeur 
            if not isinstance(valeur, __VALEURS):
                raise TypeError("La valeur doit être une chaine de caractères.")
            if not isinstance(couleur, __COULEURS):
                raise TypeError("La couleur doit être une chaine de caractères.")

        @property
        def VALEURS(self):
            return self.__VALEURS
  
        @property
        def COULEURS(self):
            return self.__COULEURS
  
        def __str__(self):
              return f"{self.valeur} de {self.couleur}"

        def __repr__(self):
            """Renvoie la représentation officielle d'une carte."""
            return f"Carte('{self.__valeur}', '{self.__couleur}')"
    

        def __eq__(self, valeur1, couleur1):
            """ Renvoie un booléen indiquant si la carte est égale à un autre objet."""
            if not isinstance(other, Carte):
                return False
            return self.__valeur == other.__valeur and self.__couleur == other.__couleur

        def __hash__(self):
            """Permet de rendre les cartes hashables."""
            return hash(repr(self))



# test pour la classe carte

    import re 


    from class 1 import Carte 
    import pytest


    @pytest.mark.parametrize(
    'kwargs, message_erreur',
    [
        ({'valeur': '567'}, "La valeur doit être une chaine de caractères."),
        ({'valeur': {"Bleu"}}, "La valeur doit être une chaine de caractères."),

        ({'couleur': '13579'}, "Le vol doit être une instance de Vol."),
        ({'couleur': ['vol']}, "Le vol doit être une instance de Vol."),
        ]
    )

    def test_carte_init(reservation_kwargs, kwargs, message_erreur):
        reservation_kwargs.update(**kwargs)
        with pytest.raises(TypeError, match=re.escape(message_erreur)):
            Carte(**reservation_kwargs)
    


# class Combinaison

      class Combinaison:

          def __init__(self, cartes:tuple[Carte]):
            self.carte = cartes
            if isinstance(cartes, tuple):
                 raise TypeError("Les cartes doivent être une liste.")
            self.combinaisons = ['brelan', 'carre', 'sequence']
            if cartes not in self.combinaisons:
                  raise ValueError ("ça n'est pas une combinaison")

          def __eq__(self):
           pass

          def est_brelan():
           pass

          def est_carre():
           pass

          def est_sequence():
           pass

          def est_valide():
           pass

          def calcule_nombre_points():
           pass

## class combinaison selon chat 

        def __init__(self, cartes):
        if not isinstance(cartes, tuple):
            raise TypeError("Les cartes doivent être un tuple.")
        self.cartes = cartes

        if len(cartes) < 3:
            raise ValueError("Une combinaison doit contenir au moins 3 cartes.")

    def __eq__(self, autre):
        if isinstance(autre, Combinaison):
            if not self.cartes and not autre.cartes:
                return True
            if len(self.cartes) == len(autre.cartes):
                return set(self.cartes) == set(autre.cartes)
        return False

    def __str__(self):
        return ", ".join(str(carte) for carte in self.cartes)

    def __len__(self):
        return len(self.cartes)

    def est_brelan(self):
        if len(self.cartes) == 3:
            valeurs = [carte.valeur for carte in self.cartes]
            couleurs = [carte.couleur for carte in self.cartes]
            return len(set(valeurs)) == 1 and len(set(couleurs)) == 3
        return False

    def est_carre(self):
        if len(self.cartes) == 4:
            valeurs = [carte.valeur for carte in self.cartes]
            couleurs = [carte.couleur for carte in self.cartes]
            return len(set(valeurs)) == 1 and len(set(couleurs)) == 4
        return False

    def est_sequence(self):
        if len(self.cartes) >= 3:
            couleurs = [carte.couleur for carte in self.cartes]
            valeurs = sorted([self.valeurs.index(carte.valeur) for carte in self.cartes])

            if len(set(couleurs)) == 1 and all(valeurs[i] == valeurs[i-1] + 1 for i in range(1, len(valeurs))):
                return True
            if valeurs == [0, 1, 2]:
                return True
        return False

    def est_valide(self):
        return self.est_brelan() or self.est_carre() or self.est_sequence()

    def calcule_nombre_points(self):
        if not self.est_valide():
            raise ValueError("La combinaison n'est pas valide.")

        points = 0
        for carte in self.cartes:
            if carte.valeur in ['Valet', 'Dame', 'Roi']:
                points += 10
            elif carte.valeur == 'As':
                if self.est_sequence():
                    points += 1
                else:
                    points += 11
            else:
                points += int(carte.valeur)
        return points


# class _ListeCartes

import copy
import random


class _ListeCartes:
    """Cette classe représente une liste de cartes.
    Et elle fournit des fonctionnalités communes à toutes les classes
    caractérisées par une liste de cartes.
    """

    def __init__(self, cartes=None):
        """
        __init__ fonction ainsi :
        - si cartes est None, on initialise avec deux jeux complets de cartes.
        - sinon, si c'est une liste de cartes, on l'utilise telle quelle.
        - sinon, on lève une erreur.
        """
        if cartes is None:
            toutes_cartes = []
            for valeur in Carte._Carte__VALEURS:
                for couleur in Carte._Carte__COULEURS:
                    carte = Carte(valeur, couleur)
                    toutes_cartes.append(carte)

                    self.__cartes = (
                        toutes_cartes * 2
                    )  # Pour qu'il y ait deux jeux de carte

        elif isinstance(cartes, list) and all(
            isinstance(carte, Carte) for carte in cartes
        ):
            self.__cartes = cartes

        else:
            raise ValueError("L'argument doit être None ou une liste de Cartes.")

    @property
    def cartes(self):
        return copy.deepcopy(self.__cartes)

    def __eq__(self, other):
        """
        __eq__ vérifie si deux instances de _ListeCartes sont égales, donc :
        - de même type
        - listes de cartes identiques (ordre inclus)

        Cette fonction renvoie un booléen.
        """
        if not isinstance(other, _ListeCartes):
            return False
        return (
            self.__cartes == other.__cartes
        )  # car on veut que ça return True ou False

    def __str__(self):
        """
        Renvoie la représentation informelle de la liste de cartes.
        Exemple : [As de Pique, Roi de Coeur]
        """
        # Chaque carte s'affiche via son __str__()
        return f"[{', '.join(str(carte) for carte in self.__cartes)}]"

    def __len__(self):
        """
        Renvoie le nombre de cartes dans la liste.
        Permet l'utilisation de len(instance).
        """
        return len(self.__cartes)

    def melanger(self):
        """
        Mélange la liste des cartes.
        """
        random.shuffle(self.__cartes)

    def ajouter_carte(self, carte):
        """
        Ajoute une carte à la fin de la liste.

        Lève une erreur si ce n'est pas une instance de Carte.
        """
        if not isinstance(carte, Carte):
            raise TypeError("L'objet ajouté doit être une instance de Carte.")
        self.__cartes.append(carte)

    def retirer_carte(self, indice=-1):
        """
        Retire et renvoie la carte à l'indice donné (par défaut la dernière carte).

        Lève une erreur si la liste est vide ou si l'indice est invalide.
        """
        if len(self.__cartes) == 0:
            raise IndexError(
                "Il est impossible de retirer une carte car la liste est vide."
            )

        if indice < -len(self.__cartes) or indice >= len(self.__cartes):
            raise IndexError("Indice invalide.")

        carte_retiree = self.__cartes[indice]
        del self.__cartes[indice]
        return carte_retiree


## __LISTES_CARTES selon CHATGPT

    class _ListeCartes:


        def __init__(self, cartes):
                self.cartes = cartes
    
        def __eq__(self, autre):
            return isinstance(autre, _ListeCartes) and self.cartes == autre.cartes
    
        def __str__(self):
            return str([str(carte) for carte in self.cartes])

        def __len__(self):
            return len(self.cartes)

        def melanger(self):
            random.shuffle(self.cartes)

        def ajouter_carte(self, carte):
            if not isinstance(carte, Carte):
                raise ValueError("L'argument doit être une instance de Carte.")
            self.cartes.append(carte)

        def retirer_carte(self, indice):
            if len(self.cartes) == 0:
                raise IndexError("La liste des cartes est vide.")
            if indice < 0 or indice >= len(self.cartes):
                raise IndexError("Indice invalide.")
            return self.cartes.pop(indice)



# class Reserve 

      class Reserve:
      """
      La réserve correspond au paquet de cartes dans lequel les joueurs piochent les cartes.
      Il est possible de distribuer les cartes aux joueurs pour commencer une partie.
      """

          def __init__(self):
        """
        On fait appel à la fonction init de la classe mère __ListeCartes
        """
        super().__init__() 
    
        def distribuer(self, nb_joueurs, indice_premier_joueur, nb_cartes):
            """
            On corrige d'abord toutes les erreurs possibles, 
            mauvais nombre de jouers, mauvais indice
            et nombre de cartes à ditribuer par personnes. 

            Puis on modélise la distribution des cartes
            et on renvoie les mains des joueurs. 
            """
            if nb_joueurs < 2 or nb_joueurs > 5:
                raise ValueError("Le nombre de joueurs doit être compris entre 2 et 5.")
            if indice_premier_joueur < 0 or indice_premier_joueur >= nb_joueurs:
                raise ValueError("L'indice du premier joueur est invalide.")
            if nb_cartes not in ["13/14", "14/15"]:
                raise ValueError("Le nombre de cartes à distribuer doit être '13/14' ou '14/15'.")
            if nb_cartes == "13/14":
                cartes_a_distribuer = 14
            else:
                cartes_a_distribuer = 15
            if len(self.cartes) < nb_joueurs * cartes_a_distribuer:
                raise ValueError("Il n'y a pas assez de cartes dans la réserve.")
            mains = [[] for _ in range(nb_joueurs)]

            compteur = indice_premier_joueur 
            for i in range(cartes_a_distribuer * nb_joueurs):
                joueur = compteur % nb_joueurs 
                carte = self.__cartes.pop(0)
                mains[joueur].append(carte)
                compteur += 1 
        
            return mains 


# class Defause

"""Implémentation de la classe Defausse."""


class Defausse(_ListeCartes):
    """La classe Defausse permet de modéliser la défausse, c'est-à-dire la liste des cartes jetées"""

    def __init__(self):
        """Cette fonction permet d'initialiser la defausse"""
        super().__init__()

    def vider(self, reserve):
        """Cette fonction permet de vider la défausse et de l'ajouter à la fin de la résèrve
        après l'avoir mélangée.
        Ainsi,"""

        if not isinstance(reserve, Reserve):
            raise ValueError("La reserve n'est pas valide car ce n'est pas une Reserve")
        self.melanger()  # On veut mélanger donc on réutilise la fonction mélanger

        for _ in range(len(self.cartes)):
            reserve.ajouter_carte(self.retirer_carte(0))


# class Main

      class Main:

        def __init__(self):
           pass

         def piocher():
           pass

         def jeter():
           pass

         def poser():
           pass
