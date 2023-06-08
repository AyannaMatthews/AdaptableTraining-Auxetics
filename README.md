# AdaptableTraining-Auxetics

This is code for training disordered elastic networks for auxetic responses and adaptive auxetic responses. The code depends on the Network_Jammed class which contains the necessary functions for manipulating the disordered elastic networks. These are generated from uploaded files containing information about the network. The adaptive training code has functions for training for positive or negative poisson ratios (non-auxetic or auxetic) and code for oscillating training that we use to create adaptive networks.

## Dependencies:
- rigidpy
- import_ipynb

## Generating Data

### Network_Jammed

Class for generating and manipulating networks. 
Run Network_Jammed.get_network(N(number_of_nodes), '1', network_id_num) to output a network class. This is what you will pass into the train() and osc() functions in the Adaptive Training code.

### Adaptive Training

#### Oscillating Training
- import a network using the instructions in the Network_Jammed section. 
- select the total time for training
- select the number of oscillations in that training
- select the training/ testing strain (eps = -1e-6)
- pass these arguments to osc(net, train_length, num_osc, eps) which will output the networks after successive bond cuts during training, the bulk moduli throughout training (Bs), and the shear moduli (Gs) throughout training.

#### Control Training
- import a network using the instructions in the Network_Jammed section. 
- select the total time for training
- select the training/ testing strain (eps = -1e-6)
- pass these arguments to train(net, train_length, eps) which will output the networks after successive bond cuts during training, the bulk moduli throughout training (Bs), and the shear moduli (Gs) throughout training.

#### Poisson Ratio

After running the networks through these training functions, pass the bulk moduli (Bs) and shear moduli (Gs) to the poisson_ratio(Gs, Bs) function to get the poisson ratios throughout training.

## Analyzing Data

### Adaptive Training Analysis

#### Classify Adaptive
- import the bulk and shear moduli for a training set (Bs, Gs) 
- select the search range overwhich we are looking for the adaptive behavior (for example, if training a network for 80 bond cuts with 4 oscillations, we are looking for the drop between the final timestep (80) and the time step 20 bond cuts before (60). So the search range will be [60, 80])
- input the extremes of poisson ratios we are counting as being adaptable (generally [+/-0.75, -/+0.75])
- outputs the poisson ratios, the mechanical failures (bool), successes (bool), adaptive training failures (bool)

#### Classify Control Up/Down
- import the bulk and shear moduli for a training set (Bs, Gs) 
- select the timepoint we are checking
- input the extreme poisson ratio (+/-0.75)
- outputs the poisson ratios, the mechanical failures (bool), successes (bool), control training failures (bool)
