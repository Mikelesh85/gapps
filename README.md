# Gapps
###  💰 Please [consider supporting the project](https://www.buymeacoffee.com/bmarsh/membership)


:snowflake: View the [Gapps site](https://web-gapps.pages.dev/)  

### Table of Contents
1. [About](#about)
2. [Getting Started](#getting-started)
3. [Supported Frameworks](#supported-frameworks)
4. [Roadmap](#roadmap)
5. [Things to know](#things-to-know)
6. [FAQ](#faq)

- Interested in some form of partnership or new license? Contact me on [discord](https://discord.gg/9unhWAqadg)
- Stay up to date on changes: https://forms.gle/EXigxbcWTSXcPnjw7  
- Discord: https://discord.gg/9unhWAqadg

### New Features :snowflake:
- SOC2, NIST CSF, NIST-800-53, CMMC, HIPAA, ASVS, ISO27001, CSC CIS18, PCI DSS and SSF have been added! That makes 10 total frameworks
- Total revamp of the UI
- Multi-tenancy is now supported!
- Collaboration with auditors  
- Vendor Questionnaires

### Next big features :snowflake:  
- Control automation?
- Endpoint agents for compliance?
- More frameworks?
- [Take a look at the current roadmap](https://github.com/users/bmarsh9/projects/1) or [submit a issue](https://github.com/bmarsh9/gapps/issues)

### About
Gapps is an Security compliance platform that makes it easy to track your progress against various security frameworks. *Gapps is currently in Alpha mode - while it works great, there may be some breaking changes as it evolves. Please do not use this in production.... yet!*.  
- Supports 10 security compliance frameworks (more coming)  
- 1500+ controls and 25+ policies out of the box for the frameworks (majority of policies are sourced from [strongdm/comply](https://github.com/strongdm/comply))
- Track the status of each control
- Add custom controls/policies
- WYSIWYG content editor  
- Vendor questionnaires

#### Captures from the platform

Control Dashboard          |
:-------------------------:|
![](img/gapps_2.PNG)  |


Project Overview          |
:-------------------------:|
![](img/gapps_1.PNG)  |

Track Progress of Controls          |
:-------------------------:|
![](img/gapps_3.PNG)  |

### Getting Started

##### Setting up the server with Docker in 2 minutes

The following instructions are to get you started very quickly. The image will be pulled from Docker Hub

```
$ git clone https://github.com/bmarsh9/gapps.git; cd gapps
$ docker-compose up -d
```

The server should be running on `http://<your-ip>:5000`  
The default email/password is `admin@example.com:admin`

Next, create a Tenant and a Project with you desired framework (e.g. SOC2). Based on the selected criteria, controls and policies will be automatically added to your project. Start exploring your project!

##### Email  

You can setup email (for sending user invites) as well by setting the following environment variables (docker-compose file or elsewhere)  

```
MAIL_USERNAME="email@gmail.com"
```

### Supported frameworks
+ SOC2
+ CMMC
+ ASVS
+ ISO27001
+ HIPAA
+ NIST CSF
+ NIST 800-53
+ CSC CIS 18
+ PCI DSS
+ SSF (custom framework "Startup Security Framework")

### Roadmap

[Take a look at the project](https://github.com/users/bmarsh9/projects/1)


### Things to know
- The mitigation details of the controls are not documented. So it won't tell you how to mitigate a specific control. This requires a ton of work to complete but there is a ticket
- Difficulty to Implement (dtc) is a field attached to the controls and every single control is labeled as "Easy" (that doesn't actually mean it is easy). This also requires a ton of work to update.


### FAQ

##### If you get a database connection error trying to start Gapps, you need to update (or remove) your env variables
```
[INFO] Checking if we can connect to the database server: postgresql://db1:db1@localhost/db1
[ERROR] could not connect to server: Connection refused
        Is the server running on host "localhost" (127.0.0.1) and accepting
        TCP/IP connections on port 5432?
could not connect to server: Cannot assign requested address
        Is the server running on host "localhost" (::1) and accepting
        TCP/IP connections on port 5432?
```

Can usually be fixed by unsetting two variables if running within docker. If you want to use a external database, see the next FAQ
```
unset SQLALCHEMY_DATABASE_URI
unset POSTGRES_HOST
```

##### Running with Docker Desktop
1. Download the [docker-compose.yml](https://github.com/bmarsh9/gapps/blob/main/docker-compose.yml) file
2. Open up a elevated command prompt and change directories (cd) to where the docker-compose.yml file was downloaded (likely Downloads)
3. Run `docker compose up`

##### View env variables for debugging
```
docker exec gapps env
```

##### Create database migration script
```
docker exec gapps alembic revision --autogenerate -m 'Migration message.'
```
##### Upgrade database to the latest state
docker exec gapps alembic upgrade head
```

##### Upgrading versions
1.) Edit `docker-compose.yml` file with the desired version from [Docker Hub](https://hub.docker.com/r/bmarsh13/gapps/tags). Anywhere you see the old version in the compose file (should be 4 instances), update it with the desired version. (e.g. bmarsh13/gapps:3.3.9 -> bmarsh13/gapps:3.4.0)  
2.) `docker-compose up -d`  
3.) [Perform database migration](https://github.com/bmarsh9/gapps#perform-database-migration) if neccesary 

##### JSON format for programmically adding controls

The format consists of controls and subcontrols. The snippet below shows an example of a control having one (1) subcontrol however you can add as many as you like. It is not a requirement to have subcontrols for a control (you can have zero). However it may make sense if you want to break down a control into specific actions that are trackable. Let's take the CIS 18 framework as an example. You could place all 18 "domains" as controls and the controls within each domain would be a subcontrol within Gapps.

```
[
    {
        "name": "Limit information system access to authorized users, processes acting on behalf of authorized users or",       
        "description": "Maintain list of authorized users defining their identity and associated role and sync with sys",       
        "guidance": "List approved users, services, and devices, and have logical controls in place to prevent unauthor",
        "ref_code": "AC.L1-3.1.1",
        "system_level": false,
        "subcategory": "Identity & Access Management (IAM)",
        "category": "Access Control",
        "dti": "easy",
        "dtc": "easy",
        "meta": {},
        "subcontrols": [
            {
                "ref_code": "3.1.1.a",
                "name": "Authorized users are identified.",
                "description": "Authorized users are identified.",
                "meta": {}
            }
        ]
    }
}
```

##### Building and pushing
```
docker build -t gapps:3.4.3 .
docker tag gapps:3.4.3 bmarsh13/gapps:3.4.3
docker push bmarsh13/gapps:3.4.3
```
