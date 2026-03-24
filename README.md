# Customer-Segmentation-using-K-means-Clustering

1. Elbow Plot Code and Output
   library(ggplot2)
   set.seed(42)
   n <- 200
   customer_data <- data.frame(
   Age           = c(rnorm(60,25,4), rnorm(70,45,6), rnorm(70,60,5)),
   Annual_Income = c(rnorm(60,30000,5000), rnorm(70,65000,8000), rnorm(70,90000,10000)),
   Spending_Score= c(rnorm(60,70,10), rnorm(70,50,12), rnorm(70,30,10)),
   Purchase_Freq = c(rnorm(60,15,3), rnorm(70,8,2), rnorm(70,4,1))
   )
   features_scaled <- scale(customer_data)
   wss <- sapply(1:10, function(k) kmeans(features_scaled, k, nstart=25)$tot.withinss)
   ggplot(data.frame(K=1:10, WSS=wss), aes(K, WSS)) +
   geom_line(color="#2C7BB6", linewidth=1.2) +
   geom_point(color="#D7191C", size=3.5) +
   geom_vline(xintercept=3, linetype="dashed", color="gray40") +
   labs(title="Elbow Plot", x="Number of Clusters (K)", y="Total WSS") +
   theme_minimal()
2. Box Plot Code and Output
   library(ggplot2); library(dplyr); library(tidyr)
   set.seed(42)
   n <- 200
   customer_data <- data.frame(
   Age           = c(rnorm(60,25,4), rnorm(70,45,6), rnorm(70,60,5)),
   Annual_Income = c(rnorm(60,30000,5000), rnorm(70,65000,8000), rnorm(70,90000,10000)),
   Spending_Score= c(rnorm(60,70,10), rnorm(70,50,12), rnorm(70,30,10)),
   Purchase_Freq = c(rnorm(60,15,3), rnorm(70,8,2), rnorm(70,4,1))
   )
   features_scaled <- scale(customer_data)
   set.seed(42)
   customer_data$Cluster <- as.factor(kmeans(features_scaled, 3, nstart=25)$cluster)
   customer_data %>%
   pivot_longer(-Cluster, names_to="Feature", values_to="Value") %>%
   ggplot(aes(Cluster, Value, fill=Cluster)) +
   geom_boxplot(alpha=0.8) +
   facet_wrap(~Feature, scales="free_y") +
   labs(title="Box Plot by Cluster") +
   theme_minimal()
3. Histogram code and output
   library(ggplot2); library(dplyr); library(tidyr)
   set.seed(42)
   n <- 200
   customer_data <- data.frame(
   Age           = c(rnorm(60,25,4), rnorm(70,45,6), rnorm(70,60,5)),
   Annual_Income = c(rnorm(60,30000,5000), rnorm(70,65000,8000), rnorm(70,90000,10000)),
   Spending_Score= c(rnorm(60,70,10), rnorm(70,50,12), rnorm(70,30,10)),
   Purchase_Freq = c(rnorm(60,15,3), rnorm(70,8,2), rnorm(70,4,1))
   )
   features_scaled <- scale(customer_data)
   set.seed(42)
   customer_data$Cluster <- as.factor(kmeans(features_scaled, 3, nstart=25)$cluster)
   customer_data %>%
   pivot_longer(-Cluster, names_to="Feature", values_to="Value") %>%
   ggplot(aes(Value, fill=Cluster)) +
   geom_histogram(bins=20, alpha=0.7, position="identity") +
   facet_wrap(~Feature, scales="free") +
   labs(title="Histogram by Cluster") +
   theme_minimal()
 
