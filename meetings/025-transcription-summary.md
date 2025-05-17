### Major Discussion Points

- **Candidate Recommendation / Candidate Recommendation Status**
  - The group discussed targeting May 28th for announcing the 1.0 candidate recommendation stage. The process involves moving from drafting to inviting implementers to use the specification and provide feedback through real implementations rather than textual comments. The importance of a validator, example files, and test suites for interoperability was emphasized. It was noted that tools and libraries are important but not a strict prerequisite for candidate recommendation status.

- **Local First Conf Talk**
  - A planned 25-minute talk at Local First Conf in Berlin will cover application interrupt and file formats. The talk aims to highlight OakIF’s historical context and demonstrate the benefits of open file formats, continuous exports, and integration possibilities with apps like TL Draw and Obsidian Canvas. Use cases such as local export, continuous export, and full source-of-truth (read/write synchronization) were outlined. The possibility of involving AI-generated OakIF content as demo material was also raised.

- **Buffers and Archive Bundles (File Packaging)**
  - Discussion centered on embedding external resources into OakIF files. Base64 embedding helps but does not scale well for large or numerous assets. The group explored the use of ZIP-based archive bundles as a practical solution for packaging multiple files, with references remaining as file URIs inside the archive. Zip archives were favored as they leverage existing tooling, allow easier manual inspection, and fit common use cases better than custom native archive formats or raw buffers. Buffers may still be useful as an extension for arbitrary binary blobs, but the general need is less pressing for canvas apps compared to 3D models.

- **Nested Canvases, Scale and Coordinate Systems**
  - A deep discussion on the role and definition of the `scale` property, coordinate systems, and relative versus global positions took place. It was agreed that:
    - Current positions are global, but scale is not clearly defined or consistently applied.
    - Scale and other transform properties (position, rotation) should likely be part of a "relative transform" or "relative node" extension rather than at the global node level.
    - There is a need to clearly distinguish between global and local (relative) position, rotation, and scale.
    - The group debated whether scale is necessary if global sizes and positions are always available; consensus leaned toward dropping `scale` at the global node level because size can represent geometry scaling, but keeping rotation distinctions made sense.
    - Relative positioning should support transformations relative to parents, factoring in rotation and scale.
    - Anchor/fit properties are needed to define how resources (e.g., images, nested OakIF files) are scaled or stretched to fit bounding boxes/tags, ideally taking CSS-like `object-fit` semantics into account (e.g., "contain," "cover," "stretch").
    - Non-uniform scaling introduces complexity and should be handled carefully, preferably defaulting to preserving aspect ratio to avoid breaking math/physics.
    - Some proposals to rename or reorganize extensions and properties for clarity were discussed, such as renaming relative node extension to relative transform extension and emphasizing redundant storage of both global and local transforms for different app capabilities.

- **Testing, Tooling, and Validation**
  - The importance of establishing a test suite, a validator, and having a robust set of example OakIF files was emphasized to ensure interoperability and ease of implementation. The group recognized the grunt work involved in this but saw AI-assisted code generation as a promising approach to help build these resources. They discussed setting up TS libraries and CLI tools to manage OakIF parsing, validation, and conversion.

---

### Action Items

- **Spec Updates**
  - Michael to add clarifications and changes regarding the global vs. local transforms, scale property disposition, and relative transforms to the spec and relevant PRs ahead of candidate recommendation.

- **Milestone and Issue Tracking**
  - Aaron to create GitHub issues reflecting open topics, bugs, and enhancements with a milestone for candidate recommendation by May 28th. The group will prioritize and debate what belongs in the milestone.

- **Website and Documentation**
  - Update the OakIF website to host a rendered HTML version of the specification to replace the current limited read-only format.
  - Add more example files and demonstrators on the website for easier onboarding.

- **Talk Preparation**
  - Aaron to finalize presentation title and content for the Local First Conf talk, including historical context, demos of OakIF usage, continuous export examples, and AI content generation.
  - Prepare demos integrating Obsidian Canvas, TL Draw, and City and Canvas showing real-time file syncing and exports.

- **Buffer / Archive Exploration**
  - Explore a ZIP-based archive bundle format for OakIF as a non-breaking extension or spec addition.
  - Consider moving buffer handling to an extension with well-defined use cases.

- **Validation and Testing Tools**
  - Review and support the open PR laying out plans for OakIF tools including parsing libraries, CLI, and tests.
  - Develop a robust test suite with automated validation and possibly visual regression testing via tools like Playwright.

---

### Takeaways

- The specification is generally solid but needs better clarity on coordinate systems, transforms, and scale.
- Candidate Recommendation status is targeted for May 28, 2024, emphasizing implementation feedback over textual spec changes.
- Local (relative) transforms, including position, rotation, and scale, are best handled in an extension distinct from the core nodes which keep global properties.
- ZIP archive bundles provide a practical and backward-compatible approach to bundling assets and external resources.
- Example files, testing infrastructure, and validators are critical for the success and adoption of OakIF.
- Supporting both simple apps that use global transforms and advanced apps that use relative/local transforms through redundancy in the spec is important.
- AI-assisted tooling may accelerate testing and adoption.
- Non-uniform scaling and anchor fitting behavior must be clearly defined to avoid interoperability and rendering issues.
- The group's approach to candidate recommendation fully embraces ongoing iteration and real-world usage before formal recommendation.
