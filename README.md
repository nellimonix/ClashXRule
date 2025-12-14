# OpenCCK Clash Rules

[Русская версия](README_RU.md) | English

This project generates rules for [Clash Premium](https://github.com/Dreamacro/clash/releases/tag/premium) based on domain lists from [OpenCCK](https://iplist.opencck.org/). Automatic builds occur daily at 21:00 UTC using GitHub Actions.

## Available Rule Lists

### Online Addresses (URL)

Use these URLs in your Clash configuration in the `rule-providers` section:

- **Adult Content Sites (porno.txt)**:
  - `https://raw.githubusercontent.com/nellimonix/ClashXRule/release/porno.txt`
  - `https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/porno.txt`

- **Discord (discord.txt)**:
  - `https://raw.githubusercontent.com/nellimonix/ClashXRule/release/discord.txt`
  - `https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/discord.txt`

- **YouTube (youtube.txt)**:
  - `https://raw.githubusercontent.com/nellimonix/ClashXRule/release/youtube.txt`
  - `https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/youtube.txt`

- **Social Networks (socials.txt)**:
  - `https://raw.githubusercontent.com/nellimonix/ClashXRule/release/socials.txt`
  - `https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/socials.txt`

- **Torrent Sites (torrent.txt)**:
  - `https://raw.githubusercontent.com/nellimonix/ClashXRule/release/torrent.txt`
  - `https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/torrent.txt`

- **Developer Tools (tools.txt)**:
  - `https://raw.githubusercontent.com/nellimonix/ClashXRule/release/tools.txt`
  - `https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/tools.txt`

- **Music Services (music.txt)**:
  - `https://raw.githubusercontent.com/nellimonix/ClashXRule/release/music.txt`
  - `https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/music.txt`

- **Roblox (roblox.txt)**:
  - `https://raw.githubusercontent.com/nellimonix/ClashXRule/release/roblox.txt`
  - `https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/roblox.txt`

## Usage

### Rule Providers Configuration

```yaml
rule-providers:
  porno:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/porno.txt"
    path: ./ruleset/porno.yaml
    interval: 86400

  discord:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/discord.txt"
    path: ./ruleset/discord.yaml
    interval: 86400

  youtube:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/youtube.txt"
    path: ./ruleset/youtube.yaml
    interval: 86400

  socials:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/socials.txt"
    path: ./ruleset/socials.yaml
    interval: 86400

  torrent:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/torrent.txt"
    path: ./ruleset/torrent.yaml
    interval: 86400

  tools:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/tools.txt"
    path: ./ruleset/tools.yaml
    interval: 86400

  music:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/music.txt"
    path: ./ruleset/music.yaml
    interval: 86400
```

### Example Rules Configuration

#### Content Filtering Mode

```yaml
rules:
  # Block adult content
  - RULE-SET,porno,REJECT
  
  # Route social networks and messengers through proxy
  - RULE-SET,discord,PROXY
  - RULE-SET,socials,PROXY
  - RULE-SET,youtube,PROXY
  
  # Block torrents
  - RULE-SET,torrent,REJECT
  
  # Allow developer tools directly
  - RULE-SET,tools,DIRECT
  
  # Route music services through proxy
  - RULE-SET,music,PROXY
  
  # Default route
  - MATCH,DIRECT
```

#### Bypass Censorship Mode

If you're in a region with internet restrictions and want to bypass them:

```yaml
rules:
  # Bypass restrictions through proxy
  - RULE-SET,discord,PROXY
  - RULE-SET,socials,PROXY
  - RULE-SET,youtube,PROXY
  - RULE-SET,music,PROXY
  - RULE-SET,tools,PROXY
  
  # Optional: block torrents to save bandwidth
  - RULE-SET,torrent,REJECT
  
  # Optional: block adult content
  - RULE-SET,porno,REJECT
  
  # Default direct connection
  - MATCH,DIRECT
```

#### Parental Control Mode

```yaml
rules:
  # Block inappropriate content
  - RULE-SET,porno,REJECT
  - RULE-SET,torrent,REJECT
  
  # Allow educational and work tools
  - RULE-SET,tools,DIRECT
  
  # Control social media access (can be set to REJECT if needed)
  - RULE-SET,discord,PROXY
  - RULE-SET,socials,PROXY
  - RULE-SET,youtube,PROXY
  - RULE-SET,music,PROXY
  
  # Default route
  - MATCH,DIRECT
```

## Data Sources

All rules are generated based on domain lists from [OpenCCK](https://iplist.opencck.org/):

- Adult Content: https://iplist.opencck.org/?format=text&data=domains&group=porn
- Discord: https://iplist.opencck.org/?format=text&data=domains&group=discord
- YouTube: https://iplist.opencck.org/?format=text&data=domains&group=youtube
- Social Networks: https://iplist.opencck.org/?format=text&data=domains&group=socials
- Torrent Sites: https://iplist.opencck.org/?format=text&data=domains&group=torrent
- Developer Tools: https://iplist.opencck.org/?format=text&data=domains&group=tools
- Music Services: https://iplist.opencck.org/?format=text&data=domains&group=music

## Installation

1. Create a new repository on GitHub
2. Copy files from this project
3. Replace `nellimonix/ClashXRule` in README with actual values
4. Enable GitHub Actions in repository settings
5. Run the workflow manually or wait for automatic execution

## Features

- **Daily Updates**: Automatic rule generation every day at 06:00 UTC
- **Multiple Categories**: 7 different rule categories for flexible traffic management
- **CDN Support**: Files available through both GitHub raw URLs and jsDelivr CDN
- **Wildcard Support**: Proper handling of domain wildcards for comprehensive coverage
- **Clash Premium Compatible**: Optimized for Clash Premium core

## License

This project is licensed under the GNU General Public License v3.0 - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- [OpenCCK](https://iplist.opencck.org/) for providing comprehensive domain lists
- [Loyalsoldier/clash-rules](https://github.com/Loyalsoldier/clash-rules) for inspiration and project structure
- The open-source community for continuous improvements