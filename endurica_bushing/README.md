## Endurica Bushing
This example accompanies a webinar hosted by Coreform and Endurica on Feb-26-2025 and an associated "deep-dive" demonstration -- both of which are available on YouTube.

1. Coreform & Endurica webinar: 
2. Deep-dive demonstration: 

The webinar provided an overview to the meshing process, including some tips and tricks, but is relatively high level in its discussion.
The deep-dive demonstration builds upon the webinar and shows the actual process of building a quality hex mesh in Coreform Cubit.

This example includes two similar, but distinct journal files.

1. `endurica_bushing_live_demo.jou`
    - This is the journal file as built during the deep-dive demonstration. Use this to follow-along with the deep-dive demo video.
2. `mesh_endurica_bushing.jou`
    - This is the journal file I used during the collaboration with Endurica to produce the webinar. 
    I use a slightly different approach than that shown in the deep dive, where I meshed the entire bushing assembly at once.
    In this script I used another commonly-used approach wherein each part within an assembly is isolated, meshed, exported to a mesh file and/or saved to a `.cub5` one at a time.
    The entire combined assembly can be recovered in Coreform Cubit by importing each `.cub5` file back into Coreform Cubit.
    Note that to support the mesh convergence study with Endurica that the beginning of the journal file contains a variable, `mesh_size`, that is used later to access predetermined mesh sizes from inline `dict` definitions:
    ```python
    #!python
    mesh_size = "medium" # Choices: ["coarse", "medium", "fine"]
    ...
    ...
    cubit.cmd(f"surface 29 size { {'coarse':2, 'medium':0.5, 'fine':0.25}[mesh_size] }" )
    ...
    cubit.cmd(f"volume all except with is_meshed size { {'coarse':6, 'medium':2, 'fine':1}[mesh_size] }" )
    ```
