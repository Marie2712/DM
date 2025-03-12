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

    #autre code possible :
    def __init__(self, valeur, couleur):
        self.valeur = valeur
        self.couleur = couleur
        self.valeurs = [
            'As', '2', '3', '4', '5', '6', '7',
            '8', '9', '10', 'Valet', 'Dame', 'Roi'
            ]
        self.couleurs = ['Pique', 'Cœur', 'Carreau', 'Trèfle']
        if valeur not in self.valeurs:
            raise ValueError('valeur invalide')
        if couleur not in self.couleurs:
            raise ValueError('couleur invalide')
    
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
