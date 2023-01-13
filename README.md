# Gapps

### Table of Contents
1. [About](#about)
2. [Getting Started](#getting-started)
3. [Roadmap](#roadmap)

Contact me and/or stay up to date on changes: https://forms.gle/EXigxbcWTSXcPnjw7  
Discord: https://discord.gg/9unhWAqadg

### New Features :snowflake:
- CMMC framework has been added!
- Total revamp of the UI
- Multi-tenancy is now supported!

### About
Gapps is an Security compliance platform that makes it easy to track your progress against various security frameworks. Currently the only frameworks are CMMC and SOC2 - however other frameworks will soon be added such as CIS CSC, ISO and NIST CSF. *Gapps is currently in Alpha mode - while it works great, there may be some breaking changes as it evolves. Please do not use this in production.... yet!*.
- 300+ controls and 25+ policies out of the box for CMMC/SOC2 (majority of policies are sourced from [strongdm/comply](https://github.com/strongdm/comply))
- Track the status of each control
- Add custom controls/policies
- WYSIWYG content editor

#### Check out the intro video below!

https://user-images.githubusercontent.com/26391921/203190627-84abcaa8-70ba-47f1-a957-dae7129299a6.mp4

#### Captures from the platform

Home Dashboard          |
:-------------------------:|
![](img/gapps_2.PNG)  |

Project Controls          |
:-------------------------:|
![](img/3_gapps_1.PNG)  |

Track Progress          |
:-------------------------:|
![](img/3_gapps_2.PNG)  |

### Getting Started

##### Setting up the server with Docker

The following instructions are to get you started very quickly. The image will be pulled from Docker Hub

```
$ git clone https://github.com/bmarsh9/gapps.git; cd gapps
$ export SETUP_DB=yes;docker-compose up -d
```

The server should be running on `http://<your-ip>:5000`  
The default email/password is `admin@example.com:admin`

Next, create a project and select the framework (SOC2). Based on the selected criteria, controls and policies will be automatically added to your project. You can also go to the Controls and Policies page and add them to your project.

### Roadmap

[Take a look at the project](https://github.com/users/bmarsh9/projects/1)

- [ ] Add additional frameworks such as NIST CSF, ISO and CIS CSC
- [ ] Add procedures for SOC2
- [ ] Add evidence collection windows for SOC2
- [ ] Add reminders for control/evidence collection
- [ ] Add tagging support
- [ ] Improve policies and documentation
- [ ] Release endpoint agent to automate collection
