#Pasos seguidos para generar el archivo renv.lock de este script

#1) install.packages("renv")

#2)library(renv)

#3) renv::init()

#4) Install the following packages with renv:
#renv::install("maptools@1.1-8") 
#renv::install("ggplot2@3.4.0") 
#renv::install("dplyr@1.0.7")
#renv::install("readxl@1.3.1")




# Beginning of the Script

#If you want to restore this project before executing this script, execute the following command: 
# renv::restore() in the command line

# Load the necessary libraries
library(maptools)
library(ggplot2)
library(dplyr)
library(readxl)

# Create folder to store the results
dir.create("output", showWarnings = FALSE)

#Read the data
bee_data <- read.table("data/WBees.txt", header = TRUE, sep = "\t")
women_data <- read_excel("data/women.xlsx")

# Hacer operaciones sencillas
bee_summary <- bee_data %>%
  group_by(Hive) %>%
  summarise(Avg_CellSize = mean(CellSize, na.rm = TRUE))

women_summary <- women_data %>%
  summarise(across(where(is.numeric), mean, na.rm = TRUE))

# Generar gráfico y guardarlo en la carpeta output
ggplot(bee_data, aes(x = CellSize)) +
  geom_histogram(binwidth = 0.01, fill = "blue", alpha = 0.7) +
  ggtitle("Distribución de CellSize en WBees")
ggsave("output/bee_histogram.png")


write.csv(bee_summary, "output/bee_summary.csv", row.names = FALSE)
write.csv(women_summary, "output/women_summary.csv", row.names = FALSE)

# Congelar el entorno
renv::snapshot()

# Para restaurar el proyecto en otro equipo, ejecutar: 
# renv::restore()

#Esta linea se ha anadido para ver si git push/pull funcionan correctamente

