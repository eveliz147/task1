
# FBB-PRIDE

We are participants of PH Bio Hackathon 2021
Our team is from Lomonosov Moscow State University

Our team's aim was to create a model to predict protein solubility!

A picture below  represents steps of our solution
![solution](https://user-images.githubusercontent.com/38766545/115983806-2fcf3a00-a5ac-11eb-8189-e5668ba0ba4b.png)

We first make some preprocessing of PDB files: removing HETATOM, re-numerating residue ids, calculating dssp and sasa, finding exposed amino acids on surface area.

As features for model we used several characteristics:

### Some standard characteristics of proteins

 - protein length and weight
 - instability index and isoelectric point of protein
 - secondary structure fractions (helix, turn, sheet)
 - molar extinction coefficient
 - charge_at_pH and flexibility
 - % of each amino acid type in protein

###Our additional characteristics 
 - % of hydrophobic atoms of exposed amino acids
 - number of clusters by exposed amino acids
 - volume of clusters
 - average kD of clusters
 - number of TM helixes (by Phobios)

## Selection of amino acids on the protein surface
We have selected amino acids that are located on the surfaces of the protein based on exposure evaluation . We obtained these values ​​from the dssp, calculated by a third-part program called mkdssp, using the prody methods. Each selected residue was characterised using kD scale and number of exposed hydrophobic atoms. Number of exposed hydrophobic atoms was then used as nodes weight.
We have also calculated the solvent accessible area for all the atoms of the exposed residues using a FreeSASA library, and then selected only the atoms with a value greater than the threshold.

## Clusters 
Using the residue hydrophobic characteristic, we have merged the amino acids that are located next to each other and then we have expanded clusters 
For top-4 clusters we estimated mean volume of side chain AA residues and mean kD, which were lately used as features


## Graph

Graph edges have been connected basing on the measured distance between the nearest atoms of such amino acids. The distance has been calculated from three-dimensional PDB coordinates. After this step we also calculated the graph kernels and used them as graph vector embeddings.


## Model

 We had 3 types of fetures: 
  *standart
  *custom tabular 
  *custom graph embeddings.


 We have constructed three types of graphs, where each one encodes one distinct feature about nodes(exposed amino acids) - kd, hydrophobicity and amino acid name. Each graph was then transformed into graph embeddings (vector representation) using the best fitting graph kernel (we’ve tried about five different types). Based on each graph types we trained models (select best for each graph types) and made prediction. Each prediction of such base models were than used as a festures. 
We concatenate these predictions with hydrophobic clusters parameters and our other tabular features to create big feature tables which than were used to train meta-model. 
Overall, the final model random forest has been trained and gave a final prediction of solubility. 
