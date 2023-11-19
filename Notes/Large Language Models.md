## Large Language Models

I am recently brainstorming about large language models for interoperation with software applications which utilize interactive multi-threaded scripting environments. Software applications of interest to me, in these regards, include, but are not limited to: IDEs, image-editing, 2D and 3D graphics, and computer-aided design and engineering tools.

I am looking forward to utilizing large language models capable of managing object-reference variables while participating in co-creative dialogs. By "managing object-reference variables in scopes", I mean obtaining those variables returned from previous function invocations and utilizing them as input arguments to subsequent function invocations, including after interspersed co-creative dialog or other joint tasks occur.

Here is a clarifying example from the GPT × Blender domain:

1. A user creates a 3D object through dialog with an AI system. The AI system invokes an object-creating function. This function returns an object reference for the AI system to subsequently use to refer to that object: `object_22841ede_6839_4480_a324_23efa147e4f4`.
2. As the user conversationally interacts to adjust the mesh of that object, the AI system utilizes the object reference: `object_22841ede_6839_4480_a324_23efa147e4f4` in function invocations.
3. The user creates and describes a new material. The material-creation function returns a reference for the AI system to subsequently use to refer to that material: `object_648a30dd_6290_4c2c_918f_6f69e4ac6e7d`.
4. The user wants to put that material on that object. The AI system utilizes both object references, invoking a function: `apply_material_to_object(object = object_22841ede_6839_4480_a324_23efa147e4f4, material = object_648a30dd_6290_4c2c_918f_6f69e4ac6e7d)`.

Functions could also provide multiple return values or otherwise provide useful JSON structures utilizing well-known schemas. These complex return values could include both object references and action references. Reasons for returning action references include enabling users to easily use the conversational user interface to undo, redo, rollback, and commit actions, including in transaction scopes.

Useful functions for a software application to provide to AI systems would include:

1. `list_all` would list all of the object references that a software application is providing to an interoperating AI system.
2. `list_some` would filter those object references using a provided predicate, e.g., to list those objects of a type.
3. `addref` would increment the reference count of an object reference. Alternatively, AI systems could be provided weak references, references to a cache-based system, or utilize other interprocess object-reference passing techniques.
4. `release` would release an object reference, decrementing its reference count. Alternatively, AI systems could be provided weak references, references to a cache-based system, or utilize other interprocess object-reference passing techniques.
5. `typeof` would return a list of types, interfaces, and categories for a referenced object.
6. `describe` would provide a natural-language description of a referenced object to an interoperating AI system.
7. `inspect` would select and/or highlight a referenced object in a visual workspace and provide an AI system with one or more screenshots of it (e.g., front, side, top, and custom).
8. `history` would provide a history of actions in which an object reference was utilized.

## Prompt Engineering and Application Programming Interfaces

Prompts to large language models could come to include both described objects and functions. Described objects could be considered for use as arguments to AI-invoked functions.

Function descriptions could also include [action-language](https://en.wikipedia.org/wiki/Action_language) or natural-language content for expressing functions' preconditions and effects.

## Supporting Multiple User Interfaces

Advanced topics include enabling users to interchangeably and seamlessly utilize both traditional graphical user interfaces and new conversational user interfaces. That is, were a user to create a 3D object manually (utilizing the traditional user interface), the interoperating AI system would, if connected, be apprised of these occurrences, receiving a natural-language "narration" of the events as well as the relevant object references.

That is, software applications could "narrate" to interoperating AI assistants those user activities performed using traditional user-interface components. These data could be stored in multimodal dialog threads and could be accompanied by object and action references. This would create and enhance the illusion that interoperating AI systems were aware of user activities and occurrences in application workspaces.

Under the hood, these functionalities could be provided by [event-based architectures](https://en.wikipedia.org/wiki/Event-driven_architecture) which enable event listeners to subscribe to software events raised as users perform tasks utilizing traditional user-interface components.

## Supporting Durative Tasks

Advanced topics include supporting session capabilities so that users can close and reopen their software applications while performing durative design and engineering tasks.

## Context Management

Teams of users and AI systems could collaborate with one another across multiple simultaneous dialog threads. For example, designed parts in larger assemblies could each have a dialog thread.

Beyond scrollable hypertext transcripts, representations of dialog histories could resemble [Mathematica](https://en.wikipedia.org/wiki/Wolfram_Mathematica) or [Jupyter](https://en.wikipedia.org/wiki/Project_Jupyter) [notebooks](https://en.wikipedia.org/wiki/Notebook_interface).

Collapsibility and expandibility could be provided for dialog transcripts and/or notebook contents. This would allow users to rapidly navigate between task contexts.

## Multiagent Systems

Considering new and emerging technologies, e.g., AutoGen, one can readily envision [multiagent systems](https://en.wikipedia.org/wiki/Multi-agent_system) performing design and engineering tasks and subtasks on behalf of users. One can also envision multi-participant, team dialogs occurring interoperably with software applications and their interactive scripting environments.

Benefits of the indicated approaches include support for multiple tasks and threads; object-reference variables could be shared between multiple AI systems in multiagent collaborations.

## Multimodal Dialogs

In addition to attaching images to multimodal dialogs, files for 3D objects could be attached, e.g., [glTF](https://en.wikipedia.org/wiki/GlTF) and [Universal Scene Description](https://en.wikipedia.org/wiki/Universal_Scene_Description) files.

## Selected Previous Works

* [AutoGen](https://github.com/microsoft/autogen)
* [Jupyter AI](https://github.com/jupyterlab/jupyter-ai)
  * [Generative AI in Jupyter](https://blog.jupyter.org/generative-ai-in-jupyter-3f7174824862)
* [Microsoft Copilot](https://en.wikipedia.org/wiki/Microsoft_Copilot)
