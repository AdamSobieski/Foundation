# Foundation 2024

This project intends to enable the development of educational technologies, e.g., [adaptive](https://en.wikipedia.org/wiki/Adaptive_learning) instructional systems and [intelligent tutoring systems](https://en.wikipedia.org/wiki/Intelligent_tutoring_system), utilizing C++ and Python.

In addition to item-based educational scenarios, e.g., scenarios involving mathematics exercises, this project intends to enable new project-based educational scenarios involving IDEs, image-editing, 3D graphics, and CAD/CAE software.

## Bibliography

* Cardona, Miguel A., Roberto J. Rodríguez, and Kristina Ishmael. "Artificial Intelligence and the Future of Teaching and Learning: Insights and Recommendations." (2023). [[PDF](https://tech.ed.gov/files/2023/05/ai-future-of-teaching-and-learning-report.pdf)]

  > AI models are historically better at closed tasks like solving a math problem or logical tasks like playing a game. In terms of life-wide and lifelong opportunities, we value learning how to succeed at open-ended and creative tasks that require extended engagement from the learner, and these are often not purely mathematical or logical. We want students to learn to invent and create innovative approaches. We want AI models that enable progress on open, creative tasks.

## Research Topics

This project will explore:

* uses of [large language models](https://en.wikipedia.org/wiki/Large_language_model) (LLMs), [large multimodal models](https://en.wikipedia.org/wiki/Large_language_model#Multimodality) (LMMs), and [multiagent systems](https://en.wikipedia.org/wiki/Multiagent_system) (e.g., [AutoGen](https://github.com/microsoft/autogen)) to advance the design and development of educational technology architectures.
* [embedding a Python interpreter](https://docs.python.org/3/c-api/) to enable the design and development of modern features such as application task automation via human-generated and AI-generated source code (see also: [Copilot in Excel video](https://www.youtube.com/watch?v=vGI6VLr8L5w)).
  * providing a user permissions system.
  * providing undo and redo capabilities.
* techniques for providing contextual, stateful, and otherwise dynamic subsets of available functions from software applications to inteoperating AI systems.
  * providing tools for developing parallel state machines.
* approaches for bidirectionally sharing multimedia data (e.g., text, images, video, and 3D models) between software applications and interoperating AI systems.
* models of educational items, exercises, activities, projects, and tasks.
* models of natural-language, machine-utilizable [design specifications](https://en.wikipedia.org/wiki/Design_specification). These will be useful for enhancing AI systems' capabilities to answer questions and provide assistance with respect to users' design-related tasks and subtasks.
* models of complex contexts which include multiple discussions, or threads, between users and AI systems.
* models of educational event streaming beyond [XES](https://xes-standard.org/), [OCEL](https://www.ocel-standard.org/), [xAPI](https://xapi.com/), and [Caliper](https://www.imsglobal.org/activity/caliper). Ideas, in these regards, include providing the capability for attaching multimedia data (e.g., text, images, video, and 3D models).
* providing a client-side background process, or [service](https://en.wikipedia.org/wiki/Windows_service), to encapsulate the details of configurably authenticating to, connecting to, and streaming data to remote cloud-based systems, e.g., [learning record stores](https://en.wikipedia.org/wiki/Learning_Record_Store), operated by learners' schools. This background process will provide (e.g., COM+) components to educational software such as Web browsers, digital textbooks, IDEs, image-editing, 3D graphics, and CAD/CAE software.

While combinations of AI systems, source-code generation, and IDEs, image-editing, 3D graphics, and CAD/CAE software have been and continue to be explored elsewhere (see: [GPT x Blender projects](https://github.com/search?q=gpt+blender&type=repositories)), this project will explore:

* uses of event-stream data from the performance of open, creative tasks for providing context data to AI systems.
* the capabilities and performance of multimodal AI systems, e.g., GPT-4V, as they receive multimedia data (e.g., images, videos, or 3D models) from applications while and after they generate and execute Python commands incrementally.
* AI systems which can assist learners during educational, creative project-based learning, e.g., answering learners' questions while observing them perform design tasks.

## Build Requirements

This project utilizes [Visual Studio 2022](https://visualstudio.microsoft.com/downloads/). To build this project, you will also need [Python](https://www.python.org/downloads/) installed and to configure the relevant projects in the solution to reference your installation's include and libraries directories.

## Notes

* [Document Object Model Ideas](/Notes/Document%20Object%20Model%20Ideas.md)
* [Graph-based Selectors](/Notes/Graph-based%20Selectors.md)
* [Objects and Iteration with Style](/Notes/Objects%20and%20Iteration%20with%20Style.md)
* [State Machines](/Notes/State%20Machines.md)
