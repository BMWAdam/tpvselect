![Repo Overview](https://raw.githubusercontent.com/BMWAdam/tpvselect/badges/badges/loc-badge.svg)


# TPV - SELECT
## Deployment
- for Hetzner@178.104.211.77
  &rarr; just <pre>./deploy.sh</pre>
- for adding a new server, modify [Flake](flake.nix)
  &rarr;
<pre>
nixosConfigurations.<name_of_new_server> = nixpkgs.lib.nixosSystem {
  system = "<architecture>"; #perhaps x86_64-linux
  specialArgs = {
    inherit kubenixconfig tpvsel;
  };

  modules = [
    # do not change this:
    disko.nixosModules.disko
    ./src/configuration/configuration.nix

    # if you want <b>to alter</b> the new server somehow, replace <i>server1.nix</i> with desired configuration.
    ./servers/server1.nix

    # for sharing secrets among various server configurations
    ./src/configuration/secrets.nix
    sops-nix.nixosModules.sops
  ];
};
</pre>
