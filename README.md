# FBB-PRIDE

We are participants of PH Bio Hackathon 2021
Our team is from Lomonosov Moscow State University

Our team's aim was to create a model to predict protein solubility!

A picture below  represents steps of our solution
![solution](https://user-images.githubusercontent.com/38766545/115983806-2fcf3a00-a5ac-11eb-8189-e5668ba0ba4b.png)

We first make some preprocessing of PDB files: removing HETATOM, re-numerating residue ids, calculating dssp and sasa, finding exposed amino acids on surface area.

As features for model we used several characteristics:
Markup:
        *protein length and weight
        *instability index and isoelectric point of protein
        *secondary structure fractions (helix, turn, sheet)
        *molar extinction coefficient
        *charge_at_pH and flexibility
        *% of each amino acid type in protein
        *% of hydrophobic atoms of exposed amino acids
        *number of clusters by exposed amino acids
        *volume of clusters
        *average kD of clusters
        *number of TM helixes (by Phobios)

