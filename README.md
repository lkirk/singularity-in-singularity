# Singularity in singularity

This is a proof-of-concept to show that it is indeed possible to run nested singularity processes.
My purpose for doing this is to create containers that can run applications that are in other other containers, allowing me to decompose the containers into small, purpose-built units.

To test this for yourself, you can do the following:

```console
sudo singularity build container.sif Singularity
singularity shell container.sif

# then, go ahead and try running
singularity shell container.sif
# as many times as you want!
```

Here is an example session where I nest 3 containers:
```
user@host$ singularity shell container.sif
Singularity> singularity shell container.sif
INFO:    Converting SIF file to temporary sandbox...
Singularity> singularity shell container.sif
INFO:    Converting SIF file to temporary sandbox...
```

And the resulting process tree (reported by htop):
```
Singularity runtime parent
├─ /bin/bash --norc
│  └─ Singularity runtime parent
│     ├─ /bin/bash --norc
│     │  └─ Singularity runtime parent
│     │     ├─ /bin/bash --norc
│     │     ├─ Singularity runtime parent
│     │     ├─ Singularity runtime parent
│     │     ├─ Singularity runtime parent
│     │     ├─ Singularity runtime parent
│     │     └─ Singularity runtime parent
│     ├─ Singularity runtime parent
│     ├─ Singularity runtime parent
│     ├─ Singularity runtime parent
│     ├─ Singularity runtime parent
│     └─ Singularity runtime parent
├─ Singularity runtime parent
├─ Singularity runtime parent
├─ Singularity runtime parent
├─ Singularity runtime parent
├─ Singularity runtime parent
├─ Singularity runtime parent
└─ Singularity runtime parent
```

If you do not want to coerce conversion to a temporary sandbox on every call (it can be time intensive for large images), you can simply create the sandbox upfront:
```
user@host$ singularity build --sandbox test container.sif
WARNING: 'nodev' mount option set on /tmp, it could be a source of failure during build process
INFO:    Starting build...
INFO:    Verifying bootstrap image container.sif
INFO:    Creating sandbox directory...
INFO:    Build complete: test
user@host$ singularity shell container.sif
Singularity> singularity shell test
```
