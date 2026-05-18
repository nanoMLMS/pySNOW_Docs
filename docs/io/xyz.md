# xyz files

This module contains functions for input/output operations (reading and writing) of `.xyz` files. 
These files have a regular structure with the following format:

`N_atoms` (first frame)

`Comment_line`

`Atom_1_chemical_symbol` `Atom_1_x_coordinate` `Atom_1_y_coordinate` `Atom_1_z_coordinate`

`Atom_2_chemical_symbol` `Atom_2_x_coordinate` `Atom_2_y_coordinate` `Atom_2_z_coordinate`

`...`

`N_atoms` (second frame)

`Comment_line`

`Atom_1_chemical_symbol` `Atom_1_x_coordinate` `Atom_1_y_coordinate` `Atom_1_z_coordinate`

`...`

PySNOW expects your xyz files to be formatted in this way for I/O operations.

## Functions

::: snow.io.xyz
