OCIF Interoperability and Sync
- Dex Devlon expresses interest in syncing the Remarkable format with OCIF.
- Another project is working on a translation layer to sync Remarkable with OneNote.
- Jess Martin suggests using an interop format like OCIF as a central layer for broader compatibility.
- Dex Devlon believes OCIF could become the primary format for syncing between different tools, such as Remarkable and TLDraw.


- Michael (MAIKEL Dev Helper) developed okiflib, a library designed to facilitate translation layers between OCIF and various formats.
- The goal is to establish a central toolchain for converting between OCIF and other formats.


- The current OCIF format is primarily designed for two-way interchange, not full real-time interoperability.
- Some prototypes are successfully using CRDTs for near real-time sync with OCIF.
- Full interop is considered a future step that requires dedicated design.
- Dex Devlon offers to contribute to the design of OCIF's interoperability aspects, leveraging his work on CRDTs.



OCIF Specification Development
- Discussion focuses on releasing OCIF spec version 0.5.1.
- It is suggested that experimental features within the spec can be labeled as unstable and pre-published to gather implementation feedback.


- The concept of "pages" within OCIF is a key design challenge.
- Many existing formats (Remarkable, Visio, PowerPoint, TLDraw, OneNote) utilize "pages" as distinct canvases.
- The current OCIF spec assumes a single canvas per file, defining a single set of nodes, relations, resources, and schemas.
- The challenge is to represent multiple independent canvases (pages) within a single OCIF file.
- Max proposes that pages could be represented as nodes with a "page extension" that includes a page number and title.
- Nodes would indicate their page affiliation through parent-child relationships.
- A concern is raised about the potential verbosity if every node must explicitly specify its parent.
- The root node of a canvas can point to a main node, which then contains pages as children.
- Parent-child relationships are currently an extension but are being considered for inclusion in the core specification due to their fundamental nature, especially for applications like 3D engines (e.g., gltf in Godot).
- A limitation of the parent-child model is that a node can only have one parent, which conflicts with the idea of a node belonging to multiple pages or groups.
- It is concluded that pages are more akin to "containers" or "groups" rather than strict "parents," as there is no inherent inheritance.
- The use of groups for pages is proposed, with a "page extension" on nodes to designate them as pages.
- For canvases that do not support the page extension, the fallback would be to display pages as visual nodes with a reasonable layout, allowing users to zoom into them.
- A problem arises with relative positioning if a node belongs to two groups or pages, as it cannot have a relative position to two different parents. This implies that nodes cannot exist on multiple pages if relative positioning is utilized.
- Layers are confirmed to be handled using groups.



Next Steps
- Max will:
-  Write up the "pages" concept using the group and node extension approach.


- Dex Devlon will:
-  Investigate TLDraw's internal parent-child relationships and potential for creating cycles.
-  Join future meetings.
-  Engage in discussions on Discord for questions and updates.
