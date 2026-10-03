# Marketing Kit

Marketing Kit lets Claude answer questions about your marketing numbers: ad
spend, installs, events, campaigns, subscriptions and store reviews. It reads
Meta Ads, Facebook Pages, Instagram, TikTok Ads, Google Ads, Google Analytics 4,
Google Search Console, AppsFlyer, RevenueCat and the public App Store pages,
and it only reads, with one exception: AppsFlyer OneLink links and integration
settings can be changed, and only after you explicitly confirm each change.

## How to use

1. Install this plugin in Claude (claude.ai, Claude Desktop or Claude Code).
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
