# Example usage in your server's flake.nix:
{
  inputs = {
    nixpkgs.url = "github:nixpkgs/nixpkgs/nixos-unstable";
    test-script.url = "github:ilios/scripts";  # Replace with your repo URL
  };

  outputs = { self, nixpkgs, test-script }: {
    nixosConfigurations.<YOUR_HOSTNAME> = nixpkgs.lib.nixosSystem {
      system = "x86_64-linux";  # Adjust for your system
      modules = [
        {
          environment.systemPackages = [
            test-script.packages.x86_64-linux.fromFile
          ];
        }
      ];
    };
  };
}
