### Discussion Points from the Open Canvas Working Group Meeting

- **Core Specification and Extensions**:  
  The group discussed the importance of a common core specification (OCIF spec) that ensures interoperability and functionality, with additional features offered as extensions. They emphasized keeping the core small and coherent to improve adoption.  
  - *Action Item*: Release version 0.3 of the OCIF spec, incorporating changes from 0.2 and 0.21, and update all related documentation.

- **Versioning Approach**:  
  They deliberated on versioning strategies for the OCIF specification, agreeing on versioning the core and extensions separately to maintain clarity and flexibility.  
  - *Action Item*: Organize schema and spec documents into versioned folders (e.g., `0.3/`), ensuring consistency.

- **Schema Development and Validation**:  
  JSON schema development was discussed, focusing on creating schemas for core components like rectangles, circles, and paths. They also debated optional versus required properties and the need for clear defaults.  
  - *Action Item*: Create a schema for the "circle" node and add it to the repository, along with other foundational examples.  
  - *Action Item*: Decide on a consistent JSON schema version and validate schemas against it.

- **Visual Nodes and Assets**:  
  The group explored how to represent basic shapes (rectangles, circles) and text in the specification, emphasizing simplicity and extensibility. They agreed to handle text as a separate asset linked to shapes.  
  - *Action Item*: Finalize definitions for visual nodes like "circle," "rectangle," and "text" and push examples to the repository.

- **Path and Freehand Support**:  
  Path data support was identified as critical for representing arbitrary shapes. They decided on supporting a subset of SVG commands for simplicity, with allowances for line-based fallbacks.  
  - *Action Item*: Define a "path" extension using basic SVG path commands and clarify its usage in the core spec.

- **Arrows and Relationships**:  
  The group discussed minimal implementations for arrows and relations, considering the complexity of directional markers and interrelations between nodes.  
  - *Action Item*: Define basic arrow properties (e.g., start and end markers) for inclusion in the core spec.

- **Tooling and Interoperability**:  
  They emphasized the importance of maintaining interoperability across tools by adhering to the OCIF format and discussed the potential for storing and exporting data in the OCIF format itself.

---

### Action Items

1. **Release Version 0.3**: Update the spec to reflect changes and publish version 0.3, addressing differences between 0.2 and 0.21.  
2. **Organize Repositories**: Create versioned folders for schema and spec documents.  
3. **Finalize Core Schemas**: Develop schemas for "circle," "rectangle," and "path" nodes, including default property specifications.  
4. **Validate Schemas**: Confirm consistency with the appropriate JSON schema version.  
5. **Push Examples**: Check in schema examples for core visual elements to the repository.  
6. **Arrow Implementation**: Define minimal arrow properties for inclusion in the core spec.

---

### Takeaways

- A smaller, well-defined core spec is likely to see better adoption, with extensions offering flexibility for additional features.
- Clear versioning and schema organization will simplify implementation and reduce confusion.
- Using the OCIF format as a storage and interchange format can enhance tool compatibility and prevent data loss during export/import processes.  
- Early examples and documentation are critical for improving understanding and encouraging contributions.