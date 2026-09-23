# GenAstro registry

The Julia registry for Gen Astro's source-available packages.

Epicycle's open packages are registered in Julia's General registry and need nothing from here. This
registry carries the packages released under `LicenseRef-GenAstro-SourceAvailable`, which General
does not accept.

## Using it

Add the registry once, then packages from it install the way any other package does.

```julia
using Pkg
Pkg.Registry.add(RegistrySpec(url = "https://github.com/GenAstro/Registry.git"))
Pkg.add("Epicycle")
```

General is still needed, since the packages here depend on packages there. A depot that has only
this registry will not resolve.

## Adding a version

Registration is done with [LocalRegistry.jl](https://github.com/GunnarFarneback/LocalRegistry.jl),
from an environment that has the package developed:

```julia
using LocalRegistry
register(MyPackage; registry = "GenAstro")
```

`register` reads the package's committed tree, so the version bump in `Project.toml` is committed
before registering, not after. It records the commit and pushes the registry entry; it does not
check that the dependency bounds are satisfiable, which General would have done, so the compat
entries are worth reading before a release rather than after.
