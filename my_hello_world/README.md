# README

## Prerequisite

```bash
# Multi-user installation
sh <(curl -L https://nixos.org/nix/install) --daemon

# Single-user installation
sh <(curl -L https://nixos.org/nix/install) --no-daemon
```

### Install flakes (optional)

Edit `/etc/nix/nix.conf` if you installed Nix as `Multi-user` or
create and edit `~/.config/nix/nix.conf` if you installed Nix as `Single-user`

and add:

```bash
experimental-features = nix-command flakes
```

## How to enter to nix-shell

```bash
nix-shell
# or
nix-shell default.nix
```
## How to build and run this project

```bash
$ nix-shell
$ alr build
Welcome to the toolchain selection assistant

In this assistant you can set up the default toolchain to be used with any crate
that does not specify its own top-level dependency on a version of gnat or
gprbuild.

If you choose "None", Alire will use whatever version is found in the
environment.

ⓘ gnat is currently not configured. (alr will use the version found in the environment.)

Please select the gnat version for use with this configuration
  1. gnat_native=13.2.1
  2. None
  3. gnat_external=12.3.0 [Detected at (...)yhmxgzjycap5mvzjfnm49raacz-gnat-wrapper-12.3.0/bin/gnat] <<- SELECT THIS
  4. gnat_arm_elf=13.2.1
  5. gnat_avr_elf=13.2.1
  6. gnat_riscv64_elf=13.2.1
  7. gnat_arm_elf=13.1.0
  8. gnat_avr_elf=13.1.0
  9. gnat_native=13.1.0
  0. gnat_riscv64_elf=13.1.0
  a. (See more choices...)
Enter your choice index (first is default):
> 3
ⓘ Selected tool version gnat_external=12.3.0

ⓘ Choices for the following tool are narrowed down to releases compatible with just selected gnat_external=12.3.0

ⓘ gprbuild is currently not configured. (alr will use the version found in the environment.)

Please select the gprbuild version for use with this configuration
  1. gprbuild=18.0.0 [Detected at (...)fs7rr33gdpj1lzjwfzhd75jcvd-gprbuild-24.0.0/bin/gprbuild] <<- SELECT THIS
  2. None
Enter your choice index (first is default):
> 1
$ alr run
```


## How to use `direnv`

Create `.envrc` file for `direnv`

```bash
cd <some-project-name>
touch .envrc
```

Edit `.envrc` like this.
This shell script prevents infinitely recursive execution of commands.

```bash
if [[ -z "$IS_IN_NIX_SHELL" ]] ; then
   export IS_IN_NIX_SHELL=1
   # add some command to execute here
   # ex) cargo watch -x check -x test
fi
```
