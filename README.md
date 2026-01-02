# AB Download Manager Flake

This is a Nix flake for [AB Download Manager](https://abdownloadmanager.com/), a modern, open-source download manager.

## Usage

### Run Directly

You can run AB Download Manager directly without installing it:

```bash
nix run github:Rishabh5321/abdownloadmanager-flake
```

### Install via Flake

Add this repository to your `flake.nix` inputs:

```nix
{
  inputs = {
    nixpkgs.url = "github:NixOS/nixpkgs/nixos-unstable";
    abdownloadmanager.url = "github:Rishabh5321/abdownloadmanager-flake";
  };

  outputs = { self, nixpkgs, ... }: {
    nixosConfigurations.my-machine = nixpkgs.lib.nixosSystem {
      system = "x86_64-linux";
      modules = [
        ({ pkgs, ... }: {
          environment.systemPackages = [
            inputs.abdownloadmanager.packages.${pkgs.stdenv.hostPlatform.system}.ab-download-manager
          ];
        })
      ];
    };
  };
}
```
