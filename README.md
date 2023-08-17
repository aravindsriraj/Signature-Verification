# Signature-Verification

**Signature verification** is the process of determining whether a given signature belongs to a specific individual. It's commonly used for authentication, security, and fraud detection purposes. Signature verification involves comparing the features of a given signature with those of a genuine reference signature to determine if they match.

Convolutional Neural Networks (CNNs) can be used for signature verification by learning to extract relevant features from signature images and then using those features to distinguish between genuine and forged signatures. To enhance the performance of CNNs for this task, contrastive loss and triplet loss are specialized loss functions that can be used to improve the feature learning process.

### Can we use Traditional CNN (Convolutional Neural Networks) to solve this task?

- Let us assume we have a company of 1000 employees.
- We decide to implement a facial recognition system(**is an important computer vision task that allows us to identify and verify a person’s identity**.)  to record the attendance of your employees.
- If we were to use traditional neural networks, we will have to face two main problems
 - First one would be the dataset.
 - It would be nearly impossible to assemble a huge collection of dataset from each of our employees.
 - But a traditional CNN won’t be able to learn features with such small collection.

- We’ll also end up with 1000 output classes
- Let’s consider that somehow we got a huge dataset from each of our employees and we trained a really good CNN model.

# **What happens when a new employee joins our organization? How can we include the person into our facial recognition system?**

- For example, if a new person is added to the database, we will have to re-train the identification system built for K classes on the new K+1 classes from scratch.
- This is because previously, the classifier had K neurons, and now we need a classifier with K+1 neurons.
- This inhibits the efficiency and scalability of the system, as every time a new face is added, the entire training procedure has to be repeated.



All these shortcomings can be overcome using a new architecture known as **siamese networks** architecture or **One-shot learning** architecture.

**1. Contrastive Loss:**
Contrastive loss is used in siamese networks, a type of neural network architecture designed to learn similarity between pairs of data points. In the context of signature verification, this involves presenting pairs of genuine and forged signature images to the CNN. The network learns to map these images into a feature space where similar signatures are closer together, and dissimilar signatures are farther apart.

The contrastive loss function encourages the network to minimize the distance between feature representations of genuine signatures while maximizing the distance between feature representations of genuine and forged signatures. The loss function can be defined as follows:

![image](https://github.com/aravindsriraj/Signature-Verification/assets/60252521/c2ea0d14-3413-4200-b89c-76d0c9d95500)


**L_contrastive = 0.5 * (1 - y) * D^2 + 0.5 * y * max(0, margin - D)^2**

Where:
- **y** is the binary label indicating whether the pair is a genuine match (1) or a forgery (0).
- **D** is the Euclidean distance between the feature representations of the two signatures.
- **margin** is a hyperparameter that determines the minimum distance threshold between genuine and forged signatures.

**2. Triplet Loss:**

Triplet loss is another loss function used for learning embeddings that capture similarity relationships. In the context of signature verification, triplet loss involves presenting a triplet of images to the CNN: an anchor (genuine), a positive (another genuine with the same identity), and a negative (forged). The network learns to map the anchor and positive closer together in the feature space compared to the anchor and negative.

The triplet loss function encourages the network to reduce the distance between the anchor and the positive while increasing the distance between the anchor and the negative, by a certain margin. The loss function can be defined as follows:

![image](https://github.com/aravindsriraj/Signature-Verification/assets/60252521/a9b58583-22f6-4734-8e37-43d2a79bceb8)


**L_triplet = max(0, D(anchor, positive) - D(anchor, negative) + margin)**

Where:

- **D(a, b)** is the distance between the feature representations of items a and b.
- **margin** is a hyperparameter that sets the desired separation between positive and negative samples.

Both contrastive loss and triplet loss contribute to training CNNs that learn more effective signature representations for verification tasks. They help the network learn to distinguish between genuine and forged signatures by learning features that capture the inherent differences between them. These specialized loss functions are particularly useful when dealing with limited labeled data, as they guide the network to focus on the most informative aspects of the data for the verification task.

