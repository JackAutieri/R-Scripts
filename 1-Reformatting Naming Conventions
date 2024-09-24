## Jack Autieri
## The purpose of this file is to restructure the naming format of "LastName, FirstName MiddleName"
## In an Excel cell divide them into 3 individual columns with their respective information

library(dplyr)
library(readxl)
library(writexl)

# Read the Excel file
df <- read_excel("Include File Path Here")
View(df)

# Function to split the Name column into First, Middle, and Last Names
split_names <- function(name) {
  parts <- strsplit(name, ", ")[[1]]  
  if (length(parts) == 2) {
    name_parts <- strsplit(parts[2], " ")[[1]]  
    first_name <- name_parts[1]  
    middle_name <- ifelse(length(name_parts) > 1, paste(name_parts[-1], collapse = " "), NA)  
    return(list(FirstName = first_name, MiddleName = middle_name, LastName = parts[1]))
  } else {
    return(list(FirstName = name, MiddleName = NA, LastName = NA))  # Handle cases where the format is not as expected
  }
}

# Apply the function and create new columns for First, Middle, and Last Names
df <- df %>%
  mutate(NameParts = lapply(Name, split_names)) %>%
  mutate(FirstName = sapply(NameParts, function(x) x$FirstName),
         MiddleName = sapply(NameParts, function(x) x$MiddleName),
         LastName = sapply(NameParts, function(x) x$LastName)) %>%
  select(-NameParts)
  


print(df)

# Write File path you would like the data frame to be downloaded to
write_xlsx(df, "Include File Path here")

# Confirm export by printing a success message
print("Data exported successfully to your File System")
