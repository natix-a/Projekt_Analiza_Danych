# Projekt_Analiza_Danych
# GitGirls 
# W składzie: 
# 1. Natalia Adamczyk 
# 2. Paulina Lackowska
# 3. Wiktoria Gliniecka
# Baza danych: Agencja nieruchomości - raport na temat agencji nieruchomości, dowiedzieć się od czego zależy CENA nieruchomości, czyli domy, mieszkania. 
# Plik: agencja_nieruchomosci


#przedstawienie sie w terminalu
#git config user.email "nattalia.adamczyk@gmail.com"
#git config user.name "Natalka"


install.packages("naniar")
install.packages("ggplot2")
install.packages("dplyr")

library(dplyr)
library(naniar)
library(ggplot2)

getwd()
data <- read.csv("agencja_nieruchomosci.csv")
data
View(data)
# Podgląd danych
head(data)
# Struktura danych
str(data)

n_miss(data$price)
n_miss(data$area)
n_miss(data$bedrooms)
n_miss(data$bathrooms)
n_miss(data$stories)
n_miss(data$mainroad)
n_miss(data$guestroom)
n_miss(data$basement)
n_miss(data$hotwaterheating)
n_miss(data$airconditioning)
n_miss(data$parking)
n_miss(data$prefarea)
n_miss(data$furnishingstatus)

n_complete(data)
prop_miss(data)

prop_miss(data$price)
prop_miss(data$area)
prop_miss(data$bedrooms)
prop_miss(data$bathrooms)
prop_miss(data$stories)
prop_miss(data$mainroad)
prop_miss(data$guestroom)
prop_miss(data$basement)
prop_miss(data$hotwaterheating)
prop_miss(data$airconditioning)
prop_miss(data$parking)
prop_miss(data$prefarea)
prop_miss(data$furnishingstatus)

miss_var_summary(data) 
vis_miss(data)

gg_miss_upset(data, 
              nsets = 3)
              
ggplot(data = data, aes(x = price, y = furnishingstatus)) +
  geom_point(size = 2, color = "cyan4") +
  theme_minimal()
  
# Załaduj ggplot2
library(ggplot2)

# Tworzenie wykresu punktowego
ggplot(data = data, aes(x = area, y = price)) +
  geom_point() +
  labs(
    title = "Cena nieruchomości wg powierzchni",
    x = "Powierzchnia",
    y = "Cena"
  ) +
  theme_minimal()

library(ggplot2)

# Wykres punktowy ceny w zależności od powierzchni
ggplot(data = data, aes(x = area, y = price)) +
  geom_point(aes(color = price), size = 3, alpha = 0.7) +
  scale_color_gradient(low = "blue", high = "red") +
  labs(
    title = "Cena nieruchomości w zależności od powierzchni",
    x = "Powierzchnia (m²)",
    y = "Cena (zł)",
    color = "Cena"
  ) +
  theme_minimal()
  
# Wykres słupkowy pięter w zależności od umeblowania
ggplot(data = data, aes(x = factor(stories), fill = furnishingstatus)) +
  geom_bar(position = "dodge") +
  labs(
    title = "Liczba pięter w zależności od statusu umeblowania",
    x = "Liczba pięter",
    y = "Liczba nieruchomości",
    fill = "Status umeblowania"
  ) +
  theme_minimal() +
  scale_fill_brewer(palette = "Set2")
  
# Wykres boxplot ceny względem klimatyzacji
ggplot(data = data, aes(x = factor(airconditioning), y = price, fill = factor(airconditioning))) +
  geom_boxplot(alpha = 0.7) +
  scale_fill_manual(values = c("skyblue", "orange")) +
  labs(
    title = "Cena nieruchomości w zależności od klimatyzacji",
    x = "Klimatyzacja (0 = brak, 1 = obecna)",
    y = "Cena (zł)",
    fill = "Klimatyzacja"
  ) +
  theme_minimal()
  
  # Histogram cen z uwzględnieniem głównej drogi
ggplot(data = data, aes(x = price, fill = factor(mainroad))) +
  geom_histogram(position = "dodge", bins = 30, alpha = 0.7) +
  scale_fill_manual(values = c("darkgreen", "yellow")) +
  labs(
    title = "Rozkład cen nieruchomości w zależności od obecności przy głównej drodze",
    x = "Cena (zł)",
    y = "Liczba nieruchomości",
    fill = "Główna droga (0 = brak, 1 = obecność)"
  ) +
  theme_minimal()

# Zmiana zmiennych na kategorie, jeśli nie są już ustawione
data <- data %>%
  mutate(
    mainroad = as.factor(mainroad),
    prefarea = as.factor(prefarea),
    airconditioning = as.factor(airconditioning),
    guestroom = as.factor(guestroom),
    basement = as.factor(basement),
    hotwaterheating = as.factor(hotwaterheating),
    furnishingstatus = as.factor(furnishingstatus)
  )

ggplot(data = data, aes(x = mainroad, y = price, fill = mainroad)) +
  geom_boxplot(alpha = 0.7) +
  scale_fill_manual(values = c("darkgreen", "yellow")) +
  labs(
    title = "Cena nieruchomości w zależności od obecności głównej drogi",
    x = "Główna droga (0 = brak, 1 = obecność)",
    y = "Cena (zł)",
    fill = "Główna droga"
  ) +
  theme_minimal()


ggplot(data = data, aes(x = prefarea, y = price, fill = prefarea)) +
  geom_boxplot(alpha = 0.7) +
  scale_fill_manual(values = c("skyblue", "orange")) +
  labs(
    title = "Cena nieruchomości w zależności od preferowanej lokalizacji",
    x = "Preferowana lokalizacja (0 = brak, 1 = obecność)",
    y = "Cena (zł)",
    fill = "Preferowana lokalizacja"
  ) +
  theme_minimal()

ggplot(data = data, aes(x = airconditioning, y = price, fill = airconditioning)) +
  geom_boxplot(alpha = 0.7) +
  scale_fill_manual(values = c("blue", "red")) +
  labs(
    title = "Cena nieruchomości w zależności od klimatyzacji",
    x = "Klimatyzacja (0 = brak, 1 = obecność)",
    y = "Cena (zł)",
    fill = "Klimatyzacja"
  ) +
  theme_minimal()
  
  ggplot(data = data, aes(x = guestroom, y = price, fill = guestroom)) +
  geom_boxplot(alpha = 0.7) +
  scale_fill_manual(values = c("purple", "green")) +
  labs(
    title = "Cena nieruchomości w zależności od pokoju gościnnego",
    x = "Pokój gościnny (0 = brak, 1 = obecność)",
    y = "Cena (zł)",
    fill = "Pokój gościnny"
  ) +
  theme_minimal()
  
  ggplot(data = data, aes(x = basement, y = price, fill = basement)) +
  geom_boxplot(alpha = 0.7) +
  scale_fill_manual(values = c("grey", "brown")) +
  labs(
    title = "Cena nieruchomości w zależności od piwnicy",
    x = "Piwnica (0 = brak, 1 = obecność)",
    y = "Cena (zł)",
    fill = "Piwnica"
  ) +
  theme_minimal()

ggplot(data = data, aes(x = hotwaterheating, y = price, fill = hotwaterheating)) +
  geom_boxplot(alpha = 0.7) +
  scale_fill_manual(values = c("cyan", "pink")) +
  labs(
    title = "Cena nieruchomości w zależności od ogrzewania ciepłą wodą",
    x = "Ogrzewanie ciepłą wodą (0 = brak, 1 = obecność)",
    y = "Cena (zł)",
    fill = "Ogrzewanie"
  ) +
  theme_minimal()

ggplot(data = data, aes(x = furnishingstatus, y = price, fill = furnishingstatus)) +
  geom_boxplot(alpha = 0.7) +
  scale_fill_brewer(palette = "Set2") +
  labs(
    title = "Cena nieruchomości w zależności od statusu umeblowania",
    x = "Status umeblowania",
    y = "Cena (zł)",
    fill = "Umeblowanie"
  ) +
  theme_minimal()
  




