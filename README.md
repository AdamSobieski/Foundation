# Foundation 2024

This project intends to enable the development of educational technologies, e.g., adaptive instructional systems and intelligent tutoring systems, utilizing C++ and Python.

This project will explore uses of large language models (LLMs), large multimodal models (LMMs), and multiagent system architectures (e.g., [AutoGen](https://github.com/microsoft/autogen)) for designing and developing intelligent tutoring systems.

In addition to item-based intelligent-tutoring scenarios, e.g., the selection and presentation of interactive mathematics exercises, this project intends to enable new project-based scenarios, e.g., enabling interoperation with modern IDEs, photo-editing software, and CAD/CAE software.

Towards enabling these educational scenarios, this project will include a client-side service which will encapsulate the details of streaming educational data, e.g., event stream data, to remote cloud services operated by learners' schools. The described service will provide components, i.e., COM+ components, to client-side software applications.

## Selected Research Topics

This project will explore:
1. [embedding Python interpreters](https://docs.python.org/3/c-api/) to convenience the development of contemporary features such as application task automation via (AI-generated) Python source code (see also: [Copilot in Excel video](https://www.youtube.com/watch?v=vGI6VLr8L5w)).
2. techniques for providing contextual, stateful, and otherwise dynamic sets of available functions to LLMs and related multiagent systems.
3. multimodal interoperability with LMMs and multiagent systems as pertinent to enhancing photo-editing and CAD/CAE software applications with AI.
4. new models for educational event streaming, e.g., models beyond [xAPI](https://xapi.com/) and [Caliper v1.2](https://www.imsglobal.org/activity/caliper). Ideas, in these regards, include providing the capability to send attached multimedia data, e.g., text, images, video, and 3D models.
5. new models for educational items, exercises, activities, projects, and tasks. Educational tasks can, for example, contain subtasks which could be performed either in sequence or in parallel, e.g., working on parts that are to be combined into resultant assemblies in a CAD/CAE application.

## Requirements

This project utilizes the Visual Studio 2022 IDE. To build, you will also need Python (>= 3.11) installed and to configure the relevant projects in the solution to reference your installation's include and libraries directories.
