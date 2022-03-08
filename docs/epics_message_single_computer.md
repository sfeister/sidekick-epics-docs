---
layout: default
title: First Steps in pvaPy
authors:
    - Scott Feister
---

# First Steps in pvaPy

Send an EPICS message within a single computer. This tutorial should work for Windows, Mac, or Linux.

## References:
1. [pvaPy on GitHub](https://github.com/epics-base/pvaPy)
1. [pvaPy Official Documentation](https://epics.anl.gov/extensions/pvaPy/production/index.html)
1. [Miniconda Documentation](https://docs.conda.io/en/latest/miniconda.html)

## Steps:
1. Pick a single computer that you will run this test on.

1. Install the "pvapy" Python module on this computer.

    1. Follow installation instructions (pip or conda depending on the OS) per the [pvaPy GitHub README](https://github.com/epics-base/pvaPy)

    2. On Windows and Linux, can be simple as `pip3 install pvapy`

    3. If you haven't already, this step may require also installing Python, miniconda, etc.

3. Clone the "pvapy" github repository into a folder on this computer, for access to the examples.

```bash
git clone https://github.com/epics-base/pvaPy.git
```

4. Navigate into the examples folder in pvapy repository you just downloaded.

5. Open up a separate terminal window. Navigate into the examples folder from that terminal window as well.

6. Your screen may now look something like this, with two terminal windows open side-by-side and both in the same "examples" folder.

![](https://i.imgur.com/dxZ3cgr.png)

7. In the left window, type `python server.py` and hit enter.

8. In the right window, type `python client.py` and hit enter.

9. Your screen should be filling up with something like this:

![](https://i.imgur.com/dvOTawV.png)

10. Congrats! It's working. You're successfully sending EPICS PVAccess messages from your server python script to your client python script.
