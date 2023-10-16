# Foundation 2024

This project intends to enable the development of educational technologies, e.g., [adaptive](https://en.wikipedia.org/wiki/Adaptive_learning) instructional systems and [intelligent tutoring systems](https://en.wikipedia.org/wiki/Intelligent_tutoring_system), utilizing C++ and Python.

In addition to item-based educational scenarios, e.g., scenarios involving mathematics exercises, this project intends to enable new project-based educational scenarios involving IDEs, image-editing, and CAD/CAE software.

## Selected Research Topics

This project will explore:

* uses of [large language models](https://en.wikipedia.org/wiki/Large_language_model) (LLMs), [large multimodal models](https://en.wikipedia.org/wiki/Large_language_model#Multimodality) (LMMs), and [multiagent systems](https://en.wikipedia.org/wiki/Multiagent_system) (e.g., [AutoGen](https://github.com/microsoft/autogen)) to advance the design and development of educational technology architectures.
* [embedding Python interpreters](https://docs.python.org/3/c-api/) to enable modern features such as application task automation via human-generated and AI-generated Python source code (see also: [Copilot in Excel video](https://www.youtube.com/watch?v=vGI6VLr8L5w)).
* techniques for providing contextual, stateful, and otherwise dynamic subsets of available functions to LLMs, LMMs, and related multiagent systems.
* approaches for bidirectionally sharing multimedia data (e.g., text, images, video, and 3D models) between software applications and interoperating LLMs, LMMs, and related multiagent systems.
* models for educational items, exercises, activities, projects, and tasks. Educational tasks can, for example, contain subtasks to be performed either in sequence or in parallel, e.g., working on parts which are to be combined into resultant assemblies using CAD/CAE software.
* models for educational event streaming beyond [XES](https://xes-standard.org/), [xAPI](https://xapi.com/), and [Caliper v1.2](https://www.imsglobal.org/activity/caliper). Ideas, in these regards, include providing the capability to attach multimedia data (e.g., text, images, video, and 3D models).
* providing a client-side background process, or [service](https://en.wikipedia.org/wiki/Windows_service), to encapsulate the details of configurably authenticating to, connecting to, and streaming data to remote cloud-based systems, e.g., [learning record stores](https://en.wikipedia.org/wiki/Learning_Record_Store), operated by learners' schools. This background process will provide (e.g., COM+) components to educational software applications such as Web browsers, digital textbooks, IDEs, image-editing, and CAD/CAE software.

While combinations of LLMs, Python source code generation, and CAD/CAE software have been and continue to be explored (see: [GPT x Blender projects](https://github.com/search?q=gpt+blender&type=repositories)), this project will explore:

* uses of event streams from software applications for interoperability with AI systems including LLMs.
* the performance of LMMs, e.g., GPT-4V, which will additionally receive multimedia data from CAD/CAE applications (e.g., images, videos, or 3D models) while or after executing Python commands incrementally.
* systems which can assist learners during educational creative projects, e.g., answering a question while observing a learner designing a gear.

## Selected Resources and Materials

* Cardona, Miguel A., Roberto J. Rodríguez, and Kristina Ishmael. "Artificial Intelligence and the Future of Teaching and Learning: Insights and Recommendations." (2023). [[PDF](https://tech.ed.gov/files/2023/05/ai-future-of-teaching-and-learning-report.pdf)]

  > AI models are historically better at closed tasks like solving a math problem or logical tasks like playing a game. In terms of life-wide and lifelong opportunities, we value learning how to succeed at open-ended and creative tasks that require extended engagement from the learner, and these are often not purely mathematical or logical. We want students to learn to invent and create innovative approaches. We want AI models that enable progress on open, creative tasks.

## Build Requirements

This project utilizes [Visual Studio 2022](https://visualstudio.microsoft.com/downloads/). To build, you will also need [Python](https://www.python.org/downloads/) (>= 3.11) installed and to configure the relevant projects in the solution to reference your installation's include and libraries directories.
