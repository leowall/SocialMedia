# SocialMedia
Analysis of Social Media - Twitter, Facebook and YouTube comments for MCC

Analysis using SocialMediaLab package to pull in Twitter data via API relating to MCC Twitter feed
Network and text analysis of data
Add in package to always look at the same version of the package

# Set working directory
setwd("U:/R")

# Specify library path
.libPaths("U:/R/library")

# Load Packages - need to amend either to check if loaded or load from elsewhere
library(SocialMediaLab)
library(igraph)
library(magrittr)
library(tm)
library(lattice)
library(wordcloud)
library(readr)

# read in the Twitter csv data from file - need to change to tidyverse
MCC_Twitter <- read.csv("G:/CEX/Planning/Planning Studies/studies/Social Media Analysis/Aug_04_12_25_00_2017_BST_@ManCityCouncil_TwitterData.csv", header = TRUE, sep = ",", row.names = "X")
UoM_Twitter <- read.csv("G:/CEX/Planning/Planning Studies/studies/Social Media Analysis/Aug_04_14_03_59_2017_BST_@OfficialUoM_TwitterData.csv", header = TRUE, sep = ",", row.names = "X")

class(MCC_Twitter)

# convert text coding
MCC_Twitter$text <- iconv(MCC_Twitter$text, to = 'utf-8')

# create Actor file
MCC_Twitter_Actor <- MCC_Twitter %>% Create("Actor")

# plot network graph of actors
plot(MCC_Twitter_Actor,vertex.shape="none",edge.width=1.5,edge.curved = .5,edge.arrow.size=0.5,asp=9/16,margin=-0.15)

# histogram of when tweets made
hist(MCC_Twitter$created_at, breaks = 50)
