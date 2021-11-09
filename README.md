# Hacker-Scoper
[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2FPinkDev1%2Fhacker-scoper&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=false)](https://hits.seeyoufarm.com)
[![goreleaser](https://github.com/PinkDev1/hacker-scoper/actions/workflows/gorelease.yml/badge.svg)](https://github.com/PinkDev1/hacker-scoper/actions/workflows/gorelease.yml)  
[![forthebadge](https://forthebadge.com/images/badges/made-with-go.svg)](https://forthebadge.com) 
[![forthebadge](https://forthebadge.com/images/badges/built-with-love.svg)](https://forthebadge.com)
[![forthebadge](https://forthebadge.com/images/badges/cc-sa.svg)](https://forthebadge.com)
[![forthebadge](https://forthebadge.com/images/badges/check-it-out.svg)](https://forthebadge.com)
[![forthebadge](https://forthebadge.com/images/badges/fo-real.svg)](https://forthebadge.com)

This is a go1.17.2 application made for quickly filtering out URLs and IP addresses which are outside of our scope. Designed with bug-bounty programs in mind, the tool will match your given `targets` URLs/IPv4s/IPv6s with those from a locally stored copy of the full [firebounty](https://firebounty.com) json of scraped scopes, OR with your own list of scopes!

## Features

- Automagically match your targets from an automatically-updated local scopes collection.
- Use your own scopes file
- Set "explicit-level" (Parse (all as) wildcards?)
- Match IPv4s
- Match IPv6s
- Match any valid URL ([RFC 3986](https://www.rfc-editor.org/rfc/rfc3986.html) Compliant)
- Attempt to scrape security.txt files from your targets
- 100% chainable with other tools: Just use `--chain-mode`, and begin piping targets into STDIN!
- Detection of mis-configured bug-bounty programs

## Installation

Download a pre-built binary from the releases page, or run:

`git clone github.com/PinkDev1/hacker-scoper && cd hacker-scoper && go build`

## Usage

```
Usage: ./hacker-scoper --file /path/to/targets [--company company | --custom-scopes-file /path/to/scopes] [--explicit-level INT] [--reuse Y/N] [--chain-mode]
Example: ./hacker-scoper --file /home/kali/Downloads/recon-targets.txt --company google --explicit-level 2
  -c, --company string
      Specify the company name to lookup.

  -cstxt, --check-security-txt
      Whether or not we will try to scrape security.txt from all domains and subdomains

  -r, --reuse string
      Reuse previously generated security.txt lists? (Y/N)
          Only needed if using "-cstxt"

  -f, --file string
      Path to your file containing URLs

  -csf, --custom-scopes-file string
      Path to a custom plaintext file containing scopes
            Default: false

  -e, --explicit-level int
      How explicit we expect the scopes to be:
       1 (default): Include subdomains in the scope even if there's not a wildcard in the scope
       2: Include subdomains in the scope only if there's a wildcard in the scope
       3: Include subdomains in the scope only if they are explicitly within the scope

  -ch, --chain-mode
      In "chain-mode" we only output the important information. No decorations.
            Default: false

  NOTE: Targets won't be matched if they don't have a valid scheme:
    ✅ http://target.com
    ✅ mongodb://127.0.0.1
    ❌ target.com
    ❌ 127.0.0.1
```

The firebounty json is automatically updated every 24hs

## Special thank you
This project was inspired by the [yeswehack_vdp_finder](https://github.com/yeswehack/yeswehack_vdp_finder)

## License
All of the code on this repository is licensed under the *Creative Commons Attribution-ShareAlike License*. A copy can be seen as `LICENSE` on this repository.
