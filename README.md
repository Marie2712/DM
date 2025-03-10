# DM
DM de programmation objet


# class Carte

      class Carte:
      """
      """
         def __init__(self, valeurs, couleurs):
              self.valeurs = ['As', '2', '3', '4','5', '6', '7', 
                             '8', '9', '10', 'Valet', 'Dame', 'Roi']
              self.couleurs = ['Pique', 'Cœur', 'Carreau', 'Trèfle']
              if valeur not in self.valeur :
                  raise ValueError ('valeur invalide')
              if couleur not in self.couleur:
                  raise ValueError ('couleur invalide')

        def __init__(self, valeurs, couleurs, valeur, couleur):
    self.__valeurs = ['As', '2', '3', '4','5', '6', '7', 
                         '8', '9', '10', 'Valet', 'Dame', 'Roi']
    self.__couleurs = ['Pique', 'Cœur', 'Carreau', 'Trèfle']
    self.couleur = couleur 
    self.valeur = valeur 
    if valeur not in self.valeur :
        raise ValueError ('valeur invalide')
    if couleur not in self.couleur:
        raise ValueError ('couleur invalide')

        
          def __str__(self):
              return f"{self.valeur} de {self.couleur}"

         def __repr__(self):
            pass

         def __eq__(self):
            pass
    
         def __hash__(self):
             pass

# class Combinaison

      class Combinaison:

          def __init__(self):
           pass

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
