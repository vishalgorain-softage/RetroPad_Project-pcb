## Methodology: Circuit Design and PCB Development via SKiDL–KiCad Pipeline

Each component of the RetroPad circuit is designed and interconnected using Python-based scripting with the SKiDL framework, followed by PCB realization in KiCad. The workflow is structured to ensure modular design, clear connectivity definition, and reproducible hardware output.

### Per-Component Circuit Definition

Each input element (button) is implemented using a reusable Python function that defines its electrical behavior. Every button consists of a push switch and a pull-down resistor (10kΩ), ensuring stable signal levels. Components are instantiated programmatically, allowing consistent and scalable circuit generation while treating each unit as an independent logical block.

### Circuit Construction Strategy

The overall circuit is constructed by defining global power nets (`VCC`, `GND`) and connecting individual button modules to dedicated signal nets. These signal lines are routed to a central connector interface, which serves as the communication bridge to an external microcontroller or input system. The design emphasizes clean net separation, modularity, and ease of expansion.

### Netlist Generation Pipeline

The complete circuit description is processed using SKiDL to generate standardized output files, including a netlist (`.net`) and an XML representation (`.xml`). Electrical Rule Check (ERC) is performed to validate connectivity and ensure there are no floating or conflicting signals. These outputs act as the interface between the logical circuit design and the physical PCB layout stage.

### PCB Layout Implementation

The generated netlist is imported into KiCad’s PCB Editor, where all components are instantiated with their respective footprints. Components are manually arranged to follow an ergonomic RetroPad layout, including directional (D-pad) and action buttons. Electrical connections are completed through routing, ensuring proper trace paths and adherence to PCB design practices.

### Layout and Routing Strategy

Component placement is optimized for usability and signal clarity, with logical grouping of related inputs. Routing is performed to minimize trace overlap and maintain clean signal paths. Ground connections are unified, and optional ground planes can be implemented to improve electrical stability and noise reduction.

### Validation and Design Checks

The PCB design is verified using design rule checks (DRC) within KiCad to ensure manufacturability and electrical correctness. Connectivity is validated against the generated netlist to confirm accurate translation from the SKiDL design stage. Any inconsistencies are resolved through iterative refinement.

### Dependency and Environment Management

The project relies on Python with the SKiDL library for circuit generation and KiCad for PCB design. All dependencies are managed within a virtual environment to ensure reproducibility. This setup allows the entire workflow—from circuit definition to PCB generation—to be executed consistently across different systems without configuration conflicts.
