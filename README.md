# BGWWO Feature Selection
## Pseudo-code of BGWWO

1. Initialize population with random solutions  
2. Set `i ← 0`  

3. **While** `i < I` do  
   - **For each wolf in the population do**  
     - Binarize position using a transfer function  
     - Apply binary solutions to select features  
     - Train KNN model on selected features  
     - Evaluate fitness  
   - **End for**  

   - Select `Xα`, `Xβ`, and `Xδ` based on fitness  
   - Update variables `a, A, C, l, p`  

   - **For each wolf in the population do**  
     - Calculate  

     $$
     \vec{D}_\alpha =
     \begin{cases} 
     \gamma \cdot \left| \vec{C}_1^* \cdot \vec{X}_\alpha(i) - \vec{X}(i) \right|, & p < 0.5 \\
     \rho \cdot e^{bl} \cdot \cos(2 \pi l) \cdot \left| \vec{C}_1^* \cdot \vec{X}_\alpha(i) - \vec{X}(i) \right|, & p \geq 0.5
     \end{cases}
     $$

      - Calculate  
      
      $$
      \vec{D}_\beta = \left| \vec{C}_2 \cdot \vec{X}_\beta(i) - \vec{X}(i) \right| 
      $$  
      
      $$
      \vec{D}_\delta = \left| \vec{C}_3 \cdot \vec{X}_\delta(i) - \vec{X}(i) \right|
      $$  
      
      - Calculate  
      
      $$
      \vec{X}_1 = \vec{X}_\alpha(i) - \vec{A}_1(D_\alpha)
      $$  
      
      $$
      \vec{X}_2 = \vec{X}_\beta(i) - \vec{A}_2(D_\beta)
      $$  
      
      $$
      \vec{X}_3 = \vec{X}_\delta(i) - \vec{A}_3(D_\delta)
      $$


     - Update wolf’s position  

     $$
     \vec{X}(i+1) = \frac{\vec{X}_1(t) + \vec{X}_2(t) + \vec{X}_3(t)}{3}
     $$

     - Update iteration: `i ← i + 1`  
   - **End for**  

4. **End while**  

5. Return `Xα` as the best solution  

## Pseudo-code of Binarization

1. Compute probability using the transfer function (e.g., $rV_2$)

$$
TF(X) = 1 - \left| \tanh(X) \right|
$$  

2. Generate a random number $p \sim U(0,1)$  

3. Update binary solution $X_b$:  

$$
X_b =
\begin{cases} 
1 & \text{if } p < TF(X) \\
0 & \text{if } p \geq TF(X) 
\end{cases}
$$  

## Pseudo-code of Fitness Evaluation

1. Apply the binary solution $X_b$ to select features from the dataset  
   - Let $N_s =$ number of selected features  
   - Let $N_t =$ total number of features  

2. Train a KNN classifier using the selected features  

3. Compute classification accuracy $CA$ on validation data  

4. Evaluate fitness:

$$
fitness = \alpha \cdot (1 - CA) + \beta \cdot \frac{|N_s|}{|N_t|}
$$

6. Return the fitness value



