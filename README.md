# Nombre de lignes dans le DataFrame
n <- nrow(df)

# Vérifier si la taille du DataFrame est supérieure à 13 000 000
if (n > 13000000) {
  prob_size <- TRUE
} else {
  prob_size <- FALSE
}

# Taille de chaque mini DataFrame
size <- ceiling(n / 10)

# Découper le DataFrame en 10 parties et assigner à des variables distinctes
periodes <- unique(df$spearman$periode)

for (i in 1:10) {
  start_idx <- (i - 1) * size + 1
  end_idx <- min(i * size, n)
  assign(paste("df_part", i, sep = "_"), df[start_idx:end_idx, ])
}

# Si nécessaire, réduire la taille du dernier DataFrame
if (prob_size) {
  df <- df[1:end_idx, ]
}

# Fonction d'agrégation
agg_function <- function(df_part) {
  aggregate(cbind(top_def_obs, top_def_obs_cnt, nb_def, nb_def_cnt, nb_US) ~ 
              pr + produit + cotation + cr2 + CAV_NBR_JR_DB_T_Cf + CAV_SLD_MOY_T_Cf + 
              ancrel_Cf + activite_Cf + ancnt_Cf + enc_epa_tit_t_Cf + TOP_CII_OUV_T_Cf + 
              periode + score + Critere, 
            data = df_part, FUN = sum)
}

# Agréger les données pour chaque partie
for (i in 1:10) {
  df_part <- get(paste("df_part", i, sep = "_"))
  assign(paste("df_part", i, "agg", sep = "_"), agg_function(df_part))
}

# Combiner toutes les parties agrégées
df_part_agg_tot <- get("df_part_1_agg")
for (i in 2:10) {
  df_part_agg_tot <- rbind(df_part_agg_tot, get(paste("df_part", i, "agg", sep = "_")))
}

# Sauvegarder le résultat final dans un fichier CSV
write.csv(df_part_agg_tot, "C:/Users/A731225/OneDrive - GROUP DIGITAL WORKPLACE/Documents/brute/base_quali_PRO_agrege.csv")
