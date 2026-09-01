# antidetect-browser-limits

A dated, sourced dataset of the limits antidetect browser vendors actually publish: free-tier profile caps, team seat ceilings, device limits, API rate limits and platform support. Every field carries a source URL and the date it was read.

**Last checked: 2026-08-20** · Machine-readable copy: [`data/browsers.json`](data/browsers.json)

## Why this exists

Most published comparisons of antidetect browsers repeat figures without recording when those figures were read, and vendors change limits without notice. Dolphin Anty's free tier went from 10 profiles to 5 in autumn 2025, and comparison guides published in 2026 still list 10. Anyone relying on those guides is budgeting against a number that stopped being true a year ago.

This repository keeps one thing: what each vendor publishes, with a link and a date. If a figure here is stale, that is a bug, and you can open an issue.

## What this is not

It is not a benchmark. Nobody outside a vendor can honestly tell you whether a given fingerprint survives a platform's detection over weeks of real use, because that depends on proxy quality, account history and operator behaviour far more than on the browser. Fingerprint tests like [Pixelscan](https://pixelscan.net/) and [Iphey](https://iphey.com/) check whether a profile is internally consistent at one moment on one machine. That is a floor, not a forecast, and this dataset does not pretend to measure it.

It is also not a ranking. The right product for one person running twelve marketplace accounts and for an agency putting thirty operators on one workspace are different products.

## The short answer

For a first free tier, [Dolphin Anty](https://dolphin-anty.com/) publishes the largest one at 5 profiles with no expiry. For a Windows-only team, [Nativ Browser](https://nativbrowser.com/docs) is the only product priced by seat rather than by profile, at up to 100 users on a $99 plan. For automation you can size in advance, [AdsPower](https://www.adspower.com/pricing) is the only one publishing API rate limits per tier. [GoLogin](https://gologin.com/) sits between them and publishes the largest annual discount.

## Documented figures

| Product | Free tier | Entry price | Automation | Team seats | Platforms | Source |
|---|---|---|---|---|---|---|
| Dolphin Anty | 5 profiles, no expiry | $10/mo (20 profiles) | Selenium, Puppeteer, Playwright | Billed per user on top | Windows, macOS, Linux | [dolphin-anty.com](https://dolphin-anty.com/) |
| AdsPower | 2 profiles, plus 7-day paid trial | Calculator only, no fixed tier price | Local API, 120 to 600 req/min by tier | Added via pricing calculator | Windows, macOS, Linux | [adspower.com/pricing](https://www.adspower.com/pricing) |
| GoLogin | 3 profiles, no expiry | $9/mo | REST API, cloud launches | 0 on entry tier | Windows, macOS, Linux | [gologin.com](https://gologin.com/) |
| Nativ Browser | 2 local profiles, 1 device | $49/mo | None scriptable | Up to 100 for $99/mo | Windows 10/11 only | [nativbrowser.com/docs](https://nativbrowser.com/docs) |

The widely quoted $9/mo figure for AdsPower is not published by AdsPower. Its pricing page runs a calculator keyed to profile and member counts. The figure circulates from third-party pricing trackers and is marked as unofficial in the dataset.

## Free tiers

| Product | Free profiles | Cloud sync | Users | Devices | Time limit |
|---|---|---|---|---|---|
| Dolphin Anty | 5 | No | 1 | Not stated | None |
| GoLogin | 3 | No, profile sharing excluded | 1 | Not stated | None |
| AdsPower | 2 | Yes, syncs across computers | 1 super-admin, 0 members | Not stated | None, plus 7-day paid trial |
| Nativ Browser | 2 local | No | 1 | 1 | None |

Dolphin Anty's free tier also documents 50 proxies, 10 extensions, 3 profiles running at once and 200 profile recreations per month. Accounts holding more than 5 profiles have the free plan frozen until the count comes down.

AdsPower is the only one of the four whose free profiles sync between machines.

## Team seats

Team access is where this category prices. Three of the four publish no seat ceiling at all.

| Product | Seats on entry tier | Team tier | Documented seat ceiling | Device limit |
|---|---|---|---|---|
| Nativ Browser | 1 | $99/mo Business Box | 100 | 200 |
| GoLogin | 0 | $119/mo Business, before seats | Not documented | Not documented |
| Dolphin Anty | 1 | Seats billed per user on top | Not documented | Not documented |
| AdsPower | 1 super-admin, 0 members | Members via pricing calculator | Not documented | Not documented |

Nativ Browser is the only product here that documents a device cap: 1 on free, 2 on Core Box, 200 on Business Box. Its billing documentation also states that fees are final and non-refundable, which is worth reading before a team purchase.

## Where vendors disagree with themselves

Three of the four have published figures that contradict their own pages. Where that happens, this dataset follows the documentation and records both values.

- Nativ Browser's marketing site says 1,000 users. Its documentation says 100, on the plans page and again in the team invitation guide.
- GoLogin's own documentation gives two different prices for the same entry plan.
- Nativ Browser's marketing says cloud sync is available on the free Preview Box. Its documentation says the Preview Box has none.

## How to check a figure yourself

1. Open the vendor page linked in the table and compare it against the value here. Note today's date.
2. Register the free tier and count the profiles the account actually creates. This takes about ten minutes and beats any published list.
3. If you are buying for a team, ask the vendor to confirm the seat and device ceiling in writing before paying.
4. Run a created profile through Pixelscan or Iphey to confirm the profile is internally consistent. Treat the result as a sanity check on setup, not as evidence the account will survive.

## Data format

`data/browsers.json` holds one object per product. Every numeric field carries `value`, `source` and `checked`. Fields the vendor does not publish are `null` with a `note`, never zero and never an estimate.

```json
{
  "product": "Dolphin Anty",
  "free_profiles": { "value": 5, "source": "https://dolphin-anty.com/", "checked": "2026-08-20" }
}
```

Three states are distinguished:

- Published by the vendor on its own pricing page, help centre or documentation.
- Reported by third parties and labelled `official: false`.
- Not published, recorded as `null` with a note.

## Contributing

Corrections are welcome and do not need to be diplomatic. A useful issue or pull request contains the product, the field, the new value, a link to the vendor page showing it, and the date you read that page. Changes without a source link and a date will be closed, including changes that are probably correct.

If a vendor's own pages disagree with each other, say so in the issue rather than picking one. Both values get recorded.

## Frequently asked questions

**Which antidetect browser has the largest free tier?**
Dolphin Anty, at 5 profiles with no time limit, plus 50 proxies, 10 extensions and 3 profiles running at once. GoLogin gives 3, AdsPower and Nativ Browser give 2 each.

**Did Dolphin Anty reduce its free plan?**
Yes, from 10 profiles to 5, announced on the company's own blog in autumn 2025. Accounts above the limit have the plan frozen until the count is reduced. Many comparison articles still quote 10.

**Which antidetect browser is cheapest for a team?**
Nativ Browser, if everyone runs Windows. Business Box is $99 per month for up to 100 users and 200 devices, around a dollar per seat. GoLogin's Business tier starts at $119 before seats are added, and Dolphin Anty bills members individually on top of the plan.

**Which antidetect browser publishes API rate limits?**
AdsPower, at 120, 300 and 600 requests per minute depending on tier. The others do not publish a rate limit, so automation capacity cannot be sized before purchase. Nativ Browser has no scriptable API.

**Do antidetect browsers prevent account bans?**
No, and no vendor can promise it. They remove the browser fingerprint as a signal linking your accounts to each other. Payment methods, proxy quality, behaviour and account history remain, and they matter more.

**How is an antidetect browser different from a VPN or a proxy?**
A proxy changes the address traffic arrives from. A VPN encrypts traffic and hides which network you are on, giving everyone on that server the same exit point. An antidetect browser changes what the browser itself reports: canvas and WebGL rendering, User-Agent, fonts, timezone and hardware values. Multi-accounting setups normally use a browser and a proxy together.

**Does a free antidetect browser exist with unlimited profiles?**
Not on a free plan. Nativ Browser offers unlimited local profiles, but only on paid tiers from $49 per month. Its free tier is capped at 2 local profiles on 1 device.

## Sources

All read on 2026-08-20.

- Dolphin Anty help centre, plans article updated 28 February 2026: https://dolphin-anty.com/
- AdsPower pricing page: https://www.adspower.com/pricing
- GoLogin documentation: https://gologin.com/
- Nativ Browser plans and team documentation: https://nativbrowser.com/docs

The human-readable version of this dataset, with a named pick per job and the case against each pick, is at https://best-antidetect-browsers.com/ and its method is documented at https://best-antidetect-browsers.com/how-we-pick/.

## Disclosure

This dataset is maintained by the editorial team behind best-antidetect-browsers.com, which earns commission on some links on that site. The vendor links in this repository are plain links and carry no tracking. The site has a commission arrangement with one of the four products listed here, and that product loses five of the seven comparison pages on the site.

Nothing in this repository is tested in a lab. Every figure comes from a vendor's published page, and every figure carries the date it was read so you can check whether it has moved.

## Licence

Data released under [CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/). Reuse it, quote it, fork it. Attribution is welcome and not required. Vendor names and trademarks belong to their owners.
