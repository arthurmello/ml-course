---
marp: true
theme: default
author: Arthur
---
<style>
:root {
    --color-background: #FFFFFF !important;
	--color-foreground: #101010 !important;
    }

</style>

<!-- _class: lead -->

# TensorFlow

---
<!-- paginate: true -->

# Ordre du jour
1. Introduction
2. Rappel: les réseaux de neurones
3. TensorFlow
4. Quelques exemples

---
# Introduction
## Que'est-ce que c'est TensorFlow?
> "TensorFlow est une **plate-forme open source** de bout en bout pour **l'apprentissage automatique**. Il dispose d'un écosystème complet et flexible d'outils, de bibliothèques et de ressources communautaires qui permet aux chercheurs de pousser l'état de l'art en matière de ML et aux développeurs de créer et de déployer facilement des applications alimentées par ML"

---
# Introduction
## Que'est-ce que c'est TensorFlow?
![width:1200px](TF1.png)

---
# Introduction
## Pourquoi TensorFlow?
- Plusieurs niveaux d'abstraction
- Fait pour être mis en production sur n'importe quelle plateforme (mobile, etc.)

---
# Rappel: les réseaux de neurones
Un réseau de neurones c’est un type de modèle, inspiré du cerveau humain, composé de plusieurs équations plus ou moins simples, imbriquées

<br>

![width:600px](neural-network-1.png)

---
# Rappel: les réseaux de neurones
La façon dans laquelle ils sont imbriqués peut varier selon le problème

<br>

![width:600px](neural-network-2.png)

---
# TensorFlow
## Tenseurs, graphes et réseaux de neurones
- Un **tenseur** est un **conteneur** qui peut contenir des données en N dimensions
- Les tenseurs sont des généralisations de matrices à l'espace à N dimensions (une matrice est donc un tenseur spécifique, à 2 dimensions).

- TensorFlow permet la création d'un **flux de données**, en utilisant des **tenseurs** et des **graphes**.

- Nous pouvons donc utiliser **TensorFlow** pour construire un **réseau de neurones** !

---
# TensorFlow
## TensorFlow vs. Keras

TF | Keras
-----|------
Générique (plusieurs tâches de ML) | Spécifique
Flexible | Intuitif
Utile pour faire de la recherche | Utile pour mettre un modèle en production

<br>
*Keras est compris dans le package TensorFlow pour Python

---
# Quelques exemples
```py
# Import `tensorflow` 
import tensorflow as tf 

# Initialize placeholders 
x = tf.placeholder(dtype = tf.float32, shape = [None, 28, 28])
y = tf.placeholder(dtype = tf.int32, shape = [None])

# Flatten the input data
images_flat = tf.contrib.layers.flatten(x)

# Fully connected layer 
logits = tf.contrib.layers.fully_connected(images_flat, 62, tf.nn.relu)

# Define a loss function
loss = tf.reduce_mean(tf.nn.sparse_softmax_cross_entropy_with_logits(labels = y, 
                                                                    logits = logits))
# Define an optimizer 
train_op = tf.train.AdamOptimizer(learning_rate=0.001).minimize(loss)

# Convert logits to label indexes
correct_pred = tf.argmax(logits, 1)

# Define an accuracy metric
accuracy = tf.reduce_mean(tf.cast(correct_pred, tf.float32))
```
