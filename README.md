# Understanding Grokking in AI 
# Final Report 
Angeliki Stathopoulos

Artificial Intelligence: From College Math to Intelligent Systems

Presented to Mr. Ivan T. Ivanov

## Reproduction with a Distinct Prime Modulus
Grokking is a phenomenon in machine learning. It’s when a deep learning model suddenly transitions from memorization to near-perfect validation accuracy, long after it has seemingly overfitted the training data. This part of the project investigates the mechanics of ‘grokking’ by using a one-layer transformer. To demonstrate the universality of this phenomenon beyond the baseline implementations, the model was trained on an addition task using a distinct prime modulus of 67. By limiting the training data and applying strong regularization, we create a setup that forces the model to move past memorization and discover an underlying pattern. 
<img width="804" height="541" alt="image" src="https://github.com/user-attachments/assets/360c26ae-4867-49bf-bc86-ab6ccecdbea7" />
<img width="900" height="446" alt="image" src="https://github.com/user-attachments/assets/4dfac896-60e0-4c17-8a55-3f813b0a7514" />
The log plot of the training and validation loss reveals a classic grokking trajectory. The training path can be characterized into three phases:

Phase 1: Overfitting & Memorization (Epochs 0 to 1000)
During the initial training phase, the model quickly achieved a perfect 100% accuracy score on its training data by memorizing the sample data rather than learning the underlying patterns. While its performance on this data appeared flawless, the model failed completely when evaluated on new validation data. This caused its error rate to rise sharply and plateau. Instead of discovering true deep patterns, the network established arbitrary patterns based on random noise within the dataset. This resulted in overfitting which makes the model incapable of handling new information.

Phase 2: The Latent Plateau (Epochs 1000 to 5000)
Although the model's test performance appears completely stagnant on the surface, adjustments are occurring behind the scenes. Weight decay, set at 1.0, acts as a filter that strips away the complex configurations used for memorization. By systematically dismantling this, the process quietly eliminates the model's overfitted habits and clears the path for it to develop more generalized patterns.

Phase 3: The Grokking Phase Transition (At Epoch 5000)
When it reaches epoch 5000, the network undergoes a sudden phase transition, ‘grokking’. The validation loss abruptly plunges to near-zero, while the validation accuracy instantly surges to 100%. This means that the model has completely abandoned its memorized lookup tables. Instead of relying on memorization, the network has successfully generalized by understanding the true mathematical structure of the task. 

Overall, by altering the baseline prime modulus to 67, the total dataset space was scaled down from the conventional 1132 = 12,769 pairs to a smaller 672 = 4,489 pairs. Consequently, the model was required to memorize less training combinations during the initial optimization phase. Because the memorization structures were less, the grokking phase transition occurred much earlier (at epoch 4,500) than the 15,000+ epochs typically documented for p = 113. Ultimately, this experiment successfully confirms the universal nature of the grokking phenomenon. While altering the prime modulus changes the timeline of the plateau, it does not alter the basic form of the model.

## Varied Training Data Fractions 
A parameter sweep maps the boundary conditions of grokking. It demonstrates that delayed generalization is not a default training behavior. It’s driven by how much data is available. At 10% data availability, the training split is too small to provide a pattern so the model overfits by memorizing the subset and fails to generalize within the 25000 epochs. At 30% data availability, the network starts grokking. However, it spends 10950 epochs overfitting before its validation accuracy suddenly clicks and shoots to perfection. On the other hand, as data becomes abundant at 60% and 90%, the model skips the memorization phase and generalizes almost. This experiment proves that when there’s a lot of data, the optimizer finds the pattern the easiest way possible. However, when there’s less data, aggressive weight decay is required to get rid of the memorization structures. 

Starting parameter sweep for 'frac_train'...

--- Training with frac_train = 0.10 ---

  Did not generalize within 25000 epochs.

--- Training with frac_train = 0.30 ---

  Generalized at epoch 10950 with test accuracy 0.9617
  
  Final epochs to generalize: 10950

--- Training with frac_train = 0.60 ---

  Generalized at epoch 500 with test accuracy 0.9536

  Final epochs to generalize: 500

--- Training with frac_train = 0.90 ---

  Generalized at epoch 150 with test accuracy 0.9883

  Final epochs to generalize: 150 
<img width="850" height="507" alt="image" src="https://github.com/user-attachments/assets/b7ed65f4-02f8-4ea2-b572-83e9ab91c9ea" />

## 1D DFT
To understand the embedding matrix and the activations of the MLP, neurons were extracted from the trained model and analyzed using a one-dimensional Discrete Fourier Transform. The Fourier spectra revealed that the learned representations were not distributed evenly. Most of the energy was concentrated which produced a sparse frequency representation. This indicates that the network discovered a Fourier-based encoding of the modular addition task. The same pattern appeared in both the embedding matrix and the MLP activations. This suggests that the model doesn’t memorize. These results provide evidence that the network has learned the underlying pattern and uses sparse frequency features.
<img width="909" height="590" alt="image" src="https://github.com/user-attachments/assets/f82dd327-a741-4ac3-b9f3-c88dbb628a25" />
<img width="900" height="579" alt="image" src="https://github.com/user-attachments/assets/e9a8ffe5-5dcc-4f57-9b33-94e9d28cdcde" />

## Transformer for Module Multiplication
This part of the report looks at how a small neural network solves a non-linear math problem: multiplying numbers with a modulo of 113. Instead of memorizing, it is forced to discover a pattern. Instead of using hard multiplications, the network turns them into simple logarithmic problems.
Because of weight decay, the model abandoned the memorization circuits and used either a trigonometric or discrete log circuit. The sudden drop in test loss is proof that the underlying pattern was found.
<img width="900" height="445" alt="image" src="https://github.com/user-attachments/assets/fea2bf1a-7176-48e2-b30c-bc5d31ab8c16" />
