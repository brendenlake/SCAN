# SCAN tasks for  compositional learning

SCAN is a set of simple language-driven navigation tasks for studying compositional learning and zero-shot generalization. The SCAN tasks were inspired by the [CommAI environment](https://github.com/facebookresearch/CommAI-env), which is the origin of the acronym (**S**implified versions of the **C**omm**A**I **N**avigation tasks).

### Citing this data set
Please cite the following paper:

Lake, B. M. and Baroni, M. (2018). [Generalization without systematicity: On the compositional skills of sequence-to-sequence recurrent networks.](https://arxiv.org/abs/1711.00350) Proceedings of ICML 2018.

### SCAN commands

SCAN consists of a set of commands (see table) and their corresponding action sequences. These are the actions an agent should perform to execute the commands successfully. The commands and actions are defined compositionally based on primitives ("jump", "walk", "run", "turn left", etc.) and modifiers such as "twice", "thrice", "and", "after", "around left", etc. Here are some examples.

|Command | Action sequence |
| --- | --- | 
| IN: jump                |                       OUT: JUMP |
| IN: jump left            |                       OUT:  LTURN JUMP | 
| IN: jump around right       |                   OUT: RTURN JUMP RTURN JUMP RTURN JUMP RTURN JUMP |
| IN: turn left twice          |                  OUT: LTURN LTURN |
| IN: jump thrice               |                 OUT: JUMP JUMP JUMP | 
| IN: jump opposite left and walk thrice   |      OUT: LTURN LTURN JUMP WALK WALK WALK | 
| IN: jump opposite left after walk around left | OUT: LTURN WALK LTURN WALK LTURN WALK LTURN WALK LTURN LTURN JUMP |

### Contents of this repository 

**Full set of SCAN commands**    
The complete set of over 20,000 SCAN commands is available here:   
[tasks.txt](tasks.txt)

We also provide a set of standard train-test splits so researchers can compare results.

**Simple train-test split**    
The simple train-test split used in the above paper is available here.
The training set includes 80% of the data, and the remaining 20% are used for the test set.    
[tasks_train_simple.txt](simple_split/tasks_train_simple.txt)    
[tasks_test_simple.txt](simple_split/tasks_test_simple.txt)

**Length train-test split**    
In this split, algorithms are trained on shorter sequences (again, about 80% of the full set) and tested on longer sequences. Length is defined as the number of output actions.    
[tasks_train_length.txt](length_split/tasks_train_length.txt)   
[tasks_test_length.txt](length_split/tasks_test_length.txt)

**Adding a new primitive**    
Here, the training set includes all of the compositional tasks that do not include "jump", as well as
just the primitive "jump" command in isolation (over-represented to consist of 10% of the samples). The test set includes all of the compositional commands that use jump.    
[tasks_train_addprim_jump.txt](add_prim_split/tasks_train_addprim_jump.txt)    
[tasks_test_addprim_jump.txt](add_prim_split/tasks_test_addprim_jump.txt)

This is similar to the split above, but the "turn left" command is added instead of jump.    
[tasks_train_addprim_turn_left.txt](add_prim_split/tasks_train_addprim_turn_left.txt)   
[tasks_test_addprim_turn_left.txt](add_prim_split/tasks_test_addprim_turn_left.txt)

**Adding a new template**
Here, the network is trained on all sequences except those containing a certain template (a complex subcommand, like "jump around right"), to which it must generalize at test time. There are 4 different splits corresponding to 4 different held-out templates: "jump around right", "*Primitive* right", "opposite right" and "around right".
[template_split](template_split/)  

**Adding primitive fillers**
Here, the training set starts out having no commands containing "around right", but is gradually increased across conditions to include commands containing the expression "*Primitive* around right" for 0, 1, 2 or 3 different primitive fillers. The test set is held constant, including only examples with the subcommand "jump around right".
[filler_split](filler_split/) 

**Few-shot**
This setting introduces a further level of granularity between the 0 filler and 1 filler conditions of the previous setting. Starting from the 0 filler condition, N new examples from the 1 filler condition are randomly sampled and added to the training set, where N varies from 1 to 1024 in powers of 2. For each N, 5 splits are available, corresponding to 5 different random samples.
[few_shot_split](few_shot_split/) 

**Additional splits**

The folder [simple_split/size_variations](simple_split/size_variations) contains additional train-test splits that vary the amount of training data. Files are named "tasks_train_simple_pX.txt" where X is the percent of SCAN commands used for training.

The folder [add_prim_split/with_additional_examples](add_prim_split/with_additional_examples) contains variations of the setup for adding the primitive "jump" command, where both the primitive jump command and varying numbers of compositional jump commands are included in the training set. Files are named "tasks_train_addprim_complex_jump_numX_repY.txt" where X is the number of (randomly selected) compositional jump commands included in training, and Y denotes different replications of the random selection.

Please refer to the paper above for a discussion of the additional splits.
