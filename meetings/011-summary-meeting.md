### Discussion Points

- **Role of JSON Schema in OCWG**: The group discussed the limitations of using JSON Schema to validate documents in OCWG. Max noted that JSON Schema can't handle the flexibility of extensions, leading to two unsatisfying options: either ignore extensions in validation or attempt to validate them with additional schemas.

- **Validation and Custom Code**: Max explained that using JSON Schema alone would not suffice for OCWG, as it requires custom code to validate extensions that cannot be predefined. The group recognized that this would complicate the validation process.

- **Group and Deletion Semantics**: The conversation focused on how groups are handled in different tools (e.g., Obsidian vs. PowerPoint). If a group is deleted, the expected behavior varies by tool. There’s a need to define whether group deletion affects its members and clarify how different structures should behave when deleted.

- **Handling Hidden Nodes**: The group examined whether hidden nodes should be treated as relations or simply as a visual artifact. Some members felt that a hidden node should remain a node but with its visual properties managed elsewhere. There was consensus that it doesn’t need to be treated as a relation.

- **Parent-Child Relationships**: There was a discussion on how to model parent-child relationships, which are commonly used in game engines and other tools. The group explored whether these should be modeled as relations or as part of the node structure itself.

- **Nesting and Groups**: The team discussed how nesting could be encoded in OCWG, either by defining a group within a group or by adding a parent-child relation type. The trade-offs between visual nodes and structural relations were highlighted.

- **Connector and Port Modeling**: Connectors and ports were noted as a challenging area due to the varied implementations across tools. The group debated how to model connector control points and paths, especially when tools use different routing rules for connectors.

- **Visual Properties vs. Relations**: There was a broader conversation about whether visual properties (e.g., connectors, arrows) should be stored within nodes or if they should be modeled as relations. Max noted that separating structural and visual properties could benefit non-visual tools.

- **General Design Principles**: The group reviewed core design principles for OCWG, including support for offline use, dynamic content, graceful degradation, extensibility, human-friendly formats, reuse of existing standards, and precision in definitions like text rendering.

- **Architectural Decision Records (ADRs)**: A suggestion was made to formalize design decisions using ADRs. This format would provide a structured way to document goals, options, and implications of specific decisions, potentially starting with the relations vs. nodes discussion.

### Action Items

- **Max**: Continue to refine the design principles and add these into the stack repo, ensuring that open issues like JSON Schema and structural relations are clearly documented.
  
- **Michael**: Review the design decisions document and provide feedback. Begin exploring the potential use of ADRs for formalizing design choices, starting with the relation and node modeling.

- **Team**: Follow up on specific connector and port modeling challenges, and how they could be encoded within the OCWG framework.

- **Aaron**: Investigate implementing parent-child relationships in the context of OCWG, particularly how they can be modeled efficiently for game engines.

- **Future Task**: Explore the inclusion of common elements like images, shapes, and arrows as part of the base OCWG specification, and consider physics as a potential extension.

### Takeaways

- **OCWG requires custom validation beyond JSON Schema**: The group acknowledged that while JSON Schema is useful, OCWG’s flexibility necessitates custom validation code, especially for handling unknown extensions.

- **Clear structure needed for group and deletion behavior**: The behavior of groups, especially regarding deletion and the impact on members, needs to be clearly defined to ensure interoperability between tools.

- **Hidden nodes are visual artifacts, not relations**: The consensus was that hidden nodes should remain visual entities with their properties stored elsewhere, and there is no need to move them to relations.

- **Parent-child relations are crucial for certain applications**: The group emphasized the importance of supporting parent-child relationships, particularly in game engines and complex canvases, and agreed this should be addressed in future discussions.

- **Modeling connectors and ports is a complex issue**: Given the different approaches tools take for handling connectors and ports, this remains a tricky area that will require further exploration.

- **Maintaining relations helps non-visual tools**: By keeping relations separate from nodes, OCWG can better support tools that prioritize semantic relationships over visual representation, enhancing flexibility for different use cases.

- **Architectural Decision Records (ADRs) might help formalize design decisions**: ADRs were suggested as a tool to document the reasoning behind decisions, particularly in complex areas like relation modeling.