# Architecture of Sidekick Model 1

Sidekick Model 1 is designed to be inexpensive, easy to understand, and easy to build. It incorporates a motorized element. It's a great way to get your first experience with EPICS.

![Model 1 Architecture Diagram](https://github.com/user-attachments/assets/51731de8-b3de-48f3-980d-987cfd2d19bf)

![Model 1 Annotated Photo](https://github.com/user-attachments/assets/33b43172-3fe0-41c9-9630-338e26a16ea6)

## Elements of the Sidekick Model 1
The Sidekick Model 1 demo consists of:

* Light source (six LEDs)
* Optical detector (a phototransistor)
* Shutter (a servo motor which swings an object to block light)
* Several Raspberry Pi computers
* Several Arduino microcontrollers
* Laptops
* A wired local area network

All components work together thanks to EPICS, which runs on all the computers in the system. The workload of control, acquisition, analysis, and visualization is distributed.

## Interaction Between Components

[![](https://mermaid.ink/img/pako:eNqVVU2PmzAU_CuWc00OgUvFVpXagCBS1KAl2wvswTWmoAJGxnQbbfa_95mPQICkSQ6RM_NmsMePl3dMeciwgaOUv9GYCIkOZpAj-NCUlKXJIkR5VqAoSVNjwai-LKXgv5mx0PVuvXpLQhkbWvH3aSQlIqxa6fpBacJppxSPKQWvJBOtOBKfHhKnpJC8O24UafeIy-rnL0GKGJnWj51lIt9kfxLKDAQ_ytemhuXhtNhzXvpiL64k7PtWvWv35W6VlgzZLGeCSH5b5uwHuphLuHLJ6C2V5W433hr5G7h7laaBWJHQct0K1Ge737i27_FIwur-_dTO2sRZu3SG5HrrQYwtDcH19P-Cq5-oT56oj87i7AeHuSuk3VdXRZQmLJdo1zTOYhiRKlj77lHGPDdQcayfe8tOm9hpIzvtAbvvyFdfz_X7MKxrlm23fl6tvpxevG-nNvczqbrzggTgTEIrXnCu3VPQbpecs2_Itqtq0jo4J7XHAaNdZfQ5po5_Hp91anat8MPz1j6157_KnXc9w9VJDCZHl6Wad08jXMU4h4PnLAzpTfDmZtRMHMPKfQYG8zkUvMdweydqyE9x7QquT3HVac3kHcFwSc1QHeNaj-MlzpjISBLCX9G7qguwjFnGAmzAMmQRqVIZ4CD_gNKqCIlkVpjAy4mNiMDgWWJSSe4dc4oNKSrWFZkJgbcha6s-_gFeJSL8)](https://mermaid.live/edit#pako:eNqVVU2PmzAU_CuWc00OgUvFVpXagCBS1KAl2wvswTWmoAJGxnQbbfa_95mPQICkSQ6RM_NmsMePl3dMeciwgaOUv9GYCIkOZpAj-DCUlKXJIkR5VqAoSVNjwai-LKXgv5mx0PVuvXpLQhkbWvH3aSQlIqxa6fpBacJppxSPKQWvJBOtOBKfHhKnpJC8O24UafeIy-rnL0GKGJnWj51lIt9kfxLKDAQ_ytemhuXhtNhzXvpiL64k7PtWvWv35W6VlgzZLGeCSH5b5uwHuphLuHLJ6C2V5W433hr5G7h7laaBWJHQct0K1Ge737i27_FIwur-_dTO2sRZu3SG5HrrQYwtDcH19P-Cq5-oT56oj87i7AeHuSuk3VdXRZQmLJdo1zTOYhiRKlj77lHGPDdQcayfe8tOm9hpIzvtAbvvyFdfz_X7MKxrlm23fl6tvpxevG-nNvczqbrzggTgTEIrXnCu3VPQbpecs2_Itqtq0jo4J7XHAaNdZfQ5po5_Hp91anat8MPz1j6157_KnXc9w9VJDCZHl6Wad08jXMU4h4PnLAzpTfDmZtRMHMPKfQYG8zkUvMdweydqyE9x7QquT3HVac3kHcFwSc1QHeNaj-MlzpjISBLCX9G7qguwjFnGAmzAMmQRqVIZ4CD_gNKqCIlkVpjAy4mNiMDgWWJSSe4dc4oNKSrWFZkJgbcha6s-_gFeJSL8)

## Next Steps

Now that you understand the architecture of the Sidekick Model 1 system, you can access all the source components needed to build your own:

**Next tutorial:** [Source Components](../model1/model1-source-components.md) - Access Arduino firmware, IOC configuration files, CAD files, and bill of materials

This provides all the downloadable resources, GitHub repositories, and documentation needed to replicate the complete Sidekick demonstration system with your own hardware.