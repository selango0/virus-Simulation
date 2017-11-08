# virus-Simulation

Introduction 

In this problem set, using Python and matplotlib you will design and implement a stochastic simulation of patient and virus population dynamics, and reach conclusions about treatment regimens based on the simulation results.

You should submit two files for this problem set: your code in ps8.py and a write-up in pdf format called ps8_writeup.pdf. Your writeup should only be a couple sentences per problem. We are not looking for long expositions. Just include the requested graphs and answer the questions completely and concisely.

Getting Started

For this problem set, you will be using the classes from Problem Set 7. Feel free to use your own implementations from Problem Set 7, or you may use the compiled version provided.

Problem 1: Implementing a simulation with drugs

For this part, use the skeleton code provided in ps8.py.

In this problem, we consider the effects of both administering drugs to the patient and the ability of virus particle offspring to inherit or mutate genetic traits that confer drug resistance. As the virus population reproduces, mutations will occur in the virus offspring, adding genetic diversity to the virus population. Some virus particles gain favorable mutations that confer resistance to drugs.

In order to model this effect, we introduce a subclass of SimpleVirus called ResistantVirus. ResistantVirus maintains the state of a virus particle’s drug resistances, and account for the inheritance of drug resistance traits to offspring. Implement the ResistantVirus class. You will test your implementation in problem 2.

We also need a representation for a patient that accounts for the use of drug treatments and manages a collection of ResistantVirus instances. For this we introduce the Patient class, which is a subclass of SimplePatient. Patient must make use of the new methods in ResistantVirus and maintain the list of drugs that are administered to the patient.

Drugs are given to the patient using the Patient class’s addPrescription() method. What happens when a drug is introduced? The drugs we consider do not directly kill virus particles lacking resistance to the drug, but prevent those virus particles from reproducing (much like actual drugs used to treat HIV). Virus particles with resistance to the drug continue to reproduce normally. Implement the Patient class.

Problem 2: Running and analyzing a simulation with a drug

In this problem, we will use the implementation you filled-in for problem 1 to run a simulation. You will create a Patient instance with the following parameters, then run the simulation and answer several questions:

viruses, a list of 100 ResistantVirus instances
maxPop, Maximum Sustainable Virus Population = 1000
Each ResistantVirus instance in the viruses list should be initialized with the following parameters:

maxBirthProb, Maximum Reproduction Probability for a Virus Particle = 0.1
clearProb, Maximum Clearance Probability for a Virus Particle = 0.05
resistances, The virus’s genetic resistance to drugs in the experiment = {'guttagonol':False}
mutProb, Probability of a mutation in a virus particle’s offspring = 0.005
Run a simulation that consists of 150 time steps, followed by the addition of the drug, guttagonol, followed by another 150 time steps. As with problem 2 (of Problem Set 7), perform multiple trials and make sure that your results are repeatable and representative.

Create 2 plots: the record of the average total population and the average population of guttagonol-resistant virus particles.

In your writeup, include these plots and answers to the questions: What trends do you observe? Are the trends consistent with your intuition?

def simulationWithDrug():
    """
    Runs simulations and plots graphs for problem 2.
    Instantiates a patient, runs a simulation for 150 timesteps, adds
    guttagonol, and runs the simulation for an additional 150 timesteps.
    total virus population vs. time and guttagonol-resistant virus population
    vs. time are plotted
    """
    # TODO

Problem 3: The effect of delaying treatment on patient outcome

In this problem, we explore the effect of delaying treatment on the ability of the drug to eradicate the virus population. You will need to run multiple simulations to observe trends in the distributions of patient outcomes.

Run the simulation for 300, 150, 75, and 0 time steps before administering guttagonol to the patient. Then run the simulation for an additional 150 time steps. Use the same initialization parameters for ResistantVirus and Patient as you did for Problem 2.

For each of these 4 conditions, repeat the experiment enough times to get a reasonable insight into the expected result (i.e. 30 times). Use pyplot’s hist() function to plot a histogram of the final virus populations under each condition. You may also find pyplot’s subplot function to be helpful. The x-axis of the histogram should be the final total virus population values (choose x axis increments or “histogram bins” according to the range of final virus population values you get by running the simulation multiple times). Then the y-axis of the histogram should be the number of patients belonging to each histogram bin. You should decide the number of times you need to repeat each condition in order to obtain a reasonable distribution. Justify your decision in your writeup.

Hint: It may take some time to run enough trials to arrive at a distribution for each condition. Debug your code using a small number of trials. Once your code is debugged, use a larger number of trials and expect the simulation to take a few minutes. Use print statements to monitor the simulation’s progress. The simulation should take about 3-6 minutes to run a reasonable number of trials.

In your writeup, include the four histograms (one for each condition of 300, 150, 75, and 0 time step delays) and justify how many times you repeated each condition for a reasonable distribution. Then answer the following questions: If you consider final virus particle counts of 0-50 to be cured (or in remission), what percentage of patients were cured (or in remission) at the end of the simulation? What is the relationship between the number of patients cured (or in remission) and the delay in treatment? Explain how this relationship arises from the model.

def simulationDelayedTreatment():
    """
    Runs simulations and make histograms for problem 3.
    Runs multiple simulations to show the relationship between delayed treatment
    and patient outcome.
    Histograms of final total virus populations are displayed for delays of 300,
    150, 75, 0 timesteps (followed by an additional 150 timesteps of
    simulation).    
    """
    # TODO

Problem 4: Designing a treatment plan with two drugs

One approach to addressing the problem of acquired drug resistance is to use cocktails — administration of multiple drugs that act independently to attack the virus population.

In problems 4 and 5, we use two independently-acting drugs to treat the virus. We will use this model to decide the best way of administering the two drugs. Specifically, we examine the effect of a lag time between administering the first and second drugs on patient outcomes.

For problems 4 and 5, use the following parameters to initialize a Patient:

viruses, a list of 100 ResistantVirus instances
maxPop, Maximum Sustainable Virus Population = 1000
Each ResistantVirus instance in the viruses list should be initialized with the following parameters:

maxBirthProb, Maximum Reproduction Probability for a Virus Particle = 0.1
clearProb, Maximum Clearance Probability for a Virus Particle = 0.05
resistances, The virus’s genetic resistance to drugs in the experiment = {'guttagonol':False, 'grimpex':False}
mutProb, Probability of a mutation in a virus particle’s offspring = 0.005
Run the simulation for 150 time steps before administering guttagonol to the patient. Then run the simulation for 300, 150, 75, and 0 time steps before administering a second drug, grimpex, to the patient. Finally, run the simulation for an additional 150 time steps.

For each of these 4 conditions, repeat the experiment enough times to get a reasonable condition (i.e. 30 times), while recording the final virus populations. Use pyplot’s hist() function to plot a histogram of the final total virus populations under each condition.

Hint: As with problem 3, the simulation will take a few minutes to run. Use print statements to monitor the simulation’s progress.

In your writeup, include the 4 histograms (for 300, 150, 75, and 0 time steps) and answer the following: What percentage of patients were cured (or in remission) at the end of the simulation? What is the relationship between the number of patients cured (or in remission) and the time between administering the two drugs?

def simulationTwoDrugsDelayedTreatment():
    """
    Runs simulations and make histograms for problem 4.
    Runs multiple simulations to show the relationship between administration
    of multiple drugs and patient outcome.
   
    Histograms of final total virus populations are displayed for lag times of
    150, 75, 0 timesteps between adding drugs (followed by an additional 150
    timesteps of simulation).
    """
    # TODO

Problem 5: Analysis of virus population dynamics with two drugs

To better understand the relationship between patient outcome and the time between administering the drugs, we examine the virus population dynamics of two individual simulations from problem 4 in more detail.

Run a simulation for 150 time steps before administering guttagonol to the patient. Then run the simulation for an additional 300 time steps before administering a second drug, grimpex, to the patient. Then run the simulation for an additional 150 time steps. Use the same initialization parameters for Patient and ResistantVirus as you did for problem 4.

Run a second simulation for 150 time steps before simultaneously administering guttagonol and grimpex to the patient. Then run the simulation for an additional 150 time steps. Make sure you run the simulation multiple times to ensure that you are analyzing results that are representative of the most common outcome.

For both of these simulations, plot the total population, the population of guttagonol-resistant virus, the population of grimpex-resistant virus, and the population of viruses that are resistant to both drugs as a function of time.

In your writeup, include the plots from both simulations and explain the relationship between the patient outcome and the time between administering the two drugs arises.

def simulationTwoDrugsVirusPopulations():
    """
    Run simulations and plot graphs examining the relationship between
    administration of multiple drugs and patient outcome.
    Plots of total and drug-resistant viruses vs. time are made for a
    simulation with a 300 time step delay between administering the 2 drugs and
    a simulations for which drugs are administered simultaneously.        
    """
    #TODO
