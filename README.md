# File Description
k_file_xx.c were all forked from https://github.com/binsec/hade/tree/master/experimental_data/src/secretFinding/for
k_file_xx.elf were compiled by clang: clang -O0 xx.c
main.py is a deobfuscation script, you can use it like:
pypy3 main.py 3_file_22.elf //I prefer to use pypy to speed up Angr
// Because I use some tricks to automatically find the "success" branch(the basic block which call puts function), so you don't need to specify the secret branch addr.
The output is:

PS C:\Users\chengrui\Downloads\pypy3.8-v7.3.7-win64\pypy3.8-v7.3.7-win64\ObfsPaper\for> ..\..\pypy3.exe main.py 3_file_22.elf
2
WARNING | 2022-03-09 12:27:12,550 | cle.loader | The main binary is a position-independent executable. It is being loaded with a base address of 0x400000.
WARNING | 2022-03-09 12:27:12,983 | cle.loader | The main binary is a position-independent executable. It is being loaded with a base address of 0x400000.
WARNING | 2022-03-09 12:27:13,036 | angr.storage.memory_mixins.default_filler_mixin | The program is accessing memory or registers with an unspecified value. This could indicate unwanted behavior.
WARNING | 2022-03-09 12:27:13,038 | angr.storage.memory_mixins.default_filler_mixin | angr will cope with this by generating an unconstrained symbolic variable and continuing. You can resolve this by:
WARNING | 2022-03-09 12:27:13,039 | angr.storage.memory_mixins.default_filler_mixin | 1) setting a value to the initial state
WARNING | 2022-03-09 12:27:13,040 | angr.storage.memory_mixins.default_filler_mixin | 2) adding the state option ZERO_FILL_UNCONSTRAINED_{MEMORY,REGISTERS}, to make unknown regions hold null
WARNING | 2022-03-09 12:27:13,041 | angr.storage.memory_mixins.default_filler_mixin | 3) adding the state option SYMBOL_FILL_UNCONSTRAINED_{MEMORY,REGISTERS}, to suppress these messages.
WARNING | 2022-03-09 12:27:13,043 | angr.storage.memory_mixins.default_filler_mixin | Filling memory at 0x7fffffffffeff7c with 4 unconstrained bytes referenced from 0x401065 (_start+0x5 in 3_file_22.elf (0x1065))
SECRET: 0x401229
WARNING | 2022-03-09 12:27:13,537 | angr.storage.memory_mixins.default_filler_mixin | Filling register ftop with 8 unconstrained bytes referenced from 0x0 (not part of a loaded object)
Deprecation warning: Use self.model.get_any_node() instead of get_any_node
WARNING | 2022-03-09 12:27:27,711 | angr.sim_manager | Cannot find states with common history line to merge. Fall back to the naive merging strategy and merge all states.
WARNING | 2022-03-09 12:27:54,869 | angr.sim_manager | Cannot find states with common history line to merge. Fall back to the naive merging strategy and merge all states.
WARNING | 2022-03-09 12:28:34,944 | angr.sim_manager | Cannot find states with common history line to merge. Fall back to the naive merging strategy and merge all states.
WARNING | 2022-03-09 12:28:38,640 | angr.storage.memory_mixins.default_filler_mixin | Filling register ftop with 8 unconstrained bytes referenced from 0x0 (not part of a loaded object)
WARNING | 2022-03-09 12:28:39,031 | angr.storage.memory_mixins.default_filler_mixin | Filling register ftop with 8 unconstrained bytes referenced from 0x0 (not part of a loaded object)
3_file_22.elf [85.91577196121216, '0x3f2e7f00']

It will output the time for deobfuscation and the input to trigger the success branch.
