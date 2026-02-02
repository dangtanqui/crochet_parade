Manual for CrochetPARADE (the Crochet PAttern Renderer, Analyzer and DEbugger)
The CrochetPARADE manual by Svetlin Tassev is licensed under CC BY-NC-SA 4.0

This manual covers both the platform as well as the CrochetPARADE grammar. NOTE: This manual is work in progress. Last updated: January 7, 2026.

Introduction
CrochetPARADE (Crochet PAttern Renderer, Analyzer, and DEbugger) is a platform that allows users to create, visualize, and analyze both 2D and 3D crochet patterns.

OVERVIEW
CrochetPARADE uses a custom language grammar that allows users to define stitches and stitch patterns. The CrochetPARADE grammar aims to ensure accuracy and precision in the crochet pattern instructions, avoiding the ambiguities encountered with instructions in plain English. The code parses and checks any user provided pattern for correctness and then creates a virtual model of the project, which is then rendered in 3D.

After rendering a pattern, users can review (‘debug’) the final project’s shape and make adjustments. The platform identifies overly loose or tight stitches, enabling users to replace them with more suitable ones before crocheting, thus reducing the need for blocking.

CrochetPARADE's export feature allows users to export an automatically generated crochet chart of their project using standard crochet symbols. One can also export an SVG image that shows stitch connections and identifies stitches by their type, row number, and position within a row. The SVG pattern shows the same information as standard crochet diagrams and can be used as an alternative guide when crocheting. Users can also export projects to 3D files that can be imported in Blender for further manipulation and visualization.

CrochetPARADE includes interactive features such as the ability to rotate, zoom, and pan the 3D view, as well as animating the pattern creation process, which can help in visualizing how stitches attach to each other. Additional features include highlighting and hiding selected stitches, and changing yarn thickness and color. Users can access stitch information by hovering over stitches in the 3D view. CrochetPARADE also allows moving and rotating disjoint objects (as in limbs of amigurumi patterns) in order to place them in their correct locations imitating sewing them together.

CrochetPARADE performs all calculations locally on your device, ensuring that no data is collected to a central server or transmitted over the internet. As a side effect, the platform can be sluggish on old hardware. Models of patterns involving (tens of) thousands of stitches can take minutes or more to calculate.

CrochetPARADE comes with a set of examples including crochet swatches, crocheting in the round, Irish crochet, amigurumis, filet crochet, edgings, mosaic crochet, and others. CrochetPARADE also includes a generator for crochet patterns for arbitrary axially/cylindrically symmetric single-crocheted shapes. It can be used for creating patterns for amigurumi bodies, as well as for hats, buffs, etc. It includes a generator for crochet spheres as well.

GOALS AND POSSIBLE APPLICATIONS
The main goal of CrochetPARADE is to facilitate crochet project design and execution.

Patterns created with CrochetPARADE can be easily shared, ensuring they are free from ambiguities or typographic mistakes. Creators can simply copy and paste the pattern text to share it, and others can use the CrochetPARADE platform to render the shared text into a model of the pattern exactly as intended by the pattern author.

CrochetPARADE can be used in education to teach crocheting but also programming skills, since the CrochetPARADE grammar follows rules similar to those of real programming languages.

The virtual models created by CrochetPARADE can be imported in 3D modelling and CGI software. Picture an animated movie where characters wear crochet hats and sweaters that match real-world crochet projects.

It is probably inevitable that the grammar along with the renderer can allow AI to learn how to write correct crochet instructions of complicated patterns (beyond simple amigurumi) based on general project descriptions.

LICENSE AND COPYRIGHT
The website and all of its computational components are free and open source and are released under the GPLv3 license.
The showcase patterns are either in the public domain (as specified in the pattern description) or are created by the author and are released in the public domain.
This user manual which includes a description of the CrochetPARADE grammar is released under the Creative Commons BY-NC-SA license. The grammar itself cannot be copyrighted and, as any language, is in the public domain.
ACKNOWLEDGEMENTS
CrochetPARADE uses the following libraries: SVG.js, three.js and PrismJS.

Keyboard shortcuts
General shortcuts.
ctrl+l: Toggle layouts.
Shortcuts in the text input area.
shift+Enter: Calculate positions of all stitches.
ctrl+Enter (experimental!): Keep positions of already placed stitches. Then calculate positions of newly added stitches since last calculation. Speeds up calculation, but results will be poorer than rerunning the whole calculation by pressing on “Calculate…” button or pressing shift+Enter.
ctrl+r (experimental!): Same as the previous one, but recalculates only the positions calculated last time the calculation was run. So, it undoes the last calculation and restarts the calculation with the new stitches only. Speeds up code, but will lead to poorer results than rerunning the whole calculation again.
left ctrl+left click: If the instructions were expanded by running "Expand instructions" from the Tools menu with "Run this dialog twice in a row?" selected, then ctrl+click in the text input on a stitch highlights the selected stitch in the editor and in the 3d canvas simultaneously, removing previous highlights.
left ctrl+left alt+left click: If the instructions were expanded by running "Expand instructions" from the Tools menu with "Run this dialog twice in a row?" selected, then ctrl+click in the text input on a stitch highlights the selected stitch in the editor and in the 3d canvas simultaneously. Unlike ctrl+click, this shortcut does not remove previous highlights.
left alt+left click: Clears previous highlights in the editor and 3d canvas.
Shortcuts in 3D view. To activate, click on the 3D canvas first.
left click and drag: Rotate view.
scroll wheel: Zoom.
(right click and drag) or (shift and left click and drag): Pan view.
a: Show stitches one by one.
ctrl+a: Hide stitches one by one.
c: Show project colors. Gray is default if no colors are specified.
esc: Reset visibility and colors of stitches.
ctrl+esc: Hide all but the first stitch.
ctrl+f: Highlight row (by entering: row number) or stitch (by entering: row number, stitch number; for example, "2,4"). Leaving the row number blank (as in ",N") will highlight the N-th stitch of every row. For example, if you enter ",0" that will highlight the beginning of each row.
ctrl+d: Highlight stitch or group of stitches with a specific label. One can also select a collection of labels if any. As an example, a collection of labels may be called 'c[ , ]' and if selected, it will highlight all stitches having labels such as 'c[0,1]', 'c[1,2]', etc. with a whitespace being a placeholder.
ctrl+h: Hide after row or stitch.
ctrl +/-: increase/decrease radii of spheres and cylinders. Affects exported GLTF file as well.
i: Toggle visibility of stitch information box.
shift+left click: Toggle persistence of stitch information box.
left ctrl+left click: If the instructions were expanded by running "Expand instructions" from the Tools menu with "Run this dialog twice in a row?" selected, then ctrl+click in the 3D canvas on a stitch highlights the selected stitch in the editor and in the 3d canvas simultaneously, removing previous highlights.
left ctrl+left alt+left click: If the instructions were expanded by running "Expand instructions" from the Tools menu with "Run this dialog twice in a row?" selected, then ctrl+click in the 3D canvas on a stitch highlights the selected stitch in the editor and in the 3d canvas simultaneously. Unlike ctrl+click, this shortcut does not remove previous highlights.
left alt+left click: Clears previous highlights in the editor and 3D canvas. When the Custom Periphery editor (Tools → Find Project Periphery) is open, Alt+Click on the 3D canvas appends the clicked edge to the custom-periphery editor.
p: Write crochet chart to SVG file. For 2D projects, it shows a face-on view. For 3D projects, it shows an orthographic projection from the current view.
r: Rotate view automatically.
o: Rotate view a tiny amount and save crochet chart SVG corresponding to that view (only for 3D models!). Repeatedly pressing o leads to saving multiple charts for different views while model is rotating. Useful for creating videos of rotating 3D crochet charts. Resolution is specified only the first time key is pressed.
s: Highlight over/under-stretched stitches. Blue for stitches that are too loose, and red for stitches that are too stretched (by more than about 15%) relative to their baseline height. The rest are shown in gray.
v: Toggle visibility of arrowheads.
The 3D visualization canvas
The 3D view shows how stitches are connected between each other. Each sphere represents the top “V” of a crochet stitch. Stitches in crocheting are worked sequentially often forming rows or rounds (or can be forming more general patterns). In the default view, the overall direction of working the stitches is illustrated by the blue connections between stitches (with arrowheads showing the direction). Red connections show the rest of the connections between the stitches. The arrowheads of those connections show which stitch they are associated with. So for example in dc,sc,dc, the single crochet stitch will connect with a blue connections to the dc stitches, and with a red connection to the stitch in which it is worked.

Information about stitches is shown when hovering over a stitch. It shows stitch row and number with row followed by | and the stitch number in the whole project in parenthesis, for example (4,23|410). Note that counting of rows and stitch numbers starts from 0! So in this example, this is the 24-th stitch in the 5-th row. Note that the overall stitch counter (in this case 410) counts non-stitches as well, such as sk, and does not count internal stitches such as stitches in bobbles or popcorns. Then, in square brackets, the information box shows the type of the stitch that is highlighted (sc for single crochet, ch for chain, etc.). The next line starts with C1: and shows “first level of context”, meaning where the stitch is relative to the rest of the stitches in the input instructions. C2: shows the “second level of context” which shows the context of the stitch within the instructions after evaluation of any variables (see below).

See the keyboard shortcuts for further information.

Tools
Tools → Find Project Periphery
Find Project Periphery attempts to identify and order the stitches that lie on the outer boundary (“periphery” or border) of your current project. This is useful for borders/edgings, joining panels, attaching motifs, finishing rounds, and picking up stitches along the side of rows.

In many projects (crocheted rows with turns, crochet lace, motifs), the stitches that are consecutive along the boundary are not consecutive in the order you crocheted them or wrote them in the pattern text. This tool builds one or more periphery graphs and provides an ordering that follows the edge, so you can work and label the boundary as a clean sequence. The tool only uses information about how the stitches are connected, and does not use a particular embedding, i.e. it does not matter what your rendered model looks like (which can change depending on the physics parameters used, such as number of iterations, initial start/seed value, etc) and whether you calculated it in 2D or 3D.

What you get
Periphery candidates (multiple, when the boundary is ambiguous). Each is shown as “Periphery #… — X edges, Y nodes”.
Highlighting of the chosen periphery stitches in the 3D canvas, and (when instructions are expanded) in the text editor as well.
Optional labeling of the periphery stitches in periphery order (see below).
Typical workflow
Render / calculate your project as usual.
Run Tools → Find Project Periphery and choose a periphery from the selector.
(Recommended) Run Tools → Expand instructions with “Run this dialog twice in a row?” so CrochetPARADE can map each stitch in the 3D canvas to a specific stitch in the text editor (needed for text highlighting of the border and for inserting labels on individual stitches).
Use the tool’s Apply label to periphery stitches section to add labels in boundary order. A useful hint: you can use different labels for different parts of the border (say RightEdge, LeftEdge, etc) of the project. To mark only the right edge for example, open the Custom periphery editor (click on Edit edges in Find project periphery), and erase the edges that don't belong to the right edge. When deleting an edge, the highlighting of that edge in the 3D canvas is removed, so in that way you can vizually figure out which edges to keep.
If needed, run Tools → Simplify instructions after labeling. If you used INDEX_ARRAY: or SORT_LABEL: (below), simplification can stay efficient because the periphery indexing is stored separately from the stitches.
Dialog options
Kmax
Controls how far the periphery detector searches for alternative routes between the endpoints of an edge when deciding how “peripheral” that edge is. Larger values can help on complex meshes, but may be slower.

Advanced settings
Max hops: if > 0, the tool may connect separate periphery components by adding shortest connecting paths (in the original stitch graph) up to this length.
Include bridge edges in output: when hops are used, controls whether those “bridge” edges are included in the periphery output (and thus in highlighting/export).
Include longest-cycle subgraph: appends an extra result containing the longest simple cycle found in the largest periphery component.
Include breaking-cycle subgraph: appends an extra result containing a shortest cycle whose removal turns the largest periphery component into a forest (disjoint trees / isolated nodes).
Apply label to periphery stitches
This section applies a label template to the periphery stitches in periphery order (consecutive around the edge). Examples of templates: A, B[k++], C[m], D[a,b++].

Evaluate counter: if the template contains ++ or --, enables counter evaluation while labeling (following periphery order).
Start: the initial counter value used when evaluating a counter.
Reverse order: (shown next to the enabled option) labels the periphery in the opposite traversal direction.
Save counter values as INDEX_ARRAY: when the counter is of the form Label[counter], this stores the enumerated counter values into an INDEX_ARRAY: line, keeping the periphery indexing separate from the stitches. This is the recommended way to label the border, as it is especially helpful if you plan to re-run Simplify instructions after expanding.
Save stitch order as SORT_LABEL: when your label template has no counter (e.g. A, B[], C[0], D[1,2]), saves the periphery traversal order into a SORT_LABEL: line while keeping the label itself simple. Using SORT_LABEL: for plain labels (labels without counters) is recommended.
If more than one counter is present, for example the label you input is of the form D[a,b++], you are offered a choice which counter to use.
Custom Periphery editor
If the automatic periphery is not the one you want (e.g., motifs with holes, lace, complex joins), you can define or tweak a periphery manually:

Enter one edge per line in the form stitch1 -- stitch2. Stitch names are suggested by an autocomplete prompt based on the edges present in the project.
Save the custom periphery; it appears in the periphery selector as a “Custom …” entry. When you save the custom periphery, the code makes a reasonable attempt to sort the stitches in adjacency order, so the order in which you input the edges in the editor is not important.
Alt+Click on the 3D canvas (while the custom editor is open) can append the clicked edge to the custom-periphery editor, allowing quick interactive construction.
Tools → Expand instructions
Objective. CrochetPARADE patterns are often written in a compact, “program-like” style (multipliers, bracketed blocks, user-defined stitches, and label counters). That is great for authoring, but it can be hard to change instructions at the individual stitch level, and it can be hard for other tools (such as periphery labeling) to operate at the level of individual stitches. Expand instructions converts compact instructions into an expanded form by writing out repeated blocks and substituting definitions when possible.

Warning: this tool overwrites the text in the editor. Save your work first.

What it does
Expands expressions such as 3*[sc,dc] into [sc,dc],[sc,dc],[sc,dc].
When possible, substitutes newly defined stitches into their expanded form.
Optionally evaluates index counters in labels (see options below).
If run “twice”, it can fully expand shorthand such as 4sc by first rewriting it into 4*sc and then writing it out as sc,sc,sc,sc. Running twice also enables stitch indexing in the editor view (so stitch numbers appear on hover), which is useful for modifying individual stitches and for tools that need per-stitch access. Moreover, once the text is expanded, one can ctrl+click on individual stitches in the editor, and they will be highlighted in the 3D canvas (and vice versa), which allows for per-stitch editing of a crochet project.
Dialog options
Substitute index counters after expansion? If checked, index variables will be evaluated. For example, $k=0$, sc.L[k++], sc.L[k] will be written out as sc.L[0], sc.L[1].
Run this dialog twice in a row? If checked, the expansion is applied twice in one go. This is the recommended mode when you want stitches indexed in the editor, stitch numbers on hover, and cross-highlighting between text and canvas to work reliably.
Because expansion is a “destructive” operation, the dialog requires answering a simple arithmetic question before enabling OK.

When to use it
When editing a pattern at the individual stitch level.
When debugging a pattern and you want to see exactly what a multiplier or a definition expands to.
Before using Find Project Periphery labeling (the periphery tool expects expanded text when inserting labels onto individual stitches).
Tools → Simplify instructions
Objective. Expansion is great for debugging and for per-stitch tools, but expanded instructions can become long and repetitive. Simplify instructions attempts to compress repeated structures back into a shorter form (for example by factoring out repeated bracket blocks). This tool is EXPERIMENTAL.

Warning: this tool overwrites the text in the editor and may break your instructions. Save your work first.

What it does
Replaces repeated blocks such as [sc,dc],[sc,dc],[sc,dc] with a compact form such as 3[sc,dc].
Optionally tries to recognize “numerical indexing” in labels and replace it with index counters (so labels become compact and programmable again).
Dialog options
Expand before simplification? If checked, CrochetPARADE will run an expansion pass first (useful when the current text still contains shorthand that would otherwise block simplification).
Attempt to simplify numerical indexing of labels and create index counters? If checked, the tool will try to replace sequences such as ch.A[0], ch.A[1], ch.A[2], ch.A[3] with a counter-style form (for example using a variable and ++). This is particularly useful when you want to get back to a compact, programmable label form that is more succinct.
As with expansion, the dialog uses a simple arithmetic question to reduce accidental use.

Typical workflow
Run Tools → Expand instructions (often in “run twice” mode) to make per-stitch operations possible.
Do your per-stitch edits (for example: change individual stitches; add/remove stitches; color individual stitches; label periphery stitches; insert labels; etc.).
Run Tools → Simplify instructions to compress the result again for readability and sharing.
Tools → Object Transform
Objective. Some patterns create multiple disjoint crochet objects (for example: amigurumi limbs, appliqués, or motifs meant to be sewn on later). Object Transform provides an interactive way to translate and rotate those objects in the 3D view, so you can preview positioning and assembly without changing the crochet structure.

What it does
Opens a floating (draggable) control panel for transforming objects.
Lets you choose an Object number and adjust its translation and rotation.
Reads and writes transformations to your instructions via the special command TRANSFORM_OBJECT: (see the language reference).
Controls and options
Object: select which disjoint object to edit.
Translation: adjust x and y using the translation canvas; adjust z with the vertical slider or number input. Use Reset Translation to return to zero. Reset Min/Max resets the scaling of the control canvas.
Rotation: adjust two angles on the rotation canvas (alpha/beta) and use the gamma slider for the third angle. Use Reset Rotation to return to zero rotation.
Guiding plane and Guiding rotation axes: toggles for drawing visual guides while transforming.
Rotation order: choose the Euler rotation order (XYZ, YZX, ZXY, XZY, YXZ, ZYX). Switching between rotation orders allows one to avoid gimbal lock.
Read from instructions: loads existing TRANSFORM_OBJECT: lines for the chosen object.
Write to instructions: writes the current transform back into the editor as a TRANSFORM_OBJECT: line.
Note: object transforms do not change stitch connectivity. They only affect how disjoint parts are positioned in the 3D view and in exported 3D models.

Pattern generators
CrochetPARADE includes a few pattern generators that are accessed from the Write your own instructions drop-down menu. These are not “Tools” menu items, but they behave like tools: they open a dialog, generate instructions, and overwrite the editor text with the generated pattern.

Generate a sphere
Objective. Quickly generate a single-crocheted sphere (useful for amigurumi heads and bodies or test swatches in the round).

Circumference (in stitches): sets the approximate equatorial circumference. The dialog accepts values between 7 and 1200.
Scatter increases and decreases: distributes increases/decreases to reduce symmetric “bulges”, especially near the poles.
The generated pattern uses continuous rounds.
Generate an axially symmetric shape
Objective. Generate patterns for arbitrary axially (cylindrically) symmetric shapes made in single crochet (for example: amigurumi bodies, hats, buffs, tubes, and other “lathe-like” forms). You define a profile curve, and CrochetPARADE generates a stitch-count schedule that follows it.

The generator opens an interactive editor where you can drag control points of the profile curve (and add / delete points via a context menu).
Scatter increases and decreases: reduces distortions by distributing shaping more evenly.
Number of stitches between green grid lines: controls the “scale” of stitch density along the profile.
X-axis range and Y-axis range: set the working area of the curve editor (useful for tall or wide shapes).
Adjust number of stitches in the round (thickness curve): optionally enables a secondary editor that lets you tweak stitch counts at different locations, allowing extra fabric to be added that may help with intended shape recovery, say after stuffing a closed amigurumi model.
Export / Import: saves and loads the curve definition as a JSON file, so you can reuse a shape later or share the shape design separately from the crochet instructions.
Save/Export options
The project can be exported in different formats:

Plain text, which is suitable for sharing. Note that every line (indicating a new row/round) will be preceded by ¶ in order to ensure that spurious new lines introduced by sharing the instructions over text-platforms will not count. If such a text is pasted back into the platform, those extra ¶ symbols will automatically be deleted. The plain text also carries version information on top, which would ensure backward compatibility if the language evolves.

Print highlighted instructions in the way one sees them in the input field. Intended new lines are preceded by ¶ similar to above. Unintended new lines created by line-wrapping are not.

Save the project's nodes and edges to a DOT-like file. Node coordinates (if precalculated) are included as a tuple after the node name. Edge lengths are included as a float after each edge. Note that positions of stitches will be included if the model was calculated already. Also, note that the file is not fully compatible with Graphviz.

Export 3D GLTF model. The model that is exported can be previewed by pressing c once the 3D canvas has been selected. This file can be imported in Blender. Once the model is imported, the stitches can be combined into one object. Then one can add hairs to the cylinders representing the yarn, add textures, as well as physics such as gravity, cloth properties, etc.

Exporting to SVG creates 3 SVG files: 1) SVG image containing the crochet pattern using standard crochet symbols -- yarn colors are optionally included; 2) SVG image showing the current view (in 3D) or the face-on view (in 2D) of the project. That SVG shows stitch connections and identifies stitches by their type, row number, and position within a row. The SVG pattern shows the same information as standard crochet diagrams and can be used as a guide when crocheting. 3) Both diagrams overlaid on top of each other. The SVG crochet diagrams can be exported in orthographic or perspective projection as viewed in the 3D canvas.

Save debug info. This can be helpful when debugging the code. A json0 format of the project (an output similar to that of Graphviz) is saved in the debug info and can be used in other visualization software.

The CrochetPARADE language
Below is the description of the CrochetPARADE language used to enter crochet patterns on the platform.

Basics
Stitch Name/Basic Command	Description
ch	Chain stitch, the foundation for many crochet projects
ss	Slip stitch, used to join rounds or move across stitches without adding height
sc	Single crochet, a basic stitch that creates a tight, sturdy fabric
hdc	Half double crochet, taller than a single crochet but shorter than a double crochet
dc	Double crochet, a tall stitch that creates an open, airy fabric
tr	Treble crochet, a very tall stitch that creates an even more open fabric
dtr	Double treble crochet, an extra tall stitch for very open, lacy patterns
trtr	Triple treble crochet, an extremely tall stitch for creating dramatic height
rsc	Reverse single crochet, also known as crab stitch, creates a decorative edging
bp... (e.g., bpsc, bphdc, bpdc, bptr)	Back post stitches, worked behind the post of the stitch below for texture
fp... (e.g., fpsc, fphdc, fpdc, fptr)	Front post stitches, worked around the post of the stitch below for texture
...fl (e.g., scfl, ssfl, dcfl, hdcfl, trfl, dtrfl, trtrfl)	Stitches worked in front loop only, creating a horizontal ridge on the back of the work
...bl (e.g., scbl, ssbl, dcbl, hdcbl, trbl, dtrbl, trtrbl)	Stitches worked in back loop only, creating a horizontal ridge on the front of the work
hdcNpuff (hdc3puff, hdc4puff, hdc5puff)	Half double crochet puff stitch made with N loops, where N is typically 3, 4, or 5
dcNbobble (dc3bobble, dc4bobble, dc5bobble)	Double crochet bobble stitch made with N stitches, where N is typically 3, 4, or 5
tr4bobble	Treble crochet bobble stitch made with 4 stitches
dcNpc (dc3pc, dc4pc, dc5pc)	N-double crochet popcorn stitch, where N is typically 3, 4, or 5
picot3	A decorative loop made with 3 chain stitches and a slip stitch
longsc, longdc, longtr	Long sc/dc/tr, worked into a stitch in a previous row for added height
ring	A magic ring, forming a circular/point-like foundation for crochet projects
stitch_nameNinc, stitch_nameNtog	CrochetPARADE can handle automatically stitch increases and decreases with stitch_nameNinc and stitch_nameNtog, respectively. Here N is an integer denoting the number of stitches of the increase or decrease. For example: sc2inc corresponds to two single-crochet stitches worked into the same stitch; and sc2tog implies that one is doing a decrease by combining two single-crochet stitches.
sk	Skip stitch, used to create spaces or shape in the pattern
tie_up	Special command: ties up stitches -- used to secure yarn end at end of project.
start_at	Special command: creates a hidden stitch used to mark the starting point of a round or row. This marks starting with a new piece of yarn at a specified location in the project. Needs to be followed by a location, e.g. start_at@[-1,0]
start_anew	Special command: creates a hidden stitch indicating the beginning of a new section or pattern of a disjoint piece.
start_a_new_chain	Special command: Begins a new chain of stitches, often used to start a new row or section of a disjoint piece.
turn	Special command: turn for turning the work at the end of a row or round. (See "Direction of sequential stitch attachment." for more details.)
...	Special command: Ellipsis (...) in the beginning of a new line indicates the previous line is continued on the current line.
<
>	Special commands: These indicate a repetition starts/ends at that symbol. Example: 3*[sc,<,ch,>,dc] translates to [ch,dc],[sc,ch,dc],[sc,ch]
.
@
~^!	Special commands: Indicate a labeled stitch, attachment to a label/stitch, and modifiers, respectively. Example: sc.A,dc@A (see "Attachment to a label" in the Manual)
#comment
\comment\	Special commands: Allows inserting comments. The pound symbol indicates a comment that extends to the end of the line. Comments enclosed between backslashes can span multiple lines.
COLOR:
BACKGROUND:	Special commands: COLOR indicates the color of the yarn that follows, while BACKGROUND - the color of the background of the 3D rendering. See the Manual for allowed colors.
TRANSFORM_OBJECT:	Special commands: Automatically generated by the "Object Transform" tool, which interactively allows the user to move and rotate objects.
INDEX_ARRAY:	Special command: defines an index array that supplies counter values for an index variable used in stitch labels (for example A[k]). Typically generated by Tools → Find Project Periphery when “Save counter values as INDEX_ARRAY” is enabled. See the INDEX_ARRAY Command section in this manual.
SORT_LABEL:	Special command: defines an explicit processing order (permutation) for stitches that share the same label without adding a counter (e.g. A, A[], A[2,3]). Recommended for periphery labeling when the periphery is a single run of adjacent stitches not necessarily sequentially crocheted (if not, an error is generated). See Labeled groups with SORT_LABEL in the Labels section.
DOT:	Special commands: Any extra arguments to the physics engine. Some options that can be set here are: iterations, start, separate, inflate, learning_rate. Also, new nodes can be created and placed at particular 3D coordinates; and new connections between nodes can be specified here. See the DOT Command section in the Manual.
Stitches are defined using common names ch for a chain, sc for single crochet, ss for slip-stitch, dc for double crochet, etc. CrochetPARADE comes with built in set of some common stitches (see table above). Stitches can also be defined using methods described further below in this chapter.

Two special "stitches" are: sk for skip a stitch, and turn for turning the work. (See "Direction of sequential stitch attachment." for more details.) Note that, turn can only appear as a last "stitch" in a row, and should be followed by a new line:

10ch,turn
sk,ch,9sc,turn
sk,ch,9sc
CrochetPARADE can handle automatically stitch increases and decreases with stitch_nameNinc and stitch_nameNtog, respectively. Here N is an integer denoting the number of stitches of the increase or decrease. For example: sc2inc corresponds to two single-crochet stitches worked into the same stitch; and sc2tog implies that one is doing a decrease by combining two single-crochet stitches.

Stitching in the front and back loops is done by adding 'fl' or 'bl' at the end of a stitch name, such as scbl (single crochet in the back loop), dcfl (double crochet in the front loop), etc. By default, only the basic stitches (ss, sc, hdc, dc, tr, dtr,trtr) are supported with the 'bl' and 'fl' options. They are rendered in 3D by slightly shifting them behind and in front of the project for 'bl' and 'fl', respectively. If you want to add the 'fl/bl' option to other stitches, then one should use a raw stitch definition (see "Raw stitch definitions and grammar"). When exporting a crochet chart to SVG, 'fl' and 'bl' stitches are rendered using their standard symbols.

Front post and back post stitches are named with 'fp' and 'bp' preceding the stitch name. So, 'fpdc' is a front post double crochet. The difference in rendering the stitches is only in their default length -- a 'fpdc' is slightly shorter than 'dc' as the stitch starts lower as it is attached to the post, not the top V of a stitch. When exporting a crochet chart to SVG, 'fp' and 'bp' stitches are rendered using their standard symbols.

Stitches can be repeated by multiplying them with an integer, say 10*sc or 10 sc or 10sc would imply 10 single crochet stitches.

Each new line is a new row/round. Rows with stitches are enumerated in the editor. The enumeration will be inaccurate if you are repeating rows by multiplying whole rows with an integer. One can repeat rows by adding an extra new line in the end, encompassing the whole expression in parenthesis or brackets, and then multiplying by a number. For example

[10sc,turn
]*3
is parsed to:

10sc,turn
10sc,turn
10sc,turn
The last iteration can be ended prematurely by adding a > as in: [2sc,>,dc]*3 is parsed to 2sc,dc,2sc,dc,2sc. Similarly, the first iteration can start at a location marked with <. Thus, [2sc,<,dc]*3 will be parsed to dc,2sc,dc,2sc,dc. Note that > and < should be at the top level (meaning not nested within other parenthesis) of the iterated expression.

Rows/rounds that are too long can be wrapped by starting a new line with .... So:

3dc
... sc,turn
will be evaluated to 3dc,sc,turn as part of the same row/round.

Comments can be entered after # and end at a new line. Multiline (and single-word/single-line) comments can be entered between two back slashes \ . See the examples below.

One can change the color of the “yarn” by using COLOR: color of stitches to follow. For more information, see the dedicated chapter on color. The background color can be changed by setting BACKGROUND: color of background, appearing alone on a new line.

COLOR: rgb(126,8,80)
DOT: any extra arguments to the physics engine
# This is a comment. # This is also a comment
\this is a comment\ dc,dc, \this is also a comment\
dc
\this is a comment 
 that continues on this line # comment
 and this is a comment
 \

BACKGROUND: white
Color
Setting the yarn or background color is done by writing:

COLOR: color_name or hex color or rgb(r,g,b)
BACKGROUND: color_name or hex color or rgb(r,g,b)
The supported colors are any of the ones listed here. Hexadecimal color code is also supported. For more information, see the three.js documentation.

INDEX_ARRAY Command
INDEX_ARRAY: is a special command that defines an explicit list of integers for an index variable/a counter. This allows CrochetPARADE to assign index values to labels independently of crochet order. It is especially useful for edge/periphery labeling, where the boundary/labelling order is different from the stitch-creation order.

Syntax: one definition per line:

INDEX_ARRAY: k={4,3,1,2,0}
Meaning: whenever CrochetPARADE evaluates the index variable k inside label brackets (e.g. sc.A[k]), it will consume the next value from the array. If the array runs out of values, CrochetPARADE will report an error.

Why this matters: you can keep many stitches labeled with the same symbolic form (for example A[k]) while storing the actual sequence of index values separately in INDEX_ARRAY:. This is important if you expand instructions witn Tools → Expand instructions to label individual stitches and then later want to run Tools → Simplify instructions again: the simplification pipeline can remain efficient because the periphery indexing is not “baked into” the stitch text.

How to create it: the easiest way is to use Tools → Find Project Periphery and enable “Save counter values as INDEX_ARRAY” when applying labels to the periphery stitches. Advanced users may also write or edit INDEX_ARRAY: lines manually. For plain labels (labels without counters), you can store an ordering with SORT_LABEL: (below) without adding a counter.

When using INDEX_ARRAY:, the index can be used in labels in plain form (e.g. A[k]) or with an increment operater, e.g. A[k++] which means consume a value from the array, then skip the next value in the array (for future evaluations of k), or A[++k] (skip a value in the array, then consume the next one). Other arithmetic is not allowed.

SORT_LABEL
SORT_LABEL: is described in the Labeled groups with SORT_LABEL subsection in the Labels section. It lets you specify an explicit processing order for stitches that share a label without introducing a counter. Works only for a single run of adjacent stitches since they would share the same label!

DOT Command
One can add additional commands to the dot file by adding those after a DOT: at the beginning of the line:

    # a (hidden) node:
    DOT: "3,27B"
    # creating a new connection outside of a stitch of length 9.0:
    DOT: "1,54" -- "1,44" 9.0
    # iterations (default: 500) until the code terminates the computation
    DOT: iterations=1000
    # seed for the random number generator (default: 0):
    DOT: start=10
    # Factor by which to separate disjoint crochet pieces (default: 1.5)
    DOT: separate=0.8
    #The inflate keyword sets how much to "inflate" the project. 
    #It controls how much distant stitches (which are not 
    #directly connected) push off of each other. Setting this
    #parameter slows down the code by a factor of two or so.
    #The default value for inflate is infinity. Reasonable values 
    #to try are 0.5-3.0.
    DOT: inflate=2.0
    # The repulsion_radius allows for more localized repulsion between nodes when
    # inflating the model. It sets the maximum graph-theoretical distance for which
    # node repulsion is included. Nodes that are further away do not repel.
    DOT: repulsion_radius=10 # (Default: infinity)
    #The learning rate controls the rate at which the code converges. 
    #Setting it too high (above 0.15 or so) can cause failure to 
    #converge. Default: 0.1
    DOT: learning_rate=0.02
    # The viscous_iterations keyword sets the number of iterations 
    # for the "viscous relaxation" post-processing step, which helps 
    # fix overly loose or tight stitches after inflating the project with 'inflate'. Higher 
    # values allow more relaxation.
    # Default value: 10. 
    DOT: viscous_iterations=10 
    # The viscous_damping keyword controls how much resistance is applied 
    # during viscous relaxation. Higher values increase damping and slow relaxation; 
    # lower values speed it up. 
    # Default value: 1.0. 
    DOT: viscous_damping=1.0 
    # The viscous_timestep keyword sets the time step for each iteration 
    # during viscous relaxation, affecting how quickly adjustments are made. 
    # Smaller values result in finer adjustments but slower overall processing. 
    # Large values may lead to failure to converge.
    # Default value: 0.1. 
    DOT: viscous_timestep=0.1 
Locations of nodes as well as new hidden nodes outside of stitches can be specified as {x,y,z} (in units of a chain length) right after the node name. Below is an example

ring
sc5inc
2sc2inc,sc,2sc2inc
9sc
4sc2tog,sc
sc5tog
DOT: "1,0|1" {0,0,0}
DOT: "4,3|19" {1,0,0}
DOT: "new hidden node"
DOT: "0,0|0" -- "new hidden node" 0.5
DOT: "new hidden node" -- "3,4|11" 0.5
DOT: "new hidden node" -- "2,4|4" 0.5
DOT: iterations=4000
    
In the code above, the stitches "1,0|1" and "4,3|19", which are present in the original pattern (one can see them by running the instructions without the DOT command), are placed at particular 3D coordinates {0,0,0} and (1,0,0), respectively. Then a new hidden node is created, and the 3 stitches "0,0|0", "3,4|11" and "2,4|4" are placed equidistant from it (distance of 0.5 chain lengths apart). One can see all stitch/node names, locations as well as connections by selecting "Save file containing nodes and edges" from the Save/Export menu. The nodes and connections added by hand after the DOT command are appended at the end of the file.

TRANSFORM_OBJECT: command
Objects can be translated by {tx,ty,tz} units and rotated by the Euler angles {rx,ry,rz} (in radians) by specifying TRANSFORM_OBJECT:object_number,tx,ty,tz,rx,ry,rz This is best done using the "Object Transform" tool, which interactively allows the user to move and rotate objects. In this context, an object is a separately crocheted pattern, not connected to other patterns. See the Amigurumi example.

Specifying attachment points
Stitches on a given row/round are automatically attached one-by-one to consecutive stitches in the previous row/round. If the work is turned at the end of a row, then that is taken into account automatically.

However, in crocheting often one needs to attach (“work”) new stitches to non-consecutive previous stitches. To allow that, the code allows specifying attachment points after the @ symbol, following a stitch in a pattern, e.g. 3sc,dc@[-1,3],dc, which specifies that the attachment point of the dc stitch should be moved to the 4 stitch (stitch and row counting start from zero) of the previous row/round (specified with a negative index: -1). The next dc is worked in the stitch after that.

Important: The first explicitly specified attachment point takes precedence. For example, in (sc,dc@B,(tr@C)@D)@A, sc attaches to A, dc to B, and tr to C. That is true even if multiple attachment heads are specified. For example in (sc,dc@B,(tr@1C)@D)@A,hdc, the tr attaches to C and that attachment updates only the @1 attachment head. Therefore, the hdc attaches to the stitch after B (the last update to attachment head 0, specified with @) in the default order of attachment. Labels such as @A, attachmend heads such as @1 and order of attachment are all defined in what follows.

There are different ways of specifying stitch attachment points:

Beginning a new row/round: enter a new line (no explicit attachment point)
The very first attachment point is initialized at the first stitch by default. So, in 5ch,sc,dc, the sc attaches to the first chain and the dc to the second chain (counting from 1).

After a new line is entered in the text, the attachment sequence resets automatically, and the next stitch attaches to the first (or rather, 0th) stitch of the previous line if there is no turn on that previous line; or that next stitch attaches to the last stitch of that previous line if there is a turn command at the end of the previous line. Here is a contrived example:


8ch,ch.A,ch
9sc,turn
sk,ss,8sc,ch,turn
sk,hdc,sc@A,sc,dc
2sk,2ch,tr
Line 2: The first sc on the second line (counting from 1) attaches to the first chain of the first line. Then the next stitches attach in sequence along Line 1.

Line 3: The ss on the third line attaches to the 8-th sc of the second line. The reason is attachment starts from the last stitch (because of the turn at the end of Line 2), but the last sc is skipped by the sk at the beginning of Line 3. The next stitches attach in reverse sequence to the stitches in Line 2 because of the turn command at the end of Line 2 (see the section Direction of sequential stitch attachment). In this example, the last of the 8sc steps past the beginning of Line 2 and therefore attaches to the last chain of Line 1, which is the previous stitch worked (i.e. next attachmetn point counting in reverse order).

Line 4: There is a turn at the end of Line 3, so the attachment point resets to the last stitch of Line 3 after the new line. The hdc attaches to the last sc of the previous line (after the last chain has been skipped by sk). Then the sc@A attaches to the chain in Line 1 marked with ch.A (see the section on Simple labels below). The next sc on Line 4 attaches to the last chain of Line 1 (the direction of sequential attachment is forward as there are an even number of turns between Line 1 and Line 4). As we ran out of stitches on Line 1, the dc attaches to the first sc on Line 2 as that is the next stitch that was worked in the project (even though it was on the next row/round/line).

Line 5: The attachment point resets because of the new line. There is no turn at the end of Line 4, so the next attachment point is the first stitch of Line 4. The 2sk means that the hdc and the sc@A are skipped in Line 4. Therefore, the tr attaches to the second sc (right before dc) on Line 4. The chains do not have attachment points so they do not increment the attachment location.

Direct Attachment: @[2,10]
Direct attachment to a particular stitch coordinate specified as a pair of integers, e.g. @[2,10]. The first integer specifies the row/round number. The second integer specifies the stitch in that row. Counting of stitches/rows/rounds starts from 0, so in the example above, the attachment is at the 11-th stitch of the 3-rd row.

Negatives numbers imply counting from the end, starting with -1 meaning the last stitch/row/round; -2 the last but one stitch/row/round, etc. Counting of rows/rounds starts at the beginning of the project. Counting of stitches starts at the first stitch of the row as written down in the instructions, disregarding any turn directives. The current stitch row and stitch position can be specified using the % symbol, so @[%,%-3] implies the current row, three stitches back before the currently worked stitch.

Attachment with stitch type counting @[sc:-1,3]
Attachments with a stitch type before a colon specify that the counting of stitches in a row is over stitches of that type. For example, @[sc:-1,3] specifies that the current stitch is worked in the 4th single crochet (sc) stitch of the previous row, as opposed to the 4th stitch in general. The direction of counting is not necessarily in the direction in which the stitches were written (compare with above), but in the crocheting direction. See the section "Direction of sequential stitch attachment".

Attachment with Relative Position: @[@+1]
The last attachment point is stored in the @ symbol, which can be referenced in an attachment point. So, for example dc,dc@[@] implies that the second dc stitch should be worked in the same stitch as the previous dc stitch.

One can go up and down the row by adding integers to @. So, @[@+2] means attach two stitches after the last attachment point. The direction is in the direction in which we are working (see the section "Direction of sequential stitch attachment") , so turns are taken into account.

One can also combine relative position identifier with a stitch type identifier. For instance, @[sc:@+1] means attach to the next sc stitch after the last attachment point. In general, an attachment expression of the form @[TYPE:@+k] is evaluated in two steps:

1) First compute the base position by moving k stitches from "@" in the crocheting direction (the same direction as sequential attachment; turns are taken into account). This yields an intermediate stitch position "@+k" that is defined in terms of all stitches in the row, regardless of their type.

2) Then, starting at that intermediate position, search forward in the crocheting direction for the first stitch whose type matches TYPE. Attach into that stitch.
If no stitch of the requested TYPE is found at "@+k" or later in the crocheting direction, the parser must emit an error.
Notes:
- @[sc:@] attaches to the nearest sc stitch at or after "@". If "@" is already on an sc stitch, it attaches there. Otherwise it attaches to the next sc stitch.
- @[sc:@+1] first moves one stitch from "@", then searches for the first sc at or after that new position. If "@" was not on an sc stitch, @[sc:@] and @[sc:@+1] resolve to the same next sc stitch.
- In a labeled group such as (sc,dc)@[@+1], the label is distributed first and then each attachment is evaluated separately, so sc@[@+1],dc@[@+1] attach to consecutive stitches, not to the same stitch.
Attachment to a label
Simple labels
In crocheting, one often uses stitch markers to keep track of particular stitch positions. Similarly, any stitch here can be labeled with a label following a .. For example, in sc,sc.A,2ch the second sc is labeled with a label A. A stitch can have multiple labels that have the distributive property. So, (3ch.A,sc).B implies that all chains have both labels A and B, whereas the sc stitch carries label B only.

One can then work a stitch in that label by attaching to A by writing sc,sc.A,2ch,ss@A. When multiple similar labels need to be used, one can use labels that differ by internal labels that are integers, such as sc,sc.A[0],sc,sc,sc.A[1]. Here A[0] and A[1] are treated as different labels.

As mentioned earlier, a stitch can attach to one label only, inheriting the syntactically closest attachment. For example, in (sc@A)@B the sc stitch attaches to A. Attachment points also distribute. Thus, (sc,dc,sc@A,sc)@B is equivalent to sc@B,dc@B,sc@A,sc@B.

Labeled groups of stitches
Basics
When multiple stitches carry the same label, we will call that a labeled group. One can attach to the whole group, or particular stitches in the group. For example 5ch.A, the label A refers to the whole 5 chain group. One can envision attaching to the chain space of that group by doing: 5ch.A,dc,2ch,2sc@A. In this case, both sc stitches will attach to the chain-5 space and will be distributed uniformly over that space. If the uniformly distributed positions do not match preexisting nodes of stitches in the labeled group, then hidden nodes will be created in between and the stitches will attach to those. The distribution of hidden nodes is uniform along the length of the labeled group with the assumption that all stitches in a labeled group have the same width (stitch height can vary).

Important: A labeled group (multiple stitches with the same label, e.g. .A) must be a run of adjacent stitches. It is an error to use the same label on non-adjacent/disjoint stitches. Use different labels in the latter case, or use indexed labels (labels with counters) to mark distinct groups, e.g. .A[0], .A[1] (or .A[k++] with $k=0$ and increments). Adjacency is checked on the stitch graph. “Adjacent” includes direct top–top connections within the same stitch, and direct bottom-top attachments; connections that pass through hidden nodes do not count. If you use SORT_LABEL:, this adjacency check is applied after sorting.

Important: After sorting, the stitches for that label must still be adjacent in the stitch graph. If they are not adjacent, the parser throws Cannot use same labels over non-adjacent stitches. “Adjacent” includes direct top–top connections within the same stitch, and direct bottom-top attachment. Connections that go through hidden nodes do not count as adjacent and will trigger an error.

Important: Stitches that attach to a labeled group must attach to stitches that are already defined (= already crocheted/worked) at that point in the instructions. In practice, this means: attach into previous stitches/rows, not into stitches that appear later in the instructions text.

Just for fun, here is an extremely contrived example which at first glance seems to violate both the adjacency and the future rules above and yet it does not: 
9ch,(ch.B).A,ch,dc@A,tr.A@B,2hdc@A
Explanation: The labeled ch and the tr share the same label A and are adjacent (tr attaches to B, which is a label carried by ch; hence the two stitches share a bottom-top node connection). The labeled group A has two stitches: 1ch, 1tr. There are three stitches worked into A: 1dc, 2hdc. The code then figures out that the dc attaches to the first stitch in the labeled group (the chain), which is not a future stitch relative to the dc; the last hdc attaches to the tr (which is not a future stitch relative to the hdc's); and the first hdc attaches into an interpolated hidden stitch lying between the ch and the tr.

Attaching to the the post of a stitch: .A^ .A^1
To attach to the post of a stitch, follow the definition of the label with a caret, ^. An integer can follow ^ specifying which post of the stitch to attach to if more than one. For example:

8*ch,turn
7*sc,dc.B^,turn
5ch,4*sc@B
Here is two example with two different posts as attachment points:

8ch,turn
6sc,dc2tog.B^0,turn
5ch,4*sc@B
which can be compared with:

8ch,turn
6sc,dc2tog.B^1,turn
5ch,4*sc@B
Skipping border stitches of a group: .A! .A!0 .A!1
If one wants to attach a set of stitches to a stitch group, then the default is that the two border stitches (first and last) of the group are valid attachment points of the set. One may however, want to skip those, and instead attach in the spaces and stitches in between those border stitches. Then adding defining a label, one can add ! if one wants to skip both bordering stitches, !0 if one wants to skip the beginning stitch, and !1 if one wants to skip the last stitch.

Here is an example:

10ch,turn
sk,9sc,turn
ch,2sc,4ch.A!,4sk,3sc,turn
4ch,5sc@A,4ch,sc
The 5 sc stitches will attach in the 4-chain space labeled with A, avoiding the first and last ch. Render the same instruction set with 4ch.A, 4ch.A!0, 4ch.A!1 to see the difference. Note that the reference @A should not contain the ! instruction.

One can combine the ! modifier with the ^ modifier:

8*ch,turn
7*sc,dc.B^!,turn
5ch,4*sc@B
Here is a topology that is a bit more involved:

9ch,turn
8sc,dc.A^,turn
4ch,[sc,sc.B^!,sc]@A
4ch,3sc@B
Adding edge stitches to a group: .A+ .A+0 .A+1 .A+! .A+!0
Let’s say, you’d like to attach stitches in a chain space. If you want the stitches to fill in the space evenly up to the stitches bordering the chain space, you would have to add the stitches before and/or after the chain space to the labeled chain-space group. That can be cumbersome. So, to do that automatically add a + after the chain-space label definition to add both bordering stitches, or +0/+1 to add the previous/next borderingstitch.

Compare the following:

8ch,turn
2sc,3ch.C+,2sc,turn
3ch,5sc@C,sc@[-1,0]
with

8ch,turn
2sc,3ch.C+!,2sc,turn 
3ch,5sc@C,sc@[-1,0]
and with

8ch,turn
2sc,3ch.C,2sc,turn
3ch,5sc@C,sc@[-1,0]
Reversing the order of attaching a set of stitches to a group of stitches: @A~
When attaching a set of stitches to a group of stitches, the code is trying to do its best, to order the attachments in a way that is least disruptive (i.e. twisting) to the project, but sometimes it fails. For example, render the following:

10ch,turn
sk,8sc,sc.A!,turn
4ch.A!,sk,9tr,turn
1ch,sk,8sc,7sc@A
If you want the 7 sc stitches attaching to the 4-chain group be attached in reverse order, then append a tilde, ~, to the end of the attachment label, as in:

10ch,turn
sk,8sc,sc.A!,turn
4ch.A!,sk,9tr,turn
1ch,sk,8sc,7sc@A~
Compare with the result from running the previous set of instructions.

Note that the syntax of CrochetPARADE distributes labels over sets of stitches. So, (3sc).A~ is the same as sc.A~,sc.A~,sc.A~. Thus, in the example below, the two sets of (3sc).A~ are treated as one set of (6sc).A~. So, the code reverses all 6 stitches and then attaches them to the group A.

9ch,turn
sk,(ch,5sc).A,3sc,turn
sk,2sc,3sc@A~,3sc@A~
is the same as:
9ch,turn
sk,(ch,5sc).A,3sc,turn
sk,2sc,6sc@A~
If one wants to attach the first 3sc in reverse and only then reverse the next 3sc and attach those in turn, one must use stitch sets (see "Multiple stitch sets attaching to a labeled group") as:

9ch,turn
sk,(ch,5sc).A[],3sc,turn
sk,2sc,3sc@A[;0]~,3sc@A[;1]~
If however, one mixes normal (forwards) and reverse (backwards) attachment as in:

9ch,turn
sk,(ch,5sc).A,3sc,turn
sk,2sc,3sc@A~,3sc@A
Then the first 3sc and the second 3sc are now treated as separate sets. The code attaches the first 3 in reverse order, and then the next 3 in normal order. In other words, the above example is equivalent to:

9ch,turn
sk,(ch,5sc).A[],3sc,turn
sk,2sc,3sc@A[;0]~,3sc@A[;1]
and similarly for any combination of forwards and backwards attachments. Therefore, the following two examples are equivalent:

9ch,turn
sk,(ch,5sc).A,3sc,turn
sk,2sc,2sc@A~,2sc@A,2sc@A~
is the same as

9ch,turn
sk,(ch,5sc).A[],3sc,turn
sk,2sc,2sc@A[;0]~,2sc@A[;1],2sc@A[;2]~
See the section "Direction of sequential stitch attachment" for the way the code chooses the default direction of attaching stitches.

Multiple stitch sets attaching to a labeled group: @A[2;1]
If one needs to attach multiple sets of stitches into a labeled stitch group, then the order in which those sets are attached can be specified with a semi-colon as follows: 6dc.A[12],5ch,3sc@A[12;1],3sc@A[12;0]. In this example, the second set of 3 sc stitches will be attached to the first 3 dc stitches, and the first 3 sc’s will attach to the second 3 sc’s. Note that to use this functionality, one needs to have a label with square brackets, such as A[12]. If no order is specified, then the stitch sets are attached in the same order as written, so in 6dc.A[12],5ch,3sc@A[12],3sc@A[12], the 6 sc stitches attach consecutively in the 6 dc stitches.

Note that each set can be reversed if you append a ~ at the end of the attachment label. Compare:

10ch,turn
sk,8sc,sc.A[]!,turn
4ch.A[]!,sk,9tr,turn
1ch,sk,8sc,3sc@A[;1]~,4sc@A[;0]
with

10ch,turn
sk,8sc,sc.A[]!,turn
4ch.A[]!,sk,9tr,turn
1ch,sk,8sc,3sc@A[;1],4sc@A[;0]
Attaching to a particular stitch in a labeled group: @A[][2]
If one wants to attach to the k-th stitch carrying the same label, then same as above, one needs to have a label with square brackets, such as A[0] and the stitch position would follow in another set of square brackets: e.g. @A[0][k] attaches to the k stitch of the stitch group labeled A[0]. Counting is in the same direction as the default stitching direction (see "Direction of sequential stitch attachment" below).

Labeled groups with SORT_LABEL
For plain labels (labels without counters such as .A, .A[], .A[2,3]), you can control labeled-group ordering with SORT_LABEL: rather than adding a label counter. This is especially useful when the label is produced by the Tools → Find project periphery tool or any time you are labelling stitches that are adjacent (a requirement for any labeled group!) but NOT sorted by adjacency and need resorting.

SORT_LABEL: stores an explicit processing order for stitches that share the same label. The line has the form:

SORT_LABEL: A = {3,4,2,1,0}
This means: collect the labeled stitches in the order they appear in your instructions (in the order they are crocheted); i.e. turn instructions have no effect on order. Then re-order that list so the 3rd stitch becomes 0-th, the 4th becomes 1st, the 2nd stays 2nd, etc. In other words the zeroth stitch worked into the group labelled by A will be worked into 3rd stitch of that group; the 1st stitch worked into A, will be worked into the 4th stitch the group labeled by A, and so on. The array is interpreted as 0-based, although 1-based indexing (1..N) is also accepted and will be converted to 0-based.

The label name can be A, B[], C[0], D[1,2], etc. SORT_LABEL: is not specific to the Periphery tool (although that tool can generate it for stitches around the periphery of your project); you may write it manually for any label.

If your label uses edge-piece syntax (e.g. .A+1), edge pieces are added after sorting when SORT_LABEL: is present. To avoid ambiguities, you should add labels to the edge nodes by hand.

Important (sorted labels only): When SORT_LABEL: is present, and a labeled stitch expands to multiple nodes (for example increases like dc2inc), the sorter will try both top-node orders (left-to-right and right-to-left) for that stitch before evaluating adjacency, so that adjacency can be preserved after sorting. No such internal re-ordering is attempted when SORT_LABEL: is not used for that labeled group.

Labels with counters: @A [++k] and .A[++k]
Note that often, one needs to create multiple labels in an algorithmic fashion. One can then use a counter (a variable initialized to an integer and then possibly incremented). One initializes the counter by placing the intializing expression between two $ signs, say $k=0$ at the beginning of a line. Then one can increment that value by using the ++ or -- operators , or writing prev k (same as --k) or next k (same as ++k). For example, $m=0$, sc.A[m],sc.A[m++],sc.A[m],sc.A[++m],sc.A[m],sc.A[prev m],sc.A[m] is evaluated to sc.A[0],sc.A[0],sc.A[1],sc.A[2],sc.A[2],sc.A[1],sc.A[1].

Note that when distributing labels with counters, the counter is evaluated first before distribution when the stitches are enclosed in parentheses/brackets, or when an integer precedes a SINGLE stitch (not enclosed in brackets) without the * symbol. So, $k=0$,2sc.A[k++],(dc,dc).A[k] evaluates to sc.A[0],sc.A[0],dc.A[1],dc.A[1]. If a stitch is multiplied by an integer using the * operator, then the label is distributed before evaluating the counter. For example, $k=1$, 3*dc.A[k++] evaluates first to $k=1$,dc.A[k++],dc.A[k++],dc.A[k++] and then to dc.A[1],dc.A[2],dc.A[3], whereas $k=1$, 3dc.A[k++] would evaluate the counter before distributing the label to give dc.A[1],dc.A[1],dc.A[1].

Note that if there are brackets/parenthesis, then omitting the * operator changes nothing. So, $c=0$,2[sc].A[c++] is the same as $c=0$,2*[sc].A[c++] and evaluates to [sc].A[0],[sc].A[1], and same for multiple stitches inside the brackets.

Also note that definition substitution is done last after labels are evaluated. Therefore, the picot stitches below, 3p.A[k++], are treated similar to 3sc.A[k++], giving p.A[0],p.A[0],p.A[0]. Those 3p's are not equivalent to 3*p.A[k++], which in turn evaluates to p.A[0],p.A[1],p.A[2]. Here is the complete code: 
DEF: p=3ch,ss@1[%,%-4]
$k=0$,3p.A[k++]
The above treats p as a single stitch, despite its definition as a series of 4 stitches. So, it is first parsed to 
DEF:p=3ch,ss@1[%,%-4]
$k=0$,[p,p,p].A[k++]
which is then evaluated to 
DEF:p=3ch,ss@1[%,%-4]
[p,p,p].A[0]
as explained above.

Note that counter algebra is permitted in the indexing. So, for example $k=3$,sc@A[(k++)%5]*5 would use the mod operator %, and would be parsed to sc@A[3],sc@A[4],sc@A[0],sc@A[1],sc@A[2]. This is especially useful when going in rounds, and the first label that you attach to is not of index 0.

One can evaluate counters in indices by selecting "Expand instructions" and checking "Substitute index counters after expansion?"

CrochetPARADE also offers a "Simplify Instructions" and selecting "Attempt to simplify numerical indexing of labels and create index counters?" The code then tries to replace expressions such as replace expressions such as ch.A[0],ch.A[1],ch.A[2],ch.A[3] with ch.A[$vara=0$vara],3*ch.A[++vara]

Multiple attachment heads: @0 @1 @2
Note that in crocheting we may be going back and forth between crocheting in different rows, or more generally in different locations in a project. Then to keep track of where we are in those different attachment locations, we can use different “attachment heads”, each one labeled with an integer after the @ symbol (the default @ implies @0). The attachment head counters are independent. So, for example: sc@[-1,2],dc@1[-2,3],sc@[@+2],dc@1[@1+2],tc will attach the second sc at [-1,4], and the second dc at [-2,5]; the tc will attach to the next stitch on the default head, so to [-1,5] (same as tc@[@+1]). We can use any of the labeling methods described above with any of the attachment heads.

Attachment of an empty stitch
One can reset the attachment point anywhere in a row by using an empty stitch. For example, sc,dc,@[@-1],tr is equivalent to sc,dc,tr@[@], both forcing the tr and dc stitches to attach to the same point. The logic is that the last attachment point after dc, is shifted back to the attachment of sc by the operator @[@-1], so the next stitch tr attaches to the attachment point of dc.

Direction of sequential stitch attachment.
If no attachment point is specified, the code tries to infer the next attachment point of the next stitch you are working into your project. It does that by checking how many turn directives are at the end of the rows between the row (let's call it A for reference) of the attachment point of the previous stitch and the current row. If that number is even, then the next stitch would by default attach to the next stitch of A in the direction in which A was crocheted. If that number is odd, then the next stitch would attach to the previous stitch on A (as we are going in reverse order). This would match the natural direction in which one crochets when executing the actual project.


If one is stitching in a labeled group of stitches by attaching to that label, then the default direction of crocheting is determined by the number of turn directives between the row of the first stitch of the labeled group and the row of that stitch of the set of stitches worked into that labeled group that comes first after the following is done: 1. If multiple sets of stitches attach to the same labeled group, sort them according to the order specified after ; (as in stitches attached to ,A[0;0] come before A[0;1]); and 2. Reverse the order of any set that has a modifier ~ after the attachment label (e.g. @A~).
Note: A turn directive inside a bracketed stitch set that attaches to a labeled group (e.g. [7dc,turn 6dc]@A) does not split the attachment into multiple stitch sets and therefore does not affect the attachment direction mid-stream. The attachment direction is chosen once for the stitch set (after sorting by ; and applying any ~ reversals). If you need different directions or ordering across multiple attaching segments, use stitch sets with A[] and @A[;i], and use ~ to reverse a particular set.

For example, the following two instruction blocks are parsed identically (the internal turn inside the @A block does not affect the attachment direction):

[9ch,turn
sk,8sc].A,ch,turn
sk,8sc,turn
[7dc,turn
6dc]@A
and

[9ch,turn
sk,8sc].A,ch,turn
sk,8sc,turn
[7dc,
6dc]@A
To control ordering/direction across segments, use @A[;0], @A[;1], etc., and append ~ to reverse a specific segment.

A stitch following a stitch (or a set of stitches) attached to a labeled group of stitches, attaches to the stitch following the whole group. Therefore in both examples below, the tr stitch attaches to the dc, even when the 4sc are attaching to A in reverse order (as indicated by the tilde):

6ch,turn
        sk,2ch,dc,2sk,(3ch).A,2sc,turn
        sk,ch,sc,4sc@A,tr
and

6ch,turn
        sk,2ch,dc,2sk,(3ch).A,2sc,turn
        sk,ch,sc,4sc@A~,tr
And in the example below, both tr are attaching to the same dc, as the attachment point is moved back to the last stitch of A by the @A's right before each tr:

6ch,turn
        sk,2ch,dc,2sk,(3ch).A,2sc,turn
        sk,ch,sc,2sc@A,tr,2sc@A,tr,sc
If working stitches in the post of a stitch using a caret (for example .A^), then the default direction of crocheting is from the attachment point of the stitch to the top of the stitch, unless there is an odd number of turn directives between the row of the top of that stitch and the first stitch of the set of stitches that are worked into the post (after the same sorting has been done as in the previous paragraph).

Note: When attaching to stitches, the stitches that are enumerated correspond to all top nodes (see "raw stitch definitions" below) present in the stitches. That means that a stitch (say sc2inc, which is 2 sc in the same stitch) with two top nodes, will have each of those top nodes enumerated with sequential numbers in the row/round that is being worked. Stitches without top nodes (e.g. internally a skip, sk, is treated like a stitch without a top node) are not enumerated and therefore one cannot attach a stitch to them.

Defining new stitches.
New stitches are defined using DEF: definition, which should be placed alone on a new line.

Creating an alias
If you are using a sequence of stitches over and over again, you may want to create an alias for them. The syntax for that is:

DEF: new_stitch_sequence_alias=stitch1,stitch2,...
#Example:
DEF: p=3ch,ss@5[%,-4] 
# Used an arbitrary attachment head 5 (@5), different from the default.
# A similar stitch alias is used in the Flower example.
One can use an alias in a pattern in the same way one uses any stitch, with one notable exception: An alias will increase the stitch count in a row not by 1 but by however many stitches are in the sequence. The way an alias is handled is by a simple string substitution, so the calculated result will not reference the name of the alias in any way.

The stitch alias p in the example above is a picot-3 stitch: ch 3,then slip stitch into the stitch preceding the picot stitch.

An alias substitution is done before counter evaluation. Therefore in the following example:


$k=0$
DEF: scA=sc@A[k]
5ch,ch.A[0],ch.A[1],ch,turn
$k=1$,sk,3ch,scA
the stitch scA is replaced first by the literal sc@A[k] and only then k is evaluated as 1 (because of the preceding $k=1$), resulting in sc@A[1]. Therefore, the sc attaches to the second labeled chain (ch.A[1]) and the first $k=0$ has no effect.

Copying a stitch (with modifications).
Let us say a pattern requires you to use the reverse single crochet stitch (rsc). That stitch has roughly the same overall geometry (height and width) and topology (connectedness) as the single crochet stitch, so you can simply use the sc stitch. However, let us say you would like to use the name rsc in the pattern. Using DEF: rsc=sc is an option, but the name rsc will not appear in the rendered project. If you would like that name to show up in the rendered project as well, then you can Copy() the stitch: DEF: new_stitch=Copy(old_stitch_name) # Example: DEF: scbl = Copy(sc) # This stitch is used in the Baby Bootie example.

If you would like to adjust the height of the newly created or a pre-existing stitch, you could do: DEF: new_stitch=Copy(old_stitch_name,new_height) # Example: DEF: dc=Copy(dc,3) # This stitch modification is used in the Blanket example.

The example above overwrites the dc stitch with a new height of 3 units.

You can also change the width of a stitch: DEF: new_stitch=Copy(old_stitch_name, new_height, new_width) # Example: DEF: narrow_sc=Copy(sc,1,0.8) # Note: You have to specify the height if you are specifying # the width, as those are positional arguments.

Raw stitch definitions and grammar.
One can use “raw stitch” grammar to define new stitches in a concise manner. Internally, the code defines basic stitches using that shorthand notation. Stitches written that way are then translated to a JSON format internally. The grammar for defining a new stitch is as follows:

DEF: new_stitch=&comment^top_nodes:bottom_nodes~attachments:other_nodes:connections
The terms “top nodes” and “bottom nodes” here refer to specific parts of a crochet stitch. The top node corresponds to the top of a crochet stitch, often identified by the ‘V’ shape formed at the top of the stitch. This is where the hook is inserted when working a traditional crochet stitch. The bottom node, on the other hand, refers to the attachment points of the crochet stitches, which are the top nodes of other stitches previously made.

Here is a breakdown of the different components of a new stitch defined this way:

Comment
The comment field is optional and is defined at the beginning of the stitch definition, after the & symbol and before the ^ symbol. They can be a brief description of the stitch, but are not used in the code. The comment cannot contain any of these characters: ^:~. For example, in the stitch definition &a sc cluster of 3 stitches^A(sc):B~A-B:C;D;E;F;G;H:!-1-A;B-1/3-C;C-1/3-D;D-1/3-A;B-1/3-E;E-1/3-F;F-1/3-A;B-1/3-G;G-1/3-H;H-1/3-A, the string a sc cluster of 3 stitches is a comment.

Top Nodes
Top nodes are defined after the ^ symbol and are separated by semicolons. Each top node must have a stitch type specified in parentheses after the stitch name. For example, in the stitch definition &sc2inc^A(sc);B(sc):C~::!-1-A;A-1-B;C-1-A;C-1-B, A(sc) is a top node where A is the stitch name and sc is the stitch type. The order in which the top nodes are written specifies the order in which they are chained together.

Bottom Nodes
Bottom nodes are defined after the first : symbol and are separated by semicolons. Unlike top nodes, bottom nodes do not have stitch types specified in parentheses. Instead, they may have an optional number prefix that indicates the attachment depth. For example, in the stitch definition &funky^A(funky):B;2C;D~A-D::!-1-A;B-1-A;C-1-A;D-1-A, B is a bottom node with an attachment depth of 1 (default when no number is specified), where C has an attachment depth of 2, meaning Stitch A attaches to the attachment point of C, and not to C directly.

A bottom node followed by [front] or [back] specifies that the stitch is worked in the front/back loop/post. For example, the default definition of double crochet in the back loop is &dcbl^A(dcbl):B[back]~A-B::!-1-A;B-2-A. The default amount of "sticking" distance in front/in the back is 0.2 times the chain length. You can change that by adding a number after front/back. So, for example the definition of front-post double crochet is: &fpdc^A(fpdc):B[front0.6]~A-B::!-1-A;B-1.5-A

The order in which the bottom nodes are written specifies the attachment order of the current stitch to the top nodes of the previous stitches.

Attachments
Attachments are defined after the ~ symbol and are separated by semicolons. Each attachment is a pair of top and bottom node names separated by a -. The top node name must come first, followed by the bottom node name. For example, in the stitch definition &ss^A(ss):B~A-B::!-1-A;B-0.4-A, A-B is an attachment indicating that top node A is attached to bottom node B. This is only used for finding the attachment point of a stitch, which has an attachment depth greater than 1.

Other Nodes
Other nodes are defined after the second : symbol and are separated by semicolons. Each other node must have a stitch type specified in parentheses after the stitch name. If no stitch type is specified, it defaults to 'hidden'. For example, in the stitch definition '&a sc cluster of 3 stitches^A(sc):B~A-B:C;D;E;F;G;H:!-1-A;B-1/3-C;C-1/3-D;D-1/3-A;B-1/3-E;E-1/3-F;F-1/3-A;B-1/3-G;G-1/3-H;H-1/3-A', nodes C through H are all “other” nodes with type set to hidden.

Connections
Connections are defined after the third : symbol and are separated by semicolons. Each connection is a pair of node names separated by a -, with a length value in between the hyphens. The first node (the tail of the connection) name must come first, followed by the length value, and then the second node (the head of the connection) name. For example, in the stitch definition &ss^A(ss):B~A-B::!-1-A;B-0.4-A, !-1-A and B-0.4-A are connections indicating that node ! is connected to node A with a length of 1, and node B is connected to node A with a length of 0.4. Note that node ! represents the previous stitch, which the current stitch is connected to.

Connections can be hidden, by preceding a connection with a *. For example, *Z-3-F is hidden, and is only rendered as thin gray threads.

If one wants to add a top node that is disjoint from the previous top node, then one can use a length of skip for that connection. So, for example the internally defined “stitch” start_anew is defined as &start_anew^A(hidden):~::!-skip-A. Thus, there is no connection between the next stitch and the previous stitch, similar to starting a new part of the project.

Recommendations: If using "Transform objects" to move/rotate disjoint objects (as in the limbs of amigurumis), you want to make sure that object detection works properly. For that, ensure that the connections for stitches that are not supposed to lead to disconnecting one object from another (i.e. all stitches except "start_anew" or "start_a_new_chain") have all hidden and top nodes connected to previous nodes. Thus, in writing out the connections, make sure that there is at least one connection to each hidden/top node (call it "A") that runs towards that node (say "!-0.5-A"). Also, when writing out the connections, I recommend you list the "blue" (top-level) connections first. This ensures that node placement is correct when exporting crochet charts to SVG. All standard stitches follow these guidelines.

Limitations, pitfalls and workarounds
Pitfalls
Do not use variables with the same name as a stitch. (Would be nice to fix this.)

Do not define stitches with the same name as variables. (Would be nice to fix this.)

An attachment point using @ as a coordinate, e.g. @[@+1], cannot work unless there was already at least one attached stitch on that row/round. That assigns the value of "@" to which we add the 1 in this example. This is by design.

The turn directive, should always be the last in a row/round/line of the code. No stitches can follow it, unless they are on a new line.

If your project looks inside-out, or equivalently it seems it is following left-hand crochet directions, then you should try using another start value (set DOT: start=2 or if unsuccessful, try other values). The reason is that the physics engine does not know which side you intend to be inside and which the outside. So, it picks at random. That is why playing around with the initial random seed by setting a start value will help resolve this.

Limitations
Crocheting in the front and back loops is supported by adding 'bl' or 'fl' after standard crochet symbols such as 'scbl', 'dcbl', etc. or by using custom stitch definitions using the raw stitch grammar as explained previously. However, the implementation is not perfect. Experiment with different starting seed values, e.g. DOT: start=12  if the stitches do not look quite right.

In most experiments I have run, the computation engine converges to within 10% of the requested stitch lengths (even when it should get them exact) when using the default settings. So, take any variations of that magnitude as spurious. That is why only stitches over/under stretched by about 15% are shown when ‘s’ is pressed.

Any stitch information beyond stitch attachment (topology) and lengths should included as comments as it cannot be captured by the platform.

The computational engine is not yet aware when stitches cross. So for example, when creating a 3D project for a flower with picots in a loop in the center of the flower, the picots sometimes may be sticking in front or behind the petals. The only workaround for now is to try a different random seeds by setting start to some random integer. For example:

DOT: start=34254 
