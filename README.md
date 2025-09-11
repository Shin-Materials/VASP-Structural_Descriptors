# VASP-Structural_Descriptors

### Simple description:
Pymatgen-based python script to extract structural descriptors from vasprun.xml or POSCAR file(s)

### How to use:
```
python Structural_descriptor.py [filenames or entries]
```
- `[filename]`: name of vasprun.xml file or POSCAR file (wildcard (*,?) is usable!)
    if you use xml file, you can extract band gap despite longer execution time
- `[entries]`: Descriptors of user choice
  - `a`, `b`, `c`, `V`: lattice parameters and volume
  - `atom1-atom2`: distance between two atoms are called with one dash (`-`)
    - atom can be designated as VESTA format or index number starting from 1.
    - Ex) In SrTiO3, Sr --> Sr1 or 1, Fe --> Fe1 or 2, O1 --> O1 or 3
  - `atom1-atom2-atom3`: bond angle is callable with two dashes joining three atoms
    - Note: This feature is to calcaulte bond angle so it automatically copies the atom so that 'bond angle' is calculated.
    - Angle between 'far' apart atoms are not reliable with this script
  - `SG`, `#SG`: Space group with symbol or space group number
  - `Eg`: Band gap (xml file is needed for this)
  - `Ewald`: Ewald summation of the given structure (nominal charge states is applied within script)
  - `natom`: Number of atoms in the structure
  - `GII`: Global Instability Index (GII) captures instability of deviation from ideal coordination environment. This uses 'Bond_Valcne2016.csv' file as reference.
  - Mathematical operation of descriptors:
     - If you format a descriptor or column with brackets (`[` and `]`), you can execute simple operations.
     - Ex) `[Fe5-O1]+[Fe5-O2]`: sum of bond length of Fe5-O1 and Fe5-O2
     - Ex) `[11-O1]+[Fe5-O2]`: sum of bond length of (11th atom)-O1 and Fe5-O2
     - Ex) `[Fe5-O1]/[Fe5-O2`]: ratio of bond length between Fe5-O1 and Fe5-O2
     - Ex) `[1]`/`[2]`: ratio between 1th column value and 2nd column value
            (Note that 0th column is the filename column).
     - Note: When you use this function in a Bash environment, you might need to envelop the entry with single quotation marks (') to avoid syntax error coming from parenthesis.
