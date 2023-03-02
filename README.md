# ClusterSim

Josh Herbeck

## Overview

This is a simple branching model of HIV transmission. There is no contact/sexual 
network created, and there are no uninfected individuals; the model just has infected
individuals who can transmit, and then the newly infected recipients who can transmit, 
and so forth through time. The output is a transmission record (line list) that 
we can use to make phylogenies and identify clusters.

Each individual has a probability of transmission per timestep, and this probability 
is a combination of contact rate (number of sexual partners per timestep) and the 
per-contact rate of transmission. There is also an individual rate of sampling 
(functionally this is the probability of removal/extinction).

First order goal:  to understand if high mean degree ("super-spreading", or a 
small-ish high risk core group/key population) is associated with more clustering 
and bigger clusters. 

Second order goal:  identify general predictors of clustering patterns (i.e. make a
simple, fast model with which I can vary offspring distribution, incidence/force 
of infection, sampling (sampling time after infection, sample fraction/coverage, and
sampling bias), and cluster thresholds and build a function for predicting clustering
patterns from those variables.


## Model structure

The model is basically two data frames:  **population_summary** and **transmission_record**, 
a creatively-named run script "Run_script.R", and some functions that are initiated
through a few scripts (see below).

A user should be able to just run the Run_script.R in order to get a line list 
of transmissions (extractable in the Population_summary).

**Population_summary** includes all individuals in the population and their individual 
data. These data include their transmission parameters, infection date, infection 
source, sampling/removal year, and cumulative partners and transmissions. This file
structure is cribbed from Adam's agent-based vaccine trial model; the difference
between Adam's model and this one is that the vaccine trial was interested in 
infections and this model is (mostly) interested in transmissions (and in recording
each transmission for downstream use).

**Transmission_record** is a simple record of whether each individual is removed or
transmits for each timestep. 

The model includes some core functions:

* *assign_heterogeneous_rates*
* *assign_homogeneous_rates*
* *assess_removal*
* *assess_transmission*
* *make_new_infections*


### How to run the model

Basically you just need to open up *Run_script.R*, modify the parameters listed below
as you see fit, and source the Run script.

Initial input parameters:

samplesize
timestep 
sim_time 
mean_partner_parameter 
acts_per_day_parameter 
lambda_parameter
removal_rate_parameter


## Notes / To do list:

1. Add in transmission rate modifier based on time since infection?

2. Currently the transmission_risk_per_day parameter combines the risk across all partners; it doesn't allow an individual to transmit multiple times in the same timestep. Might need to fix that if and only if we use timesteps greater than 1 day


