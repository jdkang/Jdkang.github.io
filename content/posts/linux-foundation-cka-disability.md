---
title: "Taking the Linux Foundation Certified Kubernetes Administrator Exam As A Disabled Person"
date: 2022-03-08T15:49:04-05:00
draft: false
---

This post is intended to document aspects of taking the Certified Kubernetes Administrator (CKA) exam as a disabled person. Specifically in my case, a visually impaired person. The hope is this will (a) make it easier for anyone in a similar situation and (b) help improve processes long-term for the disabled.

Although the CKA is a Linux Foundation exam it is proctored through [PSI](https://candidate.psiexams.com/).

To be very clear: my interactions with individuals from both the Linux Foundation and PSI were extremely positive. With their help, I was able to pass the exam with an 87.

The issues laid out here are in process and implementation within a system. Relying on individuals to make up for these gaps is not sustainable or equitable in my opinion.

These issues might not have been designed on purpose to make life difficult for the disabled, but their continued lack of remediation is a choice.

# Requesting Special Accommodations 
## The Process
As the LF [docs](https://docs.linuxfoundation.org/tc-docs/certification/lf-candidate-handbook/exam-preparation-checklist) and the attached PDF indicate, you must:

1. Pick an exam date at least 2 weeks out
2. Fill out the PDF [Special Accommodation Request Form](https://docs.linuxfoundation.org/tc-docs/certification/lf-candidate-handbook/exam-preparation-checklist#:~:text=Program%20Special%20Accommodation%20Request%20Form%20to)
    1. You will **NEED** medical verification. If you have prior documentation this seems to work OK. (I used an old doctor's note and some tax forms which indicate my condition)
3. Submit the form the PDF via [JIRA](https://jira.linuxfoundation.org/plugins/servlet/theme/portal/15/create/322)
4. After your ticket is handled, you should get a **CONFIRMATION EMAIL FROM PSI** about your accommodations.

## Issues with the Request Process
There are a few very clear points of improvement here.

1. If you are filling out a JIRA form why do you have to fill out a PDF? (PDFs are not very accessible as well)
2. There is essentially a coordination penalty for needing to request accommodations due to the order of operations that need to occur. 
    - Incorporating the accommodations sub-process into the **normal exam request workflow** would go a long way to mitigating issues.
3. It was not made clear to me either via documentation or the ticket that I would ultimately get a confirmation of accommodations from PSI.

On point (3) this actually cost me nearly 40 minutes of extra time before the exam as I worked with a very kind proctor to figure the situation out. As I never got this confirmation email nor did I know to expect one, I was quite panicked before the exam that something had gone wrong. 

# Taking the Actual Exam
In addition to _Testing Environment Requirements_ in the [Candidate Handbook](https://docs.linuxfoundation.org/tc-docs/certification/lf-candidate-handbook/candidate-requirements), some details worth noting.

1. You can have clear water in a clear glass of water
2. Your proctor will probably let you have a break albeit with the clock running. This is particularly important since 1.5 time = 3 hours of exam.
3. You will need to be able to position your camera with your face (and mouth) very clearly in view AND be able to move the camera around to inspect many aspects of your setup. I was asked to lift my laptop, move a mousepad, etc.
    - This is important if you need to sit close to the monitor like myself as traditional ways of mounting the camera on top or via a stand can be challenging to satisfy this requirement. In most work/meeting situations a larger shot frame is okay but not for the exam.
4. For the visually impaired, I was able to use the [Dark Reader](https://chrome.google.com/webstore/detail/dark-reader/eimadpbcbfnmbkopoojfekhnkhdbieeh?hl=en-US) chrome extension with the simulator to create a **high contrast** environment. I did also request this with the special accommodations form as well. (Obviously a dark mode within the actual simulator would have been more ideal.)
5. The `CTRL+l` bash shortcut works to clear the terminal. This can be useful if you have to zoom the screen in very far.

# More General Comments and Tips
This section is more general advice not necessarily only useful to the visually impaired or those with disabilities.

## Arbitrary UI Quirks and Restrictions
There are some design decisions in the PSI emulator that do not seem to make a lot of sense, especially considering the fact you are _constantly_ sharing your video, sound, and desktop.

1. Only one terminal. (Yes I realize you could technically try to use tmux)
2. The built-in notepad is cumbersome. Being able to use something like notepad++ or sublime should be a real consideration.

## Setup Your Environment
As noted in the killer.sh practice simulator, it is worth it to spend some time to setup your main environment. e.g.

`~/.vimrc`
```vimrc
set expandtab
set shiftwidth=2
set tabstop=2
set number
set ic
set incsearch
```
- `expandtab, shiftwidth=2, tabstop=2` - make dealing with YAML a lot easier especially when pasting from the k8s docs
- `ic` - case incentive searching with `/`
- `incserach` - highlights search results as you type. you can cycle through with `CTRL+g` and `CTRL+t` during a search.

`kubectl` arg helpers
```bash
export do='--dry-run=client -o=yaml'
export now='--grace-period=0 --force'
```

## Use vim Visual Mode
When pasting in fragments from the k8s docs or copying labels across multiple parts of the segment, vim's visual mode can be very helpful and much quicker than manually tabbing.

Some quick tips:
1. `shift+V` to enter visual mode. Use `j`/`k` to select lines
2. use `y` to yank (copy) thje line(s)
3. use `:>` to indent or `:<` to unindent. You can do multiple indents, e.g. `:>>` or `:<<`
3. use `@:` to repeat the last action, e.g. add another indent
4. if you are using `d` to quickly delete, using just `p` will give you a headache. if you want to **ensure** you are pasting from the _yanked buffer_ use `"0p` or `"0P`
