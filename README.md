# nix 

## Installation
```
curl https://nixos.org/nix/install | sh
```
On `error: cloning builder process: Operation not permitted` do: 
  - CentOS: add `sandbox = true` to `/etc/nix/nix.conf`
  - Debian (and possibly others): do `sysctl kernel.unprivileged_userns_clone=1` (it probably does not survive a system restart)


## Files
```
$HOME/.nix-profile/etc/profile.d/nix.sh
$HOME/.nix-defexpr/channels/nixpkgs/pkgs/top-level/
$HOME/.nix-defexpr/channels/nixpkgs/pkgs/top-level/default.nix
```

## Environment vars
```
echo $NIX_PATH
```

## Files
```
~/.config/nix/nix.conf
```

## Commands
```
nix-env --install emacs --dry-run

nix-env --list-generations

nix-store --serve # serve repo?

nix-store --gc

nix-store --query
nix-env -q # show installed packages
nix-env -qa # show all packages
nix-env -qaP # show all packages and their full names

nix-channel --update # update channel
```

## Haskell infrastructure

Show haskell packages:
```
nix-env -f "<nixpkgs>" -qaP -A haskellPackages
nix-env -qaP -A nixpkgs.haskellPackages
```

https://nixos.org/nixpkgs/manual/#users-guide-to-the-haskell-infrastructure


https://alpmestan.com/posts/2017-09-06-quick-haskell-hacking-with-nix.html
```
$ nix-shell -p "haskell.packages.ghc821.ghcWithPackages (pkgs: [pkgs.aeson pkgs.dlist])"
```

https://nixos.org/nix/manual/#ssec-builtins

## Pills
https://nixos.org/nixos/nix-pills/enter-environment.html


```
List real paths
nix-env -q --out-path

Runtime dependencies:
nix-store -q --references `which nix-repl`

nix-store -q --referrers `which nix-repl`

Closure inspection:
nix-store -qR `which nix-repl`

See curated package sets:
builtins.attrNames pkgs.haskell.packages
```
