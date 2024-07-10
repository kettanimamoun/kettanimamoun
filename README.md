# Supposons que 'Studio' est votre DataFrame
# Studio <- read.csv('votre_fichier.csv') # Exemple pour lire le fichier csv

# Nombre de lignes dans le DataFrame
n <- nrow(Studio)

# Taille de chaque mini DataFrame
size <- ceiling(n / 5)

# Découper le DataFrame en 5 parties et assigner à des variables distinctes
for (i in 1:5) {
  start_idx <- (i - 1) * size + 1
  end_idx <- min(i * size, n)
  assign(paste("Studio_part", i, sep = "_"), Studio[start_idx:end_idx, ])
}

# Afficher les mini DataFrames
print(Studio_part_1)
print(Studio_part_2)
print(Studio_part_3)
print(Studio_part_4)
print(Studio_part_5)

