# V-Kit

Marketing Kit: your ad, app and subscription numbers — in Claude and ChatGPT.

V-Kit (Marketing Kit) lets Claude answer questions about your marketing numbers: ad
spend, installs, events, campaigns, subscriptions and store reviews. It reads
Meta Ads, Facebook Pages, Instagram, TikTok Ads, Google Ads, Google Analytics 4,
Google Search Console, AppsFlyer, RevenueCat, App Store Connect (your own
apps, with a team key you save on the site) and the public App Store pages. It
only reads, with two exceptions, each made only after you explicitly confirm
the change: AppsFlyer OneLink links and integration settings, and turning on
App Store Connect Analytics Reports.

V-Kit is free while in beta; pricing will be announced in advance.

## Quickest way: a custom connector (no plugin needed)

Do this on claude.ai in a web browser, not in the Claude Desktop app — the
connector is saved to your Claude account and then works in Claude Desktop and
on your phone too.

1. Open https://claude.ai/customize/connectors → **Add custom connector**.
   Name: `V-Kit`, URL: `https://marketing-kit.app/mcp`. Leave the OAuth
   client fields empty and press **Add**.
2. Press **Connect**, sign in with Google or Meta and press **Allow**. Then
   authorize your sources on https://marketing-kit.app/connections.
3. Start a new chat (https://claude.ai/new) and ask: “Check my V-Kit status”.

The plugin below is optional: it adds a reference skill next to the same
connector.

## Install the plugin (optional, before the Claude directory listing)

Until the plugin is listed in the Claude directory, you add it from this
repository, `arey325/marketing-kit-plugin`.

**claude.ai (web) and Claude Desktop**

1. Open **Customize → Plugins** (claude.ai/customize/plugins, or Customize in
   the Claude Desktop sidebar).
2. Press **Add → Add marketplace**, enter `arey325/marketing-kit-plugin` (or
   `https://github.com/arey325/marketing-kit-plugin`) and add it.
3. Open the marketplace and turn on **Sync automatically**, so plugin updates
   reach you (or press **Check for updates** from time to time).
4. Find **V-Kit** among the plugins and press **Add**.

If you cannot add a marketplace, download this repository as a zip
(**Code → Download ZIP**) and use **Add → Upload plugin**. An uploaded plugin
does not update by itself.

**Claude Code**

```bash
claude plugin marketplace add arey325/marketing-kit-plugin
claude plugin install v-marketing-kit@v-marketing-kit
```

Inside a session the same steps are `/plugin marketplace add
arey325/marketing-kit-plugin` and `/plugin install v-marketing-kit@v-marketing-kit`.
Then run `/reload-plugins`, open `/mcp`, pick the v-marketing-kit server and
authenticate. For updates open `/plugin` → **Marketplaces** → `v-marketing-kit` →
**Enable auto-update** (it is off by default for marketplaces you add by hand).

**Phone (iOS and Android)**

Plugins are added on the web or in Claude Desktop, not in the phone app. A
plugin you install there is saved to your account, and its skill and connector
are available in chats in the mobile apps with the same account. If it does
not show up on the phone, use the connector without the plugin: **Customize →
Connectors → Add custom connector** → `https://marketing-kit.app/mcp`.

**After installing**

- Open the plugin → **Connectors** tab → **Connect**; sign in to V-Kit
  with Google or Meta and press **Allow**.
- Remove a skill you uploaded by hand (`v-marketing-kit`, or the older
  `marketing-kit`: **Customize → Skills**) and, if you like, the local
  Claude Desktop extension (**Settings → Extensions**), so you do not have two
  sets of V-Kit tools. Had Marketing Kit before? See the next section.

Without the plugin: **Customize → Connectors → Add custom connector** →
`https://marketing-kit.app/mcp` gives you the tools without the skill.

## Had Marketing Kit before?

Up to version 1.12 V-Kit was installed under the name `marketing-kit`. The new
plugin, skill and extension are called `v-marketing-kit`: they are new items,
so remove the old one once by hand, otherwise Claude shows every tool twice.
Step by step: https://marketing-kit.app/install#migrate.

- **Plugin, claude.ai and Claude Desktop:** **Customize → Plugins → Marketing
  Kit → Uninstall**. Remove the `marketing-kit` marketplace, add
  `arey325/marketing-kit-plugin` again (its name is now `v-marketing-kit`) and
  install **V-Kit**.
- **Plugin, Claude Code:**

  ```bash
  claude plugin uninstall marketing-kit@marketing-kit
  claude plugin marketplace remove marketing-kit
  claude plugin marketplace add arey325/marketing-kit-plugin
  claude plugin install v-marketing-kit@v-marketing-kit
  ```

- **Claude Desktop extension:** remove **Marketing Kit** in **Settings →
  Extensions** before installing V-Kit.
- **A skill uploaded by hand:** delete `marketing-kit` in **Customize →
  Skills**.
- **A custom connector added by URL** keeps working (the address
  `https://marketing-kit.app/mcp` is the same); do not add it a second time
  next to the plugin.

## How to use

1. Install the plugin as described above.
2. Open the plugin's **Connectors** tab and press **Connect**.
3. Sign in at marketing-kit.app with Google or Meta.
4. On https://marketing-kit.app/connections authorize the sources you need and
   save the AppsFlyer, RevenueCat and App Store Connect keys there.
5. Ask Claude. A good first message is: `check V-Kit status`.

## What is in the plugin and where your data goes

The plugin contains only a skill (instructions for Claude) and a connector
address. It has no scripts, starts no local processes and writes nothing to
your disk.

- Claude sends tool calls to `https://marketing-kit.app/mcp`: from Anthropic's
  servers when you use claude.ai, from your own machine when you use Claude Code.
- The V-Kit server then calls the APIs of Meta, TikTok, Google (Ads,
  Analytics, Search Console), AppsFlyer, RevenueCat and Apple (App Store Connect
  with a short-lived token the server signs from your saved key, and the public
  App Store endpoints), on your behalf.
- The server stores your account, your source tokens and keys (encrypted),
  temporary download files for large results (up to 24 hours) and an audit log
  of requests, without secrets.

Read the [Privacy Policy](https://marketing-kit.app/privacy) and the
[Terms](https://marketing-kit.app/terms) for details.

## Contact

connect@valas.team

## License

MIT, see `LICENSE`.
