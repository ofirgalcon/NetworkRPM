# NetworkRPM

A small macOS app from [GalCon](https://www.gal.uk). It tests how fast your network is and how it actually feels when the link is under pressure — the part that matters most for real use.

![NetworkRPM](NetworkRPM.png)

Click **Test** to run a measurement. **Save** (⌘S) writes the last result to a text file, including an Ethernet or Wi-Fi snapshot taken at the moment the test started.

## Why responsiveness matters

Speed tells you how wide the pipe is. But a wide pipe can still make video calls stutter, games lag, or pages feel sticky — especially on a shared or loaded connection.

Responsiveness measures exactly that. It probes the network while the link is saturated, so the score reflects how things actually behave when it matters. Idle delay, by contrast, is the quiet-link round trip — useful context, but an optimistic reading.

The Responsiveness score is in RPM (round trips per minute). Higher is better. Lower milliseconds are better.

More background: [Apple Network Responsiveness](https://support.apple.com/en-us/HT212313) and the [Network Quality community wiki](https://github.com/network-quality/community/wiki).

## Requirements

- macOS 14.6 or later

## What you're looking at

**Uplink / download** — the Mbps the connection can carry in each direction. Think of it as pipe width.

The **Accuracy** label (Low / Medium / High) next to these numbers tells you how much you can trust that Mbps figure. It is not a grade of how fast the connection is.

**Idle** — round-trip delay when the link is quiet, shown in milliseconds and RPM. Lower ms and higher RPM are both good. Accuracy here means the same thing: how reliable is this particular reading.

**Responsiveness** — how the network feels when the path is loaded. The quality label (Low / Medium / High / Very High) is the experience grade. A High or Very High score means the connection held up well under traffic. Accuracy here is separate from quality — it tells you how much to trust the reading, not how good the experience was. You can absolutely have Medium quality with High accuracy; they're measuring different things.

**Transport / Security / HTTP / HTTP loaded** — delay at each stage while the link is busy. Transport is often blank when you're running HTTP/3.

**Caption** — shows protocol, interface, and test server.

**Ethernet** — port speed, duplex, and media, captured the moment you clicked Test.

**Wi-Fi** — radio rate, SNR, RSSI, noise, and channel, captured the moment you clicked Test.

## Colours in the UI

The app uses colour to help you read results at a glance:

- **Uplink is teal, download is blue** — so you can tell the two directions apart without squinting.
- **Responsiveness** turns green for a good experience (High or Very High quality), orange for Medium, and red for Low.
- **Idle and the latency row** shade greener as RPM climbs.
- **Wi-Fi SNR** shades greener with a stronger signal.

## Using the app

1. Open **NetworkRPM**.
2. Pick your options in the toolbar, then click **Test**. Speed and RPM update while the test runs.
3. Hover any **ⓘ** icon for a plain-English explanation of that control or result.
4. For the full help page, click **?** next to Save, or go to **Help → NetworkRPM Help**.

| Option | What it does |
| --- | --- |
| **Interface** | Which connection to test. Automatic uses your Mac's default. Only connections currently in use appear here. |
| **Mode** | Parallel tests upload and download at the same time. Sequential does them one after the other. |
| **Protocol** | Automatic picks for you. Force HTTP/2 or HTTP/3 (QUIC) if you need to compare protocols. |
| **Time** | Cap how long the test runs, or leave it Automatic so it stops when it has enough samples. |

The test saturates the link for up to the time you set. Don't run it on a metered or shared connection you care about.

## Install

macOS 14.6 or later. Universal (Apple silicon and Intel).

**DMG:** [Download NetworkRPM](https://github.com/ofirgalcon/NetworkRPM/releases/latest/download/NetworkRPM.dmg) and drag it to Applications.

**PKG:** [Download the installer](https://github.com/ofirgalcon/NetworkRPM/releases/latest/download/NetworkRPM.pkg), or deploy it with MDM.

Older builds: [Releases](https://github.com/ofirgalcon/NetworkRPM/releases).

**Homebrew** (cask — GUI apps are not formulas):

```bash
brew install --cask networkrpm
```

That command works once the cask is on Homebrew. It fetches the disk image from GitHub Releases.

If you still have the old **NetworkQuality** app, quit it and remove it after installing.

## Deploying

The installer pkg drops **NetworkRPM** into `/Applications`. No restart needed — just quit the app first if it is already open.

**Munki:** import the [pkg from Releases](https://github.com/ofirgalcon/NetworkRPM/releases/latest/download/NetworkRPM.pkg) — receipt is `com.gal.NetworkQuality`. Pin a version with the tagged URL (`.../releases/download/vX.Y.Z/NetworkRPM.pkg`).

**Jamf:** Upload that pkg as a package and deploy as usual.

## License

Copyright © 2024–2026 [GalCon](https://www.gal.uk).

Free to use and to pass on at no charge — personal or commercial — as long as you credit GalCon and include a link to [gal.uk](https://www.gal.uk). You may not sell the app.
