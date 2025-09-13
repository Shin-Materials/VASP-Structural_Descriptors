# VASP-Structural_Descriptors

### Simple description:
Pymatgen-based Python script to extract structural descriptors from vasprun.xml or POSCAR file(s)

### How to use:
```
python Structural_descriptor.py [filenames or entries]
```
- `[filename]`: name of vasprun.xml file or POSCAR file (wildcard (*,?) is usable!)
    if you use xml file, you can extract band gap despite longer execution time
- `[entries]`: Descriptors of user choice
  - `atom1-atom2`: the distance between two atoms is called with one dash (`-`)
    - atoms can be designated as VESTA format (Sr1, Sr2, etc.)
    - Or, index number starting from 1 (This feature will be useful to compare a set of structures with different chemistries)
    - Ex) In SrTiO3, Sr --> Sr1 or 1, Fe --> Fe1 or 2, O1 --> O1 or 3
  - `atom1-atom2-atom3`: bond angle is callable with two dashes joining three atoms
    - This feature is intended to calculate angles for neighboring atoms
    - If the distance between atoms is comparable to the lattice parameters, I recommend double-checking the value using VESTA.
  - `SG`, `#SG`: Space group with symbol or space group number
  - `Eg`: Band gap (xml file is needed for this)
  - `a`, `b`, `c`, `alpha`, `beta`, `gamma`: lattice parameters and interaxial angles
  - `V`: unit cell volume
  - `natom`: number of atoms in the structure
  - `Ewald`: Ewald summation of the given structure (nominal charge states will be automatically assigned)
  - `GII`: Global Instability Index (GII) captures instability of deviation from the ideal coordination environment. Parameters will be taken from 'Bond_Valcne2016.csv' file as reference.
  - `atom1.BV`: bond valence of the atom1, calculated based on the same parameters used for GII. 
      - Ex) `Sr1.BV`
  - Mathematical operation of descriptors:
     - If you format a descriptor or column with brackets (`[` and `]`), you can execute simple operations.
     - Ex) `[Fe5-O1]+[Fe5-O2]`: sum of bond length of Fe5-O1 and Fe5-O2
     - Ex) `[11-O1]+[Fe5-O2]`: sum of bond length of (11th atom)-O1 and Fe5-O2
     - Ex) `[Fe5-O1]/[Fe5-O2`]: ratio of bond length between Fe5-O1 and Fe5-O2
     - Ex) `[1]`/`[2]`: ratio between 1th column value and 2nd column value
            (Note that 0th column is the filename column).
     - Note: If you want to use parentheses for complicated forms, you may want to enclose the expression with quotation marks (') to avoid a syntax error coming from parentheses. For example, `([1]+[2])/2`
