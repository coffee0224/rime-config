# Rime config
This is a rime configuration forked from [rime-ice](https://github.com/iDvel/rime-ice), which is used in Nixos.

## Usage
1. get sha256 of git repo
```
nix run nixpkgs#nix-prefetch-git -- https://github.com/coffee0224/rime-config.git 
```
2. wrapped as nix package
```
# rime-config.nix
{ pkgs ? import <nixpkgs> {} }:

pkgs.fetchFromGitHub {
  owner  = "coffee0224";
  repo   = "rime-config";
  rev    = "b51352d95dc3e58e30f86db5a8796b7c981a6652"; # commit id
  sha256 = "0q34gq0a95fxn6gbk6amg1b1vpm1gzvl7sy29f7fc567swpjkdsq";
}
```

3. config home-manager
```
{ config, pkgs, lib, ... }:

let
  rime-config = pkgs.callPackage ./rime-config.nix {};
in
{
  home.file.".local/share/fcitx5/rime/" = {
    source = rime-config;      
    recursive = true;             
  };
}
```
