## Large Language Models

I am recently brainstorming about large-language-model-based AI systems which can utilize scripting environments while interacting in dialog threads. With the unfolding capabilities of large language models, these scripting environments could be multi-threaded or otherwise concurrent.

I look forward to utilizing large language models which are capable of managing variables in scopes while engaging in co-creative dialogs. By managing variables in scopes, I mean obtaining variables returned from function invocations and using these variables as input arguments to subsequent function invocations.

Here is a clarifying example from the GPT×Blender domain:

1. A user creates a 3D object through dialog with an AI system. The AI system invokes an object-creating function. This function returns an object reference for the AI system to subsequently use to refer to that object: `object_22841ede_6839_4480_a324_23efa147e4f4`.
2. As the user verbally interacts to adjust the mesh of that object, the AI system utilizes its object reference: `object_22841ede_6839_4480_a324_23efa147e4f4` in function invocations.
3. The user creates and describes a new material. The material-creation function returns a reference for the AI system to subsequently use to refer to that material: `object_648a30dd_6290_4c2c_918f_6f69e4ac6e7d`.
4. The user wants to put that material on that object. The AI system utilizes both object references, invoking a function: `apply_material_to_object(object = object_22841ede_6839_4480_a324_23efa147e4f4, material = object_648a30dd_6290_4c2c_918f_6f69e4ac6e7d)`.

Functions could provide multiple return values or otherwise provide useful JSON structures utilizing well-known schemas. These complex return values could include both object references and action references. Reasons for returning action references include enabling users to easily undo, redo, rollback, and commit actions, including in transaction scopes.

Useful functions for a software application to provide to AI systems, for these scenarios, include:

1. `list_all` would list all of the object references that a software application is providing to an interoperating AI system.
2. `list_some` would filter those object references using a provided predicate, e.g., to list those objects of a type.
3. `addref` would increment the reference count of an object reference. Alternatively, AI systems could be provided weak references, references to a cache-based system, or utilize other interprocess object-reference passing techniques.
4. `release` would release an object reference, decrementing its reference count. Alternatively, AI systems could be provided weak references, references to a cache-based system, or utilize other interprocess object-reference passing techniques.
5. `typeof` would return a list of known types, interfaces, and categories for a referenced object.
6. `describe` would provide a natural-language description of a referenced object to an interoperating AI system.
7. `inspect` would select and/or highlight a referenced object in a visual workspace and provide an AI system with one or more screenshots of it (e.g., front, side, top, and custom).

Brainstorming on API topics, prompts to large language models could come to include both described objects and functions. Described objects could be used as arguments to AI-invoked functions. Described functions could include typing information for their parameters, and could also describe their other preconditions and effects.

Advanced topics include enabling users to interchangeably and seamlessly utilize both traditional graphical-user-interface and new conversational input techniques. That is, were a user to create a 3D object manually (utilizing the traditional user interface), the interoperating AI system would, if connected, be apprised of these occurrences, receiving a natural-language "narration" of the events as well as the relevant object references.

That is, software applications could "narrate" those user activities involving traditional user-interface components to AI assistants while also providing them with object and action references and this would create the illusion that AI systems were aware of user activities and occurrences in application workspaces. Under the hood, this functionality could be provided by means of eventing systems in software applications which enable event listeners to subscribe to those events raised as users utilized traditional user-interface components.

Data privacy concerns can be alleviated by allowing users to be able to easily connect and disconnect AI systems from their software applications as desired.
