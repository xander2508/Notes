`Event Tracing For Windows (ETW)` is a general-purpose, high-speed tracing facility provided by the operating system. Using a buffering and logging mechanism implemented in the kernel, ETW provides a tracing mechanism for events raised by both user-mode applications and kernel-mode device drivers.

![[etw.webp]]

* `Controllers`: The Controllers component, as its name implies, assumes control over all aspects related to ETW operations. It encompasses functionalities such as initiating and terminating trace sessions, as well as enabling or disabling providers within a particular trace.

At the core of ETW's architecture is the publish-subscribe model. This model involves two primary components: