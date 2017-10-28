# SCAN tasks for  compositional learning

SCAN consists of simple language-driven navigation tasks for studying compositional learning. These **S**implified versions of the **C**omm**A**I **N**avigation tasks, where the original CommAI environment can be accessed [here](https://github.com/facebookresearch/CommAI-env). 

### Citing this data set
Please cite the following paper:

Lake, B. M. and Baroni, M. (2017). Still not systematic after all these years: On the compositional skills of sequence-to-sequence recurrent networks. _arXiv preprint_.

### SCAN commands

SCAN consists of commands paired with action sequences. Examples are included below:


|Command | Action sequence |
| --- | --- | 
| IN: jump                |                       OUT: JUMP |
| IN: jump left            |                       OUT:  LTURN JUMP | 
| IN: jump around right       |                   OUT: RTURN JUMP RTURN JUMP RTURN JUMP RTURN JUMP |
| IN: turn left twice          |                  OUT: LTURN LTURN |
| IN: jump thrice               |                 OUT: JUMP JUMP JUMP | 
| IN: jump opposite left and walk thrice   |      OUT: LTURN LTURN JUMP WALK WALK WALK | 
| IN: jump opposite left after walk around left | OUT: LTURN WALK LTURN WALK LTURN WALK LTURN WALK LTURN LTURN JUMP |

The commands and actions are defined compositionally based on primitives ("jump", "walk", "run", "turn left", etc.) and modifiers such as ("twice", "thrice", "and", "after", "around left", etc.).

### Contents

The complete set of SCAN commands is available here:   
[tasks.txt](tasks.txt)

The simple train-test split used in the paper is available here (80% used for training):    
[tasks_train_simple.txt](simple_split/tasks_train_simple.txt)   
[tasks_test_simple.txt](simple_split/tasks_test_simple.txt)

The split based on length (of the action sequence) is available here:   
[tasks_train_length.txt](simple_split/tasks_train_length.txt)   
[tasks_test_length.txt](simple_split/tasks_test_length.txt)

The split for adding the primitive "jump" command and testing on the compositional jump commands:
[tasks_train_addprim_jump.txt](add_prim_split/tasks_train_addprim_jump.txt)   
[tasks_test_addprim_jump.txt](add_prim_split/tasks_test_addprim_jump.txt)

The split for adding the primitive "turn left" command and testing on the compositional turn left  commands:
[tasks_train_addprim_turn_left.txt](add_prim_split/tasks_train_addprim_turn_left.txt)   
[tasks_test_addprim_turn_left.txt](add_prim_split/tasks_test_addprim_turn_left.txt)

**Additional splits**

The folder [simple_split/size_variations](simple_split/size_variations) contains additional train-test splits that vary the amount of training data. Files are named "tasks_train_simple_pX.txt" where X is the percent of SCAN commands used for training.

The folder [add_prim_split/with_additional_examples](add_prim_split/with_additiona_examples) contains variations of the adding the primitive "jump" setup, where the primitive jump command and varying numbers of compositional jump commands are included during training. Files are named "tasks_train_addprim_complex_jump_numX_repY.txt" where X is the number of (randomly selected) compositional jump commands and Y is different replications of the random selection.