# Foundation 2024

This project intends to enable the development of educational technologies, e.g., [adaptive](https://en.wikipedia.org/wiki/Adaptive_learning) instructional systems and [intelligent tutoring systems](https://en.wikipedia.org/wiki/Intelligent_tutoring_system), utilizing C++ and Python.

This project will explore uses of [large language models](https://en.wikipedia.org/wiki/Large_language_model) (LLMs), [large multimodal models](https://en.wikipedia.org/wiki/Large_language_model#Multimodality) (LMMs), and [multiagent systems](https://en.wikipedia.org/wiki/Multiagent_system) (e.g., [AutoGen](https://github.com/microsoft/autogen)) for designing and developing intelligent tutoring system architectures.

In addition to item-based intelligent-tutoring scenarios, e.g., scenarios involving mathematics exercises, this project intends to enable new project-based educational scenarios involving IDEs, image-editing, and CAD/CAE software.

## Selected Research Topics

This project will explore:
1. [embedding Python interpreters](https://docs.python.org/3/c-api/) to enable the development of modern features such as application task automation via (AI-generated) Python source code (see also: [Copilot in Excel video](https://www.youtube.com/watch?v=vGI6VLr8L5w)).
2. techniques for providing contextual, stateful, and otherwise dynamic subsets of available functions to LLMs and related multiagent systems.
3. multimodal interoperability with LLMs, LMMs, and related multiagent systems as pertinent to the advancement of image-editing and CAD/CAE software applications.
4. models for educational event streaming beyond [xAPI](https://xapi.com/) and [Caliper v1.2](https://www.imsglobal.org/activity/caliper). Ideas, in these regards, include providing the capability to send attached multimedia data, e.g., text, images, video, and 3D models.
5. models for educational items, exercises, activities, projects, and tasks. Educational tasks can, for example, contain subtasks which can be performed either in sequence or in parallel, e.g., working on parts which are to be combined into resultant assemblies using CAD/CAE software.
6. providing a client-side background process, a [service](https://en.wikipedia.org/wiki/Windows_service), to encapsulate the details of configurably authenticating to, connecting to, and streaming educational data to remote cloud-based systems, e.g., [learning record stores](https://en.wikipedia.org/wiki/Learning_Record_Store), operated by learners' schools. This background process will provide (e.g., COM+) components to educational software applications such as Web browsers, digital textbooks, IDEs, image-editing, and CAD/CAE software.

## Requirements

This project utilizes the Visual Studio 2022 IDE. To build, you will also need Python (>= 3.11) installed and to configure the relevant projects in the solution to reference your installation's include and libraries directories.
