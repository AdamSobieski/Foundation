# Foundation 2024

This project intends to enable the development of educational technologies, e.g., [adaptive](https://en.wikipedia.org/wiki/Adaptive_learning) instructional systems and [intelligent tutoring systems](https://en.wikipedia.org/wiki/Intelligent_tutoring_system), utilizing C++ and Python.

In addition to item-based educational scenarios, e.g., scenarios involving mathematics exercises, this project intends to enable new project-based educational scenarios involving IDEs, image-editing, 3D graphics, and CAD/CAE software.

## Bibliography

* Cardona, Miguel A., Roberto J. Rodríguez, and Kristina Ishmael. "Artificial Intelligence and the Future of Teaching and Learning: Insights and Recommendations." (2023). [[PDF](https://tech.ed.gov/files/2023/05/ai-future-of-teaching-and-learning-report.pdf)]

  > AI models are historically better at closed tasks like solving a math problem or logical tasks like playing a game. In terms of life-wide and lifelong opportunities, we value learning how to succeed at open-ended and creative tasks that require extended engagement from the learner, and these are often not purely mathematical or logical. We want students to learn to invent and create innovative approaches. We want AI models that enable progress on open, creative tasks.

## Research Topics

This project will explore:

* uses of [large language models](https://en.wikipedia.org/wiki/Large_language_model) (LLMs), [large multimodal models](https://en.wikipedia.org/wiki/Large_language_model#Multimodality) (LMMs), and [multiagent systems](https://en.wikipedia.org/wiki/Multiagent_system) (e.g., [AutoGen](https://github.com/microsoft/autogen)) to advance the design and development of educational-technology architectures.
* [embedding Python interpreters](https://docs.python.org/3/c-api/) to enable the design and development of systems which provide task automation and content creation via AI-generated source code (see also: [Copilot in Excel](https://www.youtube.com/watch?v=vGI6VLr8L5w)).
  * providing a permissions system.
  * providing undo and redo capabilities.
  * providing multimodal feedback to AI systems (e.g., images, videos, or 3D models) as and after they execute source-code incrementally.
* providing contextual, stateful, and dynamic subsets of software applications' functions to interoperating AI systems.
  * providing tools for the development of parallel state machines.
* approaches for bidirectionally sharing multimedia data between software applications and interoperating AI systems (e.g., text, images, video, and 3D models).
* models of educational items, exercises, activities, projects, and tasks.
 * assisting learners during educational, creative project-based learning.
* models of natural-language, machine-utilizable [design specifications](https://en.wikipedia.org/wiki/Design_specification).
  * enhancing AI systems' capabilities to answer questions and to provide assistance with respect to users' design-related tasks and subtasks.
* models of complex contexts which include multiple discussions, or threads, between users and AI systems.
* models of educational event streaming beyond [XES](https://xes-standard.org/), [OCEL](https://www.ocel-standard.org/), [xAPI](https://xapi.com/), and [Caliper](https://www.imsglobal.org/activity/caliper).
  * providing the capability for attaching multimedia data (e.g., text, images, video, and 3D models).
  * uses of event-stream data from the performance of open, creative tasks in providing context to AI systems.
* developing a client-side background process, or [service](https://en.wikipedia.org/wiki/Windows_service), to encapsulate the details of configurably authenticating to, connecting to, and streaming data to remote cloud-based systems, e.g., [learning record stores](https://en.wikipedia.org/wiki/Learning_Record_Store), operated by learners' schools. This background process will provide (e.g., COM+) components to other educational software such as Web browsers, digital textbooks, IDEs, image-editing, 3D graphics, and CAD/CAE software.

## Build Requirements

This project utilizes [Visual Studio 2022](https://visualstudio.microsoft.com/downloads/). To build this project, you will also need [Python](https://www.python.org/downloads/) installed and to configure the relevant projects in the solution to reference your installation's include and libraries directories.

## Notes

* [Document Object Model Ideas](/Notes/Document%20Object%20Model%20Ideas.md)
* [Graph-based Selectors](/Notes/Graph-based%20Selectors.md)
* [Objects and Iteration with Style](/Notes/Objects%20and%20Iteration%20with%20Style.md)
* [Selecting Events with Style](/Notes/Selecting%20Events%20with%20Style.md)
* [State Machines](/Notes/State%20Machines.md)
