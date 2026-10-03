# Marketing Kit

Marketing Kit lets Claude answer questions about your marketing numbers: ad
spend, installs, events, campaigns, subscriptions and store reviews. It reads
Meta Ads, Facebook Pages, Instagram, TikTok Ads, Google Ads, Google Analytics 4,
Google Search Console, AppsFlyer, RevenueCat and the public App Store pages,
and it only reads, with one exception: AppsFlyer OneLink links and integration
settings can be changed, and only after you explicitly confirm each change.

## Install (before the Claude directory listing)

Until the plugin is listed in the Claude directory, you add it from this
repository, `arey325/marketing-kit-plugin`.

**claude.ai (web) and Claude Desktop**

1. Open **Customize → Plugins** (claude.ai/customize/plugins, or Customize in
   the Claude Desktop sidebar).
2. Press **Add → Add marketplace**, enter `arey325/marketing-kit-plugin` (or
   `https://github.com/arey325/marketing-kit-plugin`) and add it.
3. Open the marketplace and turn on **Sync automatically**, so plugin updates
   reach you (or press **Check for updates** from time to time).
4. Find **Marketing Kit** among the plugins and press **Add**.

If you cannot add a marketplace, download this repository as a zip
(**Code → Download ZIP**) and use **Add → Upload plugin**. An uploaded plugin
does not update by itself.

**Claude Code**

```bash
claude plugin marketplace add arey325/marketing-kit-plugin
claude plugin install marketing-kit@marketing-kit
```

Inside a session the same steps are `/plugin marketplace add
arey325/marketing-kit-plugin` and `/plugin install marketing-kit@marketing-kit`.
Then run `/reload-plugins`, open `/mcp`, pick the Marketing Kit server and
authenticate. For updates open `/plugin` → **Marketplaces** → `marketing-kit` →
**Enable auto-update** (it is off by default for marketplaces you add by hand).

**Phone (iOS and Android)**

Plugins are added on the web or in Claude Desktop, not in the phone app. A
plugin you install there is saved to your account, and its skill and connector
are available in chats in the mobile apps with the same account. If it does
not show up on the phone, use the connector without the plugin: **Customize →
Connectors → Add custom connector** → `https://marketing-kit.app/mcp`.

**After installing**

- Open the plugin → **Connectors** tab → **Connect**; sign in to Marketing Kit
  with Google or Meta and press **Allow**.
- Remove the `marketing-kit` skill you uploaded by hand (**Customize →
  Skills**) and, if you like, the local Claude Desktop extension (**Settings →
  Extensions**), so you do not have two sets of Marketing Kit tools.

Without the plugin: **Customize → Connectors → Add custom connector** →
`https://marketing-kit.app/mcp` gives you the tools without the skill.

## How to use

1. Install the plugin as described above.
2. Open the plugin's **Connectors** tab and press **Connect**.
3. Sign in at marketing-kit.app with Google or Meta.
4. On https://marketing-kit.app/connections authorize the sources you need and
   save the AppsFlyer and RevenueCat keys there.
5. Ask Claude. A good first message is: `check Marketing Kit status`.

## What is in the plugin and where your data goes

The plugin contains only a skill (instructions for Claude) and a connector
address. It has no scripts, starts no local processes and writes nothing to
your disk.

- Claude sends tool calls to `https://marketing-kit.app/mcp`: from Anthropic's
  servers when you use claude.ai, from your own machine when you use Claude Code.
- The Marketing Kit server then calls the APIs of Meta, TikTok, Google (Ads,
  Analytics, Search Console), AppsFlyer and RevenueCat, and Apple's public App
  Store endpoints, on your behalf.
- The server stores your account, your source tokens and keys (encrypted),
  temporary download files for large results (up to 24 hours) and an audit log
  of requests, without secrets.

Read the [Privacy Policy](https://marketing-kit.app/privacy) and the
[Terms](https://marketing-kit.app/terms) for details.

## Contact

connect@valas.team

## License

MIT, see `LICENSE`.
