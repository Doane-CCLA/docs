# Customizing Your Environment in HPC

The HPC environment may be customized to suit your needs.

<!-- TODO add link to Linux section when it gets published -->

 ## Project-Specific Environment Variables

Some projects have environment modules that will prepare the environment with the specific needs of the project. To list the available project modules, type `module avail`. At the top of the output is a section titled `/software/tools/modules`. The environment modules begin with `env/`. To load one of these environments:

```bash
module load env/cades-bsd
```

<!-- TODO are these still functional? -->
