---
layout: post
title: "Vensim and EMA Workbench"
date: 2019-06-27
description: Tips and tricks for the intermediate to advanced Vensim user. Covers connecting quantitative models to the exploratory modeling analysis (EMA workbench) tool # Add post description (optional)
img: SD.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Modeling, EMA]

---

## Vensim and EMA Workbench: Advanced Windows Setup
This post contains setup help for the intermediate to advanced Vensim user. The following information is for users that are interested in connecting their Vensim model to the python library known as the Exploratory Modeling and Analysis (EMA) workbench, but are experiencing difficulty setting up the connection. As explained in the [EMA documentation](https://emaworkbench.readthedocs.io/en/latest/installation.html), installing the workbench is straightforward (``pip install ema_workbench``). Often, difficulty occurs when users want to use Vensim (which is 32-bit) and EMA workbench in python (which is often run on 64-bit machines).

### Why does 32 vs 64 bit matter?
(Note: Written for Windows users) There are two major categories of computer processors: 32-bit and 64-bit. Older operating systems (e.g. Windows 98) all use 32-bit processors. After about the late 1990s-early 2000s, home computers had 64-bit processors. The \"-bit\" terminology just means that the computer works in data units that are either 32 or 64 bits wide. Computers with 64-bit processors can run more calculations per second and are also capable of running 32-bit versions of programs. The opposite is not true (a 32-bit operating system can\'t run a 64-bit program). Finally, 64-bit processors can come in multiple cores (for regular computers, generally 2, 4, 6, or 8 cores are possible) which allow for faster computations.

### Vensim is 32-bit
Because Vensim is a 32-bit program, you also need a 32-bit version of Python.  More than likely, however, you may have 64-bit Python installed on your machine, which is generally offers you more speed and performance. So that leaves you with two options: downgrade to 32-bit Python, or set up virtual environments so that you can have multiple versions on your system.

### How do I make virtual environments so I can use both 32 and 64 bit?
If you have a 64-bit Windows machine, but want to be able to run 32-bit programs (like Vensim) on your machine - a virtual environment is an good way to do it. You can do this with conda environment. Note that non-conda virtual environments are also possible, though I find conda easier to work with.

### What\'s the deal with Vensim DSS and DLL?
__DSS:__ The DSS version of Vensim gives you additional control over Vensim compared to the PLE version. It enables you to link to external functions or programming software through the Vensim Dynamic Link Library (DLL). By default, Vensim DSS installs DLL support files in the DLL subdirectory of Vensim (usually in ``C:\Windows\System32`` or ``C:\Windows\SysWOW64``), with the name ``vendll32.dll``. Do not rename the Vensim DLL or it will not work.

__DLL:__ A DLL is something that many programs have. The Vensim DLL is simply a separate program that allows Vensim to be called from other applications, such as Excel or ema_workbench. This allows you to extend the functionality of Vensim by making your SD model available for analysis by an outside program. You need to use a 32 bit development environment to use the 32 bit DLLs.

As a final reminder, keep in mind that the Vensim DLL only supports Windows and it can only use packaged models (``.vpm`` files, not ``.mdl`` files).

__.dll and .lib:__ When you install Vensim DSS, the Vensim DLL will be put in the same directory as the program (not in a system directory) which means you have to move it to a different directory or add the program directory to your system PATH in order to use the DLL. Example models and supporting files will be installed into a public folder or your home directory.

The ``.lib`` extension is a static version and the ``.dll`` is the dynamic version of the program. They are close but not the same thing, so if you\'re getting \'Vensim DDL not found\' errors you may need to hunt down the ``vendll32.dll`` program, since just the ``.lib`` version may not be sufficient.

## For more help...
[EMA Workbench Connectors](https://emaworkbench.readthedocs.io/en/stable/ema_documentation/connectors/vensimDLLwrapper.html)

[External Functions and the Vensim DLL](https://www.vensim.com/documentation/index.html?25845.htm)

[Vensim DLL Overview](hhttps://www.vensim.com/documentation/index.html?dss_dll.htm)
