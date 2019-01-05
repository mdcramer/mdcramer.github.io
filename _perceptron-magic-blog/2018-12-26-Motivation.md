---
title: Motivation
excerpt: What is the motivation for this project?
tags:
- Perceptron
- motivation
last_modified_at: 2018-12-26 00:00:00 +0000

---
## Using Deep Learning to correct spelling mistakes

### Motivation

This project was inspired by [Tal Weiss'](https://medium.com/@majortal) post on [Deep Spelling](https://medium.com/@majortal/deep-spelling-9ffef96a24f6). His [Deep Spell](https://github.com/MajorTal/DeepSpell/blob/master/keras_spell.py) code can be found on Github.

Here is the beginning of a code block:

    # Check for command line argument to use small data
    print ("Command line args are: {}".format(str(sys.argv)))
    small = 'small' in str(sys.argv)
    # small = True # Use this to force small data. Comment out when running script.
    
    if (small):
        print("Using the small data.")
        directory = "small_graph"
        # This is where the small graph is going to be saved and reloaded
        GRAPH_PARAMETERS = "small_graph/graph_params" # Filename for storing parameters associated with the graph    
        SOURCE_INT_TO_LETTER = "small_graph/sourceinttoletter.json" # Filename for INT to letter List for source sentences
        TARGET_INT_TO_LETTER = "small_graph/targetinttoletter.json" # Filename for INT to letter List for target sentences
        SOURCE_LETTER_TO_INT = "small_graph/sourcelettertoint.json" # Filename for letter to INT List for source sentences
        TARGET_LETTER_TO_INT = "small_graph/targetlettertoint.json" # Filename for letter to INT List for source sentences
        checkpoint = "./small_graph/best_model.ckpt"
    else:
        print("Using the large data.")
        # This is where the large graph is going to be saved and reloaded
        directory = "large_graph"
        GRAPH_PARAMETERS = "large_graph/graph_params" # Filename for storing parameters associated with the graph    
        SOURCE_INT_TO_LETTER = "large_graph/sourceinttoletter.json" # Filename for INT to letter List for source sentences
        TARGET_INT_TO_LETTER = "large_graph/targetinttoletter.json" # Filename for INT to letter List for target sentences
        SOURCE_LETTER_TO_INT = "large_graph/sourcelettertoint.json" # Filename for letter to INT List for source sentences
        TARGET_LETTER_TO_INT = "large_graph/targetlettertoint.json" # Filename for letter to INT List for source sentences
        checkpoint = "./large_graph/best_model.ckpt"

End of code.