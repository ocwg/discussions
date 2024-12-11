### Major Discussion Points

- **Spec Organization and Structure**  
  The group discussed organizing the spec by separating design decisions, goals, and requirements from the main spec document. This would follow a structured approach like the Architecture Decision Record (ADR) model to keep the main document concise and focused.

- **Licensing for the Specification**  
  A Creative Commons CC BY-SA license was proposed, allowing modifications with attribution and permitting commercial use. The intent was to avoid confusion and ensure wide usability for tool vendors.

- **Spec Generation Tools**  
  The team reviewed tools like Markdown to Spec and Bikeshed, which convert Markdown into formatted HTML specifications. This approach would streamline editing and maintain consistency with industry standards.

- **Canvas Definition**  
  Participants noted the absence of a clear definition for "canvas" in existing documentation and proposed adding this to Wikipedia for clarity. The concept of a 2D or 3D model equivalent was discussed in terms of nodes, relations, and schemas.

- **JSON File Structure**  
  Key aspects of the OCIF file format were defined, including using a root-level attribute `OCIF` for schema identification and deciding to make arrays for nodes, relations, and resources optional to simplify file creation.

- **Coordinate System and Positioning**  
  The group agreed on a left-handed coordinate system (X-axis going right, Y-axis going down, Z-axis into the screen) with logical pixels as the unit. Nodes would be positioned using their top-left corner, consistent with most UI tools.

- **Nodes, Relations, and Resources**  
  Nodes would have unique IDs, positions, optional size and rotation attributes, and a flexible handling of properties. Resources could have multiple representations (e.g., SVG, PNG, text) and fallbacks, while relations would connect nodes with defined types.

- **Schemas and Extensions**  
  Schemas were defined for both the OCIF format and extensions. Extensions would use a `type` property to specify functionality, and schemas would allow concise local naming with global URIs for flexibility and interoperability.

- **File Extensions and MIME Types**  
  The team preferred `.OCIF.json` for file extensions to balance JSON editor compatibility and OCIF-specific identification. They discussed registering a MIME type like `application/OCIF+json` once the format is more developed.

- **Community Hosting and Namespaces**  
  Namespaces for official specs and community extensions were proposed, with examples like `canvasprotocol.org/OCIF`. A potential community server for user-generated extensions was discussed, separate from the official namespace.

### Action Items

- **Spec Organization**  
  Prepare a structured spec document by separating design decisions, goals, and requirements into dedicated sections.

- **Canvas Definition**  
  Draft a formal definition of "canvas" and consider submitting it to Wikipedia.

- **Coordinate System Documentation**  
  Finalize and document the agreed-upon left-handed coordinate system with logical pixels.

- **Fallbacks and Extensions**  
  Develop detailed examples showing how extensions and fallbacks function within resources.

- **Schemas**  
  Define schema URI structure and versioning more precisely, and ensure schema-local naming conventions are clear.

- **File Format Registration**  
  Explore MIME type registration with IANA for `application/OCIF+json`.

### Takeaways

- Using Markdown-based tools like Bikeshed simplifies spec editing while maintaining industry compatibility.
- Clear definitions and structured documentation are essential for adoption and understanding of OCIF.
- Flexibility in extensions and schemas supports a wide range of use cases, ensuring the format remains robust and scalable.
- Community involvement and hosting solutions can promote extension development without compromising the official standard.