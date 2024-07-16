## File format currently supported 

- Standard mmCIF from [PDB](https://www.rcsb.org/) and [PDB-DEV](https://pdb-dev.wwpdb.org/) (.cif,.bcif)
- mmCIF from cellPACK (.cif, .bcif). `_entity.details` holds the function, `_entity.pdbx_description` holds the full name with hierarchy path, `_entity.pdbx_ec` holds the original PDB file used, and `_entity.pdbx_parent_entity_id` holds the label. Instances are defined as [biological assemblies](https://pdb101.rcsb.org/learn/guide-to-understanding-pdb-data/biological-assemblies#Anchor-Biol).
- mmCIF from [Petworld (.cif, .bcif)](http://yasara6.org/petworld/index.html). Each object is present only once in the mmCIF file, and the locations of all the instances are provided as transformation matrices in the `_pdbx_struct_oper_list` fields, which are normally used to define the biological assembly (BIOMT record in old PDB files). More format details can be found in the header of each mmCIF file. Furthermore, we added an entry in `_pdbx_model.description` to add a description for each entity.
- Explorer manifest (.zip). A special format designed for the explorer that you can use to view your own custom models.
- Mol* session (.molx). The Mol\* session format, which is a zip archive containing all assets and the states to reproduce a session.



## Manifest : Generic File Format Documentation

This document outlines the structure and types used in the Generic file format, which is designed to handle a variety of data types including structures, meshes, and trajectories.

### Types

#### GenericRoot

Represents the root element in the hierarchy.

- `id` (string): Unique identifier for the root element.
- `label` (string, optional): A human-readable label for the root.
- `description` (string, optional): A description of what the root represents.
- `children` ([GenericGroup[]](#genericgroup)): An array of child groups under this root.

#### GenericGroup

Defines a group that can be part of a root or another group.

- `id` (string): Unique identifier for the group.
- `root` (string): Reference to `GenericRoot.id`, indicating the root to which this group belongs.
- `label` (string, optional): A human-readable label for the group.
- `description` (string, optional): A description of the group.
- `children` ([GenericGroup[]](#genericgroup), optional): Nested groups within this group.

#### GenericEntity

Describes an entity that can be a file with associated groups.

- `file` (string): The entity file name with support for various formats like `.gro`, `.cif`, `.pdb`, `.xyz`, `.mol`, `.sdf`, `.ply`, etc.
- `label` (string, optional): Label for the entity.
- `description` (string, optional): Description of the entity.
- `groups` (object[]): An array of objects linking the entity to its groups. Each object has:
  - `id` (string): Reference to `GenericGroup.id`.
  - `root` (string): Reference to `GenericRoot.id`.
- `instances` ([GenericInstances](#genericinstances), optional): Definitions of instances of the entity.
- `sizeFactor` (number, optional): A factor indicating the scale of the entity; defaults to 1.

#### BinaryData

Defines binary data which can be used in instances.

- `file` (string | Asset): The file or asset containing the binary data.
- `view` (object, optional): Specific view into the binary data, including:
  - `byteOffset` (number): The offset in bytes from the start of the file.
  - `byteLength` (number): The length of the data segment in bytes.

#### GenericInstances

Specifies the instances of an entity, detailing positions and rotations.

- `positions`: Specifies translation vectors:
  - `data` (number[] | [BinaryData](#binarydata)): The data itself or a reference to binary data.
  - `type` (object, optional): Describes how to interpret the data; defaults to `{ kind: 'Array', type: 'Float32' }`.
- `rotations`: Specifies rotations (Euler angles, quaternion rotations, or rotation matrices):
  - `variant` (string): Specifies the type of rotation ('euler', 'quaternion', or 'matrix').
  - `data` (number[] | [BinaryData](#binarydata)): The data itself or a reference to binary data.
  - `type` (object, optional): Describes how to interpret the data.

#### GenericFrame

Describes a single frame in a trajectory.

- `time` (number): The time at which the frame occurs.
- `entities`: An array of entities with their respective instances.
  - `file` (string): The file name of the entity.
  - `instances` ([GenericInstances](#genericinstances)): Instances of the entity in this frame.

#### GenericTrajectory

Describes a trajectory consisting of multiple frames.

- `label` (string, optional): Label for the trajectory.
- `description` (string, optional): Description of the trajectory.
- `frames` ([GenericFrame[]](#genericframe)): An array of frames making up the trajectory.

#### GenericManifest

Defines the overall structure of a Generic file.

- `label` (string, optional): Label for the manifest.
- `description` (string, optional): Description of the manifest.
- `roots` ([GenericRoot[]](#genericroot)): An array of root elements.
- `entities` ([GenericEntity[]](#genericentity)): An array of entities.
- `trajectories` ([GenericTrajectory[]](#generictrajectory), optional): An array of trajectories, if any.

### Example

```json
{
  "label": "cellPACK",
  "description": "cellPACK model",
  "roots":[
    // GenericRoot
    {
        "id": "compartments",
        "label": "Compartment",
        "description": "Compartment hierarchy",
        "children" : [
            // GenericGroup
            {
            "id": "root.proteins",
            "root": "compartments",
            "label": "Proteins",
            "description": "Proteins",
            "children": []
            },
            ...
        ]
    },
    {
      "id": "functions",
      "label": "Function",
      "description": "Functional classification",
      "children": [
        {
          "id": "Metabolism",
          "root": "functions",
          "label": "Metabolism",
          "description": "Metabolism",
          "children": [
            {
              "id": "Membrane Transport",
              "root": "functions",
              "label": "Membrane Transport",
              "description": "Membrane Transport",
              "children": []
            },
            ...
        }
    },
    ...
  ],
  "entities": [
    //GenericEntity
    {
        "file": "SERCA_Y1.bcif",
        "label": "SERCA_Y1",
        "description": "Sarcoplasmic/endoplasmic reticulum calcium ATPase 1 PDB entry [2YFY](http://www.rcsb.org/pdb/explore.do?structureId=2YFY)",
        "groups": [
            {
            "id": "root.proteins",
            "root": "compartments"
            },
            {
            "id": "Essential",
            "root": "essentiality"
            },
            {
            "id": "Membrane Transport",
            "root": "functions"
            }
        ],
        "instances": 
        //GenericInstances
        {
            "positions": {
            "data": 
            //BinaryData
            {
                "file": "SERCA_Y1_data.bin",
                "view": {
                "byteOffset": 0,
                "byteLength": 3240
                }
            },
            "type": {
                "kind": "Array",
                "type": "Float32"
            }
            },
            "rotations": {
            "variant": "quaternion",
            "data": //BinaryData
            {
                "file": "SERCA_Y1_data.bin",
                "view": {
                "byteOffset": 3240,
                "byteLength": 4320
                }
            },
            "type": {
                "kind": "Array",
                "type": "Float32"
            }
            }
        },
        "sizeFactor": 0.0
    },
    ...
    {
      "file": "TT1.ply",
      "label": "TT1_membrane",
      "description": "TT1 membrane",
      "groups": [
        {
          "id": "root.TT1.membrane",
          "root": "compartments"
        },
        {
          "id": "Essential",
          "root": "essentiality"
        },
        {
          "id": "Generic",
          "root": "functions"
        }
      ],
      "instances": null,
      "sizeFactor": 0.0
    }
  ],
  "trajectories": null
}

```