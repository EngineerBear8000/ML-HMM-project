# Hidden Markov Model for Named Entity Recognition

## 1. Emission Parameter Training and Data Preprocessing

The first phase of the project focused on data preprocessing and emission parameter estimation. The implementation began with a flexible data parsing function that carefully reads training data, handling both labeled and unlabeled sentences. One preprocessing step was implementing smoothing techniques to handle rare words and improve model generalization.

Key preprocessing techniques included:
- Handling unknown words by replacing rare words (occurring less than 3 times) with a special '#UNK#' token
- Identifying and tracking unique tags in the dataset
- Creating a comprehensive emission probability dictionary

The emission probability calculation involved:
1. Counting word-tag occurrences
2. Normalizing counts by tag frequency
3. Creating a probability distribution for each word-tag pair

This approach ensured that the model could handle unseen words by using the '#UNK#' token.

## 2. Transition Parameters and Viterbi Algorithm

The second question is about calculating the transition probabilities between tags and implementing the fundamental Viterbi algorithm for sequence prediction. The transition probability calculation involved:
- Creating a count-based transition matrix
- Calculating probabilities of tag transitions
- Normalizing transitions by previous tag frequencies

The Viterbi algorithm was implemented as a dynamic programming approach to find the most likely sequence of tags. Key algorithmic components included:
- Initialization with start probabilities
- Recursive probability calculation to iterate through every step i, every tag in all the unique tags and all paths from the unique tags in last step i-1.
- Highest probability for the path to that node is calculated with the transition, emission and previous path probabilities.
- Backtracking through with backpointer dict to determine the optimal tag sequence

The algorithm handles:
- Log probability calculations to prevent numerical underflow
- Handling of unknown words
- Efficient sequence prediction
- laplace smoothing with the max function as implementation during emission parameter calculation somehow doesnt product coherent results.

Computational complexity was managed by using log probabilities and implementing efficient recursion and backtracking strategies.

## 3. Top-K Viterbi Algorithm Enhancement

Building upon the standard Viterbi algorithm, the implementation extended to a top-K Viterbi approach. This enhancement allows exploration of multiple potential tag sequences, providing more nuanced predictions.

Key changes in the top-K implementation included:
- Maintaining K best paths at each step
- adding and additional innermost loop to calculate probabilities for the top paths from the previous tag. 
- Sort all the candidate paths found and only store the top 4 in the node
- Extended backtracking to reconstruct multiple tag sequences

The top-K approach offers several advantages:
- Increased prediction flexibility
- Exploration of alternative tag sequences
- Potential for more robust sequence modeling

The implementation successfully demonstrated the ability to generate multiple candidate tag sequences, expanding the predictive capabilities of the base Viterbi algorithm.

## 4. Feature-Based Perceptron Model: Towards Advanced Sequence Labeling

The fourth phase introduced a feature-based perceptron approach to sequence labeling, representing a more sophisticated machine learning technique for named entity recognition.

Key components of the feature-based model included:
- Comprehensive feature extraction function
- Features capturing:
  * Word characteristics
  * Capitalization
  * Numeric content
  * Punctuation
  * Contextual word information
  * Previous and next word context

The perceptron training algorithm:
- Initializes weights to zero
- Iteratively updates weights based on prediction errors
- Learns feature importance for different tag predictions

While the implementation was not fully completed, it laid groundwork for a more adaptive sequence labeling approach that could potentially improve upon the HMM model's performance.

## Experimental Results and Observations

The implementations were evaluated on a named entity recognition task, with results demonstrating:
- Entity precision around 83.58%
- Entity recall around 84.23%
- F-score of approximately 0.8390

These metrics suggest the models performed quite effectively in identifying and classifying named entities.

## Conclusion

This work demonstrated a basic implmentation of Hidden Markov Models for sequence labeling, starting from basic HMM techniques and evolving towards more sophisticated machine learning methods. 

# Running the code

code can be run cell by cell in sequence with the input files in the same folder as the python notebook q1,2,3,4.ipynb. This notebook contains the code for solving all 4 questions. It also includes markdown cells with the outputs from the evaluation script provided.   