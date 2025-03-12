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
    __valeur = ('As', '2', '3', '4','5', '6', '7', '8', '9', '10', 'Valet', 'Dame', 'Roi')
    __couleur = ('Pique', 'Coeur', 'Carreau', 'Trêfle')
      
    def __init__(self, valeur, couleur):
    self.__couleur = couleur 
    self.__valeur = valeur 
    if not isinstance(valeur, str):
        raise TypeError("La valeur doit être une chaine de caractères.")
    if valeur not in self.__valeur:
        raise ValueError ('valeur invalide')
    if couleur not in self.__couleur:
        raise ValueError ('couleur invalide')
    
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

# class _ListeCartes

      class _ListeCartes:

          def __init__(self):
           pass

          def __eq__(self):
           pass

          def __str__(self):
           pass

          def __len__():
           pass

          def melanger():
           pass 

          def ajouter_carte():
           pass 

          def retirer_carte():
           pass

# class Reserve 

      class Reserve:

          def __init__(self):
           pass

          def distribuer():
           pass

# class Defause

      class Defausse:

         def __init__(self):
           pass

          def vider():
           pass

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
