# Install packages
install.packages("survival")
install.packages("ggplot2")
install.packages("devtools")

# Load packages
library(survival) 
library(ggplot2)
library(survminer)
library("devtools")
devtools::install_github("kassambara/survminer")

# This line grabs the API helper functions read_civis and write_civis
source_gist('https://gist.github.com/wlattner/9321823060b27885792f4adb9cfd7ffa',filename='civis_r_api.R')

cluster <- 'Civis Databse'

# Load Data
df <- read_civis(Sys.getenv('retention_model_training_data'), database = cluster)

# Question: Do we have some insights from data exploration?

# Let's create a survival curve
fit <- survfit(Surv(date_observed, churned_in_month) ~ 1, data = df)

# Let's create a graph
ggsurvplot(fit)

# Let's improve the graph
g1 <- ggsurvplot(fit, 
           color = "#2E9FDF", 
           ylim=c(.75,1),
           xlab = 'Days since hire', 
           ylab = '% Survival')
g1

# Question: what happens?

# Now with two groups (based on gender)
fit2 <- survfit(Surv(date_observed, churned_in_month) ~ female, data = df)
ggsurvplot(fit2)

# Let's improve the graph
g2 <- ggsurvplot(fit2, legend = "bottom", 
           legend.title = "Gender",
           conf.int = TRUE,
           pval = TRUE,
           ylim=c(.75,1), lty = 1:2, mark.time = FALSE,
           xlab = 'Days since subscription', ylab = '% Survival',
           legend.labs = c("Male", "Female"))
g2

# We can add the risk table
g3 <- ggsurvplot(fit2, legend = "bottom", 
                 legend.title = "Gender",
                 conf.int = TRUE,
                 pval = TRUE,
                 ylim=c(.75,1), lty = 1:2, mark.time = FALSE,
                 xlab = 'Days since subscription', ylab = '% Survival',
                 legend.labs = c("Male", "Female"),
                 risk.table = TRUE, risk.table.y.text.col = TRUE)
g3

# Question: what happens?
