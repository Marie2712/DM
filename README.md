# DM
DM de programmation objet


# class Carte


"""Implémentation de la classe Carte."""


    class Carte:
        """Cette classe permet d'afficher de manière particulière les cartes du jeu
        Parameters
        ----------

    Valeur : __valeur
    Toutes les valeurs que les cartes peuvent prendre.

    Couleur : __couleur
    Tous les symboles que peuvent prendre les cartes.

    """

    __VALEURS = (
        "As",
        "2",
        "3",
        "4",
        "5",
        "6",
        "7",
        "8",
        "9",
        "10",
        "Valet",
        "Dame",
        "Roi",
    )
    __COULEURS = ("Pique", "Coeur", "Carreau", "Trêfle")

    def __init__(self, valeur, couleur):
        self.__couleur = couleur
        self.__valeur = valeur
        if valeur not in self.__VALEURS:
            raise ValueError("La valeur doit être une des valeurs valides.")
        if couleur not in self.__COULEURS:
            raise ValueError("La couleur doit être une des couleurs valides.")

    @property
    def valeur(self):
        return self.__valeur

    @property
    def couleur(self):
        return self.__couleur

    @classmethod
    def VALEURS(cls):
        """Retourne les valeurs possibles des cartes."""
        return cls.__VALEURS

    @classmethod
    def COULEURS(cls):
        """Retourne les couleurs possibles des cartes."""
        return cls.__COULEURS
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



     """Implémentation des tests pour la classe Carte."""
    
    from carte import Carte
    import pytest
    
    
    @pytest.mark.parametrize(
        "valeur, couleur, message_erreur",
        [
            # Nous allons traiter tous les cas ! :
            # 1er cas : la valeur n'est pas une chaîne de caractères
            (345, "Coeur", "La valeur doit être une chaine de caractères."),
            ({"valeur": "Vert"}, "Trêfle", "La valeur doit être une chaine de caractères."),
            # 2ème cas : la couleur n'est pas une chaîne de caractères
            ("As", 13579, "La couleur doit être une chaine de caractères."),
            ("As", ["Coeur"], "La couleur doit être une chaine de caractères."),
            # 3ème cas : la valeur n'est pas valide
            ("10", "Bleu", "La couleur doit être une des couleurs valides."),
            # 4ème : la couleur n'est pas valide
            ("As", "Rose", "La couleur doit être une des couleurs valides."),
        ],
    )
    def test_carte_init(valeur, couleur, message_erreur):
        with pytest.raises((TypeError, ValueError), match=message_erreur):
            Carte(valeur, couleur)
    
    
    @pytest.mark.parametrize(
        "valeur, couleur, str_voulu",
        [
            ("As", "Pique", "As de Pique"),
            ("10", "Coeur", "10 de Coeur"),
            ("Valet", "Carreau", "Valet de Carreau"),
            ("Roi", "Trêfle", "Roi de Trêfle"),
            ("Dame", "Coeur", "Dame de Coeur"),
        ],
    )
    def test_str(valeur, couleur, str_voulu):
        carte = Carte(valeur, couleur)
        assert str(carte) == str_voulu
    
    
    @pytest.mark.parametrize(
        "valeur, couleur, repr_voulu",
        [
            ("As", "Pique", "Carte('As', 'Pique')"),
            ("10", "Coeur", "Carte('10', 'Coeur')"),
            ("Valet", "Carreau", "Carte('Valet', 'Carreau')"),
            ("Roi", "Trêfle", "Carte('Roi', 'Trêfle')"),
            ("Dame", "Coeur", "Carte('Dame', 'Coeur')"),
        ],
    )
    def test_repr(valeur, couleur, repr_voulu):
        carte = Carte(valeur, couleur)
        assert repr(carte) == repr_voulu
    
    
    @pytest.mark.parametrize(
        "valeur1, couleur1, valeur2, couleur2, resultat_voulu",
        [
            ("Roi", "Pique", "Roi", "Pique", True),
            ("10", "Coeur", "10", "Coeur", True),
            ("Valet", "Carreau", "Dame", "Carreau", False),
            ("Roi", "Trêfle", "Roi", "Coeur", False),
            ("Dame", "Coeur", "Dame", "Coeur", True),
        ],
    )
    def test_eq(valeur1, couleur1, valeur2, couleur2, resultat_voulu):
        carte1 = Carte(valeur1, couleur1)
        carte2 = Carte(valeur2, couleur2)
        assert (carte1 == carte2) == resultat_voulu
    
    
    @pytest.mark.parametrize(
        "valeur1, couleur1, valeur2, couleur2, meme_hash",
        [
            ("As", "Pique", "As", "Pique", True),
            ("10", "Coeur", "10", "Coeur", True),
            ("Valet", "Carreau", "Dame", "Carreau", False),
            ("Roi", "Trêfle", "Roi", "Coeur", False),
            ("Dame", "Coeur", "Dame", "Coeur", True),
        ],
    )
    def test_hash(valeur1, couleur1, valeur2, couleur2, meme_hash):
        carte1 = Carte(valeur1, couleur1)
        carte2 = Carte(valeur2, couleur2)
        assert (hash(carte1) == hash(carte2)) == meme_hash

    


# class Combinaison

          from carte import Carte


    class Combinaison:
        """
        Cette classe permet de modéliser les différents types de combinaisons de cartes
    
        parameters
        ------------------------------
    
        cartes : tuple 
            tuple contenant des cartes de jeux
    
        """
        def __init__(self, cartes):
            """
            Cette fonction initie le tuple de cartes 
            """
            if not isinstance(cartes, tuple):
                raise TypeError("Les cartes doivent être un tuple.")
            if not all(isinstance(carte, Carte) for carte in cartes):
                raise TypeError("Tous les éléments du tuple doivent être des instances de Carte.")
            self.__cartes = cartes
    
        @property
        def cartes(self):
            return self.__cartes
    
        @cartes.setter
        def cartes(self, cartes):
            raise AttributeError("L'attribut 'cartes' est en lecture seule.")
    
        def __eq__(self, other):
            """
            On vérifie que ce sont des tuples avec les mêmes cartes, 
            peu importe l'ordre.
            """
            if isinstance(other, Combinaison):
                if not self.__cartes and not other.__cartes:
                    return True
                if len(self.__cartes) == len(other.__cartes):
                    return set(self.__cartes) == set(other.__cartes)
            return False
    
        def __str__(self):
            return ", ".join(f"{carte.valeur} de {carte.couleur.lower()}" for carte in self.__cartes)
    
        def __len__(self):
            return len(self.__cartes)
    
        def __est_brelan(self):
            """
            Vérifie que la combinaison de carte est bien un brelan, 
            il faut que : 
            - Il y a trois cartes
            - les cartes ont la même valeur
            - les trois cartes sont des couleurs toutes différentes
            """
            if len(self.__cartes) == 3:
                valeurs = [carte.valeur for carte in self.__cartes]
                couleurs = [carte.couleur for carte in self.__cartes]
                return len(set(valeurs)) == 1 and len(set(couleurs)) == 3
            else:
                return False
    
        def __est_carre(self):
            """
            Vérfie que la combinaison de carte est bien un carré, 
            il faut que :
            - Il y a quatre cartes
            - les cartes ont la même valeur
            - les quatre cartes sont des couleurs toutes différentes
            """
            if len(self.__cartes) == 4:
                valeurs = [carte.valeur for carte in self.__cartes]
                couleurs = [carte.couleur for carte in self.__cartes]
                return len(set(valeurs)) == 1 and len(set(couleurs)) == 4
            else:
                return False
    
        def est_sequence(self):
            """
            Vérifie que la combinaison de carte est bien une séquence, 
            il faut donc vérifier que :
            - il y a au moins 3 cartes
            - toutes les cartes sont de la même couleur
            - les cartes se suivent
            """
            if len(self.__cartes) >= 3:
                couleurs = [carte.couleur for carte in self.__cartes]
                valeurs = sorted([Carte.VALEURS().index(carte.valeur) for carte in self.__cartes])
    
                if len(set(couleurs)) != 1:
                    return False
    
                if valeurs == [0, 1, 2]:
                    return True
                return all(valeurs[i] == valeurs[i-1] + 1 for i in range(1, len(valeurs)))
            else :
                return False
    
        def est_valide(self):
            """
            Vérifie que la combinaison est soit une séquence, soit un carré, 
            soit un brelan
            """
            if len(self.__cartes) < 3:
                raise ValueError("Une combinaison doit contenir au moins 3 cartes.")
            else:
                return self.__est_brelan() or self.__est_carre() or self.est_sequence()
    
        def calcule_nombre_points(self):
            """
            Permet de calculer les points de chaque combinaison, 
            relève des erreurs si les combinaisons ne sont pas valides.
            """
            if not self.est_valide():
                raise ValueError("La combinaison n'est pas valide.")
    
            points = 0
            for carte in self.__cartes:
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
    
        def get_brelan(self):
            return self.__est_brelan()
    
        def get_carre(self):
            return self.__est_carre()



# test classe combinaison 

        import pytest
        from carte import Carte
        from combinaison import Combinaison 
        
        
        
        @pytest.mark.parametrize(
            "param, erreur_attendue",
            [
                (tuple([Carte("As", "Coeur"), Carte("2", "Trêfle"),
                        Carte("3", "Carreau")]), None),
                (tuple([Carte("As", "Coeur"), Carte("2", "Trêfle")]), ValueError),
                ([Carte("As", "Coeur"), Carte("2", "Trêfle"), Carte("3", "Carreau")],
                 TypeError),
                (tuple([]), ValueError),  # combinaison vide
            ],
        )
        def test_combinaison_init(param, erreur_attendue):
            if erreur_attendue:
                with pytest.raises(erreur_attendue):
                    Combinaison(param)
            else:
                assert Combinaison(param) is not None
        
        
        @pytest.mark.parametrize(
            "param1, param2, resultat_attendu",
            [(tuple([Carte("As", "Coeur"), Carte("2", "Trêfle"),
                     Carte("3", "Carreau")]),
                tuple([Carte("As", "Coeur"), Carte("2", "Trêfle"),
                       Carte("3", "Carreau")]), True),
                (tuple([Carte("As", "Coeur"), Carte("2", "Trêfle")]),)
                (tuple([Carte("As", "Coeur"), Carte("2", "Trêfle")]), True),
                tuple([Carte("As", "Coeur"), Carte("2", "Trêfle")]),
                (tuple([Carte("2", "Trêfle"), Carte("As", "Coeur")]), True),
                (tuple([Carte("As", "Coeur")]), tuple([Carte("As", "Coeur"),
                                                       Carte("2", "Trêfle")]), False),
                (tuple([Carte("As", "Coeur")]), tuple([Carte("As", "Trêfle")]), False),
                ],
        )
        def test_combinaison_eq(param1, param2, resultat_attendu):
            combinaison1 = Combinaison(param1)
            combinaison2 = Combinaison(param2)
            assert (combinaison1 == combinaison2) == resultat_attendu
        
        
        @pytest.mark.parametrize(
            "param, resultat_attendu",
            [
                (tuple([Carte("As", "Coeur"), Carte("2", "Trêfle"), Carte("3", "Carreau")]),
                 "As de coeur, 2 de Trêfle, 3 de carreau"),
                (tuple([Carte("As", "Coeur"), Carte("As", "Trêfle"), Carte("As", "Carreau")]),
                 "As de coeur, As de Trêfle, As de carreau"),
            ],
        )
        def test_combinaison_str(param, resultat_attendu):
            combinaison = Combinaison(param)
            assert str(combinaison) == resultat_attendu
        
        
        @pytest.mark.parametrize(
            "param, resultat_attendu",
            [
                (tuple([Carte("As", "Coeur"), Carte("2", "Trêfle"), Carte("3", "Carreau")]), 3),
                (tuple([Carte("As", "Coeur"), Carte("As", "Trêfle"), Carte("As", "Carreau"),
                        Carte("2", "Carreau")]), 4),
            ],
        )
        def test_combinaison_len(param, resultat_attendu):
            combinaison = Combinaison(param)
            assert len(combinaison) == resultat_attendu
        
        
        @pytest.mark.parametrize(
            "param, est_brelan, est_carre, est_sequence",
            [
                (tuple([Carte("As", "Coeur"), Carte("As", "Trêfle"), Carte("As", "Carreau")]),
                 True, False, False),
                (tuple([Carte("5", "Coeur"), Carte("5", "Trêfle"), Carte("5", "Carreau"),
                        Carte("5", "Pique")]),
                 False, True, False),
                (tuple([Carte("2", "Coeur"), Carte("3", "Coeur"), Carte("4", "Coeur")]),
                 False, False, True),
                (tuple([Carte("As", "Coeur"), Carte("2", "Coeur"), Carte("3", "Coeur")]),
                 False, False, True),
                (tuple([Carte("As", "Coeur"), Carte("6", "Coeur"), Carte("7", "Coeur")]),
                 False, False, False),
            ],
        )
        def test_combinaison_validite(param, est_brelan, est_carre, est_sequence):
            combinaison = Combinaison(param)
            assert combinaison.est_brelan() == est_brelan
            assert combinaison.est_carre() == est_carre
            assert combinaison.est_sequence() == est_sequence
        
        
        @pytest.mark.parametrize(
            "param, est_valide, points_attendus",
            [
                (tuple([Carte("As", "Coeur"), Carte("As", "Trêfle"), Carte("As", "Carreau")]),
                 True, 33),
                (tuple([Carte("10", "Coeur"), Carte("10", "Trêfle"), Carte("10", "Carreau")]),
                 True, 30),
                (tuple([Carte("2", "Coeur"), Carte("3", "Coeur"), Carte("4", "Coeur")]),
                 True, 9),
                (tuple([Carte("10", "Coeur"), Carte("Valet", "Trêfle"),
                        Carte("Roi", "Carreau")]),
                 True, 30),
                (tuple([Carte("As", "Coeur"), Carte("2", "Carreau"), Carte("3", "Pique")]),
                 False, ValueError),
            ],
        )
        def test_combinaison_calcul_points(param, est_valide, points_attendus):
            combinaison = Combinaison(param)
            if est_valide:
                assert combinaison.calcule_nombre_points() == points_attendus
            else:
                with pytest.raises(ValueError):
                    combinaison.calcule_nombre_points()
        
`

# class _ListeCartes

"""Implémentation de la classe _ListeCartes."""

    import copy
    import random
    from carte import Carte


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
    
                    self.__cartes = toutes_cartes * 2  # Pour qu'il y ait deux jeux de carte
    
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
                raise TypeError("L'argument 'carte' doit être une instance de Carte.")
    
            self.__cartes.append(carte)
    
        def retirer_carte(self, indice=-1):
            """
            Retire et renvoie la carte à l'indice donné (par défaut la dernière carte).
    
            Lève une erreur si la liste est vide ou si l'indice est invalide.
            """
            if len(self.__cartes) == 0:
                raise Exception(
                    "La liste de cartes est vide, aucune carte ne peut être retirée."
                )
    
            if not isinstance(indice, int):
                raise ValueError(
                    f"L'indice de la carte à retirer n'est pas valide. "
                    f"L'indice est un entier entre 0 et {len(self.__cartes) - 1} inclus, "
                    f"mais l'indice est '{indice}'."
                )
    
            if indice < 0 or indice >= len(self.__cartes):
                raise ValueError(
                    f"L'indice de la carte à retirer n'est pas valide. "
                    f"L'indice est un entier entre 0 et {len(self.__cartes) - 1} inclus, "
                    f"mais l'indice est {indice}."
                )
    
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

     """Implémentation de la classe Reserve."""

from base import _ListeCartes


class Reserve(_ListeCartes):
    """
    La réserve correspond au paquet de cartes dans lequel les joueurs piochent
    les cartes.
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
            raise ValueError(
                "Le nombre de cartes à distribuer doit être '13/14' ou '14/15'."
            )
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



# test class reserve ( bcp de chat) 

   import pytest
from reserve import Reserve
from carte import Carte


# Test regroupé pour la méthode distribuer
@pytest.mark.parametrize(
    "nb_joueurs, indice_premier_joueur, nb_cartes, cartes_distribuees, erreur_attendue",
    [
        (1, 0, "14/15", None, "Le nombre de joueurs doit être compris entre 2 et 5."),
        # Cas où l'indice du premier joueur est invalide
        (3, 3, "14/15", None, "L'indice du premier joueur est invalide."),
        # Cas où le nombre de cartes à distribuer est invalide
        (
            3,
            0,
            "12/13",
            None,
            "Le nombre de cartes à distribuer doit être '13/14' ou '14/15'.",
        ),
    ],
)
def test_distribuer(
    nb_joueurs, indice_premier_joueur, nb_cartes, cartes_distribuees, erreur_attendue
):
    reserve = Reserve()

    # Créer des cartes fictives pour le test uniquement si la distribution doit réussir
    if erreur_attendue is None:
        # Liste des valeurs valides pour les cartes
        valeurs_valides = [
            "2",
            "3",
            "4",
            "5",
            "6",
            "7",
            "8",
            "9",
            "10",
            "Valet",
            "Dame",
            "Roi",
            "As",
        ]
        cartes = [
            Carte(valeur, "Pique")
            for valeur in valeurs_valides
            for _ in range(nb_joueurs * cartes_distribuees)
        ]
        reserve.ajouter_cartes(cartes)

    if erreur_attendue:
        with pytest.raises(ValueError) as excinfo:
            reserve.distribuer(
                nb_joueurs=nb_joueurs,
                indice_premier_joueur=indice_premier_joueur,
                nb_cartes=nb_cartes,
            )
        assert str(excinfo.value) == erreur_attendue
    else:
        mains = reserve.distribuer(
            nb_joueurs=nb_joueurs,
            indice_premier_joueur=indice_premier_joueur,
            nb_cartes=nb_cartes,
        )

        # Vérifier que chaque joueur a le bon nombre de cartes
        assert len(mains) == nb_joueurs
        assert all(len(main) == cartes_distribuees for main in mains)



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
        
        
# test class Defausse
        
        """Implémentation des tests pour la classe Defausse."""
    
    import pytest
    from carte import Carte
    from defausse import Defausse
    from collections import Counter
    from reserve import Reserve
    
    
    @pytest.mark.parametrize(
        "param, resultat_voulu",
        [
            ([], []),
            ([Carte("Dame", "Trêfle"), Carte("Dame", "Trêfle")]),
            (
                [Carte("Dame", "Trêfle"), Carte("Roi", "Trêfle")],
                [Carte("Dame", "Trêfle"), Carte("Roi", "Trêfle")],
            ),
        ],
    )
    def test_defausse_init(param, resultat_voulu):
        """Teste que vider() lève une erreur si le paramètre n'est pas une Reserve."""
        defausse = Defausse(param)
        assert defausse._Listecarte == resultat_voulu
    
    
    @pytest.mark.parametrize(
        "defausse_init, reserve_init, resultat_union_attendu",
        [
            ([], [], []),
            ([Carte("As", "Pique")], [], [Carte("As", "Pique")]),
            ([], [Carte("As", "Pique")], [Carte("As", "Pique")]),
            (
                [Carte("As", "Pique")],
                [Carte("7", "Coeur")],
                [Carte("As", "Pique"), Carte("7", "Coeur")],
            ),
            (
                [Carte("5", "Trèfle")],
                [Carte("2", "Coeur")],
                [Carte("5", "Trèfle"), Carte("2", "Coeur")],
            ),
        ],
    )
    def test_defausse_vider(defausse_init, reserve_init, resultat_union_voulu):
        defausse = Defausse(defausse_init)
        reserve = Reserve(reserve_init)
        defausse.vider(reserve)
        assert len(defausse == 0)
        nouvelle_reserve = reserve._ListeCartes__cartes
        assert Counter(nouvelle_reserve) == Counter(resultat_union_voulu)

# class Main

      class Main:
        def __init__(self):
            super().__init__()  # on utilise super() pour accéder à la classe mère
    
        def __eq__(self, autre):
            """
            Vérifie l'égalité de la main avec une autre main.
            """
            if not isinstance(autre, Main):
                return False
            return sorted(self.cartes) == sorted(autre.cartes)
    
        def piocher(self, reserve):
            """
            Pioche la première carte de la réserve et l'ajoute à la main.
            """
            if len(reserve) == 0:
                raise ValueError("La réserve est vide.")
            carte = reserve.retirer_carte(0)
            self.ajouter_carte(carte)
    
        def jeter(self, indice, defausse):
            """
            Jette une carte de la main dans la défausse.
            """
            if indice < 0 or indice >= len(self.cartes):
                raise IndexError("Indice invalide.")
            carte = self.retirer_carte(indice)
            defausse.append(carte)
    
        def poser(self, combinaisons):
            """
            Pose une ou plusieurs combinaisons de cartes (brelans, carrés, séquences).
            Vérifie que les combinaisons sont valides.
            """
            if not combinaisons:
                raise ValueError("Aucune combinaison à poser.")
    
            indices = set()
            for combinaison in combinaisons:
                for indice in combinaison:
                    if indice < 0 or indice >= len(self.cartes):
                        raise IndexError(f"Indice {indice} invalide.")
                    if indice in indices:
                        raise ValueError(f"Indice {indice} déjà utilisé.")
                    indices.add(indice)
    
            total_points = 0
            sequence_presente = False
            for combinaison in combinaisons:
                points_combinaison, est_sequence = self.valider_combinaison(combinaison)
                total_points += points_combinaison
                if est_sequence:
                    sequence_presente = True
    
            if not sequence_presente:
                raise ValueError("La première pose doit contenir au moins une séquence.")
            if total_points < 51:
                raise ValueError("La somme des points doit être d'au moins 51 pour la première pose.")
    
            for combinaison in combinaisons:
                for indice in sorted(combinaison, reverse=True):
                    self.retirer_carte(indice)
    
            return combinaisons, total_points

# test main 

    import pytest
    from carte import Carte
    from main import Main
    from defausse import Defausse
    from reserve import Reserve
    
    
    @pytest.fixture
    def setup_mains():
        # Initialisation des objets nécessaires pour les tests
        main_1 = Main()
        main_2 = Main()
    
        # Simuler des cartes et les ajouter à la main
        carte_as = Carte("As", "Coeur")
        carte_2 = Carte("2", "Carreau")
        carte_3 = Carte("3", "Pique")
    
        main_1.ajouter_carte(carte_as)
        main_1.ajouter_carte(carte_2)
        main_1.ajouter_carte(carte_3)
    
        # Créer une main similaire pour main_2
        main_2.ajouter_carte(carte_as)
        main_2.ajouter_carte(carte_2)
        main_2.ajouter_carte(carte_3)
    
        # Initialisation de la réserve et de la défausse pour les tests piocher et jeter
        reserve = Reserve()
        defausse = Defausse()
    
        return main_1, main_2, reserve, defausse
    
    
    @pytest.mark.parametrize(
        "main1, main2, attendu",
        [
            (tuple([Carte("As", "Coeur"), Carte("2", "Carreau"), Carte("3", "Pique")]),
             tuple([Carte("As", "Coeur"), Carte("2", "Carreau"), Carte("3", "Pique")]),
             True),
            (tuple([Carte("As", "Coeur"), Carte("2", "Carreau")]),
             tuple([Carte("As", "Coeur"), Carte("2", "Carreau"), Carte("3", "Pique")]),
             False),
            (tuple([Carte("As", "Coeur"), Carte("2", "Carreau")]),
             tuple([Carte("2", "Carreau"), Carte("As", "Coeur")]),
             True),
        ],
    )
    def test_eq_mains(main1, main2, attendu):
        """Test de la méthode __eq__ pour vérifier l'égalité entre deux mains."""
        main1_obj = Main()
        main2_obj = Main()
    
        for carte in main1:
            main1_obj.ajouter_carte(carte)
    
        for carte in main2:
            main2_obj.ajouter_carte(carte)
    
        assert (main1_obj == main2_obj) == attendu
    
    
    @pytest.mark.parametrize(
        "reserve_cartes, main_cartes, attendu",
        [
            (tuple([Carte("As", "Trêfle")]), tuple([Carte("As", "Coeur"), Carte("2", "Carreau"), Carte("3", "Pique")]), True),
            (tuple([Carte("As", "Trêfle"), Carte("5", "Pique")]), tuple([Carte("As", "Coeur"), Carte("2", "Carreau")]), True),
        ]
    )
    def test_piocher(reserve_cartes, main_cartes, attendu, setup_mains):
        """Test de la méthode piocher pour vérifier qu'une carte est bien ajoutée à la main depuis la réserve."""
        main_1, _, reserve, _ = setup_mains
        for carte in reserve_cartes:
            reserve.ajouter_carte(carte)
    
        for carte in main_cartes:
            main_1.ajouter_carte(carte)
    
        main_1.piocher(reserve)
    
        assert len(main_1.cartes) == len(main_cartes) + 1
        assert main_1.cartes[-1] in reserve_cartes
        assert reserve_cartes[0] not in reserve.cartes
    
    
    @pytest.mark.parametrize(
        "indice, attente_erreur",
        [
            (0, None),
            (10, IndexError),
        ],
    )
    def test_jeter(indice, attente_erreur, setup_mains):
        """Test de la méthode jeter pour vérifier qu'une carte est bien enlevée de la main et ajoutée à la défausse."""
        main_1, _, _, defausse = setup_mains
        carte_as = main_1.cartes[0]
        if attente_erreur:
            with pytest.raises(attente_erreur):
                main_1.jeter(defausse, indice)
        else:
            main_1.jeter(defausse, indice)
            assert carte_as not in main_1.cartes
            assert carte_as in defausse.cartes
    
    
    @pytest.mark.parametrize(
        "indices_combinaison, erreur_attendue",
        [
            ([[0, 1, 2]], None),
            ([[0, 0, 1]], ValueError),
            ([[0, 10]], IndexError),
        ]
    )
    def test_poser(indices_combinaison, erreur_attendue, setup_mains):
        """Test de la méthode poser pour vérifier les erreurs et les comportements de validation."""
        main_1, _, _, _ = setup_mains
        if erreur_attendue:
            with pytest.raises(erreur_attendue):
                main_1.poser(indices_combinaison)
        else:
            combinaisons, points = main_1.poser(indices_combinaison)
            assert len(combinaisons) > 0
            assert points > 0
    
    
    @pytest.mark.parametrize(
        "indices_combinaison, points_attendus",
        [
            ([[0, 1, 2]], 6),
            ([[0, 1]], 3),
        ]
    )
    def test_poser_points(indices_combinaison, points_attendus, setup_mains):
        """Test de la méthode poser pour vérifier le calcul des points."""
        main_1, _, _, _ = setup_mains
        combinaisons, points = main_1.poser(indices_combinaison)
        assert points == points_attendus

