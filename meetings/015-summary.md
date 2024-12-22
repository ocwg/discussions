### Major Discussion Points

- **Specification 0.2 Implementation**  
  The group discussed that specification 0.2 is ready for implementation beyond proof-of-concept stages. Michael provided feedback on Max's pull request to ensure readiness.  

- **Rotational Center and Positioning**  
  It was agreed that the rotational center of a note should be consistent with its positioning point, set as the top-left corner, to align with industry standards. The spec will be updated accordingly.

- **Array vs. Map for Resource Validation**  
  The group debated using arrays with unique ID fields versus maps for resources. Arrays were chosen for better validation error messages and simplicity when merging files.  

- **Documentation for Design Decisions**  
  The team emphasized documenting the rationale behind decisions, such as choosing arrays over maps, in a design decisions document for transparency and consistency.

- **Extensions Structure and Description**  
  Discussions focused on the need for a standardized format for extensions, including a schema, description, and examples. Extensions should have a clear documentation structure, potentially stored as `readme.md` files.  

- **Relation Types and Extensions**  
  The group explored how to structure relations and extensions, emphasizing that relation types could also function as extensions of a base relation. This would make the model more consistent with nodes.

- **Bundling Schemas in Files**  
  The benefits of bundling schemas with ocif files versus linking them externally were debated. The group leaned towards bundling for offline usability and version control.  

- **Relative Constraints Extension**  
  The proposed "relative constraints" extension would define positions and rotations relative to another node, providing flexibility for visual and structural relationships.  

### Action Items

1. **Spec Updates**  
   - Update the specification to align the rotational center and positioning point.
   - Change references from maps to arrays for resources in the spec.

2. **Documentation Development**  
   - Document the rationale for design decisions in a dedicated section.
   - Create a template for extension documentation using `readme.md` files.

3. **Schema Handling**  
   - Develop a command-line tool to bundle schemas with ocif files for easier distribution.

4. **Next Meeting Agenda**  
   - Decide on built-in versus external extensions for nodes and relations.
   - Revisit and finalize the "relative constraints" extension.

### Takeaways

- Using arrays over maps simplifies validation and merging processes.
- Clear and consistent documentation is critical for maintaining the spec and onboarding contributors.
- Bundling schemas with ocif files enhances offline usability and ensures version consistency.
- The "relative constraints" extension shows potential for adding flexibility to node positioning and rotation but requires further refinement.