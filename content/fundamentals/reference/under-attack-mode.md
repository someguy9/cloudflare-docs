---
pcx_content_type: reference
source: https://support.cloudflare.com/hc/en-us/articles/200170076-Understanding-Cloudflare-Under-Attack-mode-advanced-DDOS-protection-
title: Under Attack mode
---

# Under Attack mode

Cloudflare's **I'm Under Attack mode** performs additional security checks to help mitigate layer 7 DDoS attacks. Validated users access your website and suspicious traffic is blocked. It is designed to be used as one of the last resorts when a zone is under attack (and will temporarily pause access to your site and impact your site analytics).

When enabled, visitors receive an interstitial page.

## Enable Under Attack mode

I'm Under Attack mode is disabled by default for your zone.

### Globally

To put your entire zone in I'm Under Attack mode:

{{<render file="_under-attack-mode-dash-instructions.md" withParameters="**On**">}}

### Selectively

To turn on I'm Under Attack mode for specific pages or sections of your site, use a [configuration rule](/rules/configuration-rules/).

{{<example>}}

**When incoming requests match**

* **Field:** _URI Path_
* **Operator:** _starts with_
* **Value:** `/admin`

If you are using the Expression Editor, enter the following expression:<br>
`(starts_with(http.request.uri.path, "/admin"))`

**Then the settings are**

1. For **I'm Under Attack**, select **Add**.
2. Switch the toggle to **On**.

{{</example>}}

To turn it on for specific ASNs (hosts/ISPs that own IP addresses), countries, or IP ranges, use [IP Access Rules](/waf/tools/ip-access-rules/).

---

## Preview Under Attack mode

To preview what I'm Under Attack mode looks like for your visitors:

1. Log into the [Cloudflare dashboard](https://dash.cloudflare.com).
2. Select your account.
3. Go to **Manage Account** > **Configurations**.
4. Go to **Custom Pages**.
5. For **Managed Challenge / I'm Under Attack Mode™**, select **Custom Pages** > **View default**.

The `Checking your browser before accessing...` challenge determines whether to block or allow a visitor within five seconds. After passing the challenge, the visitor does not observe another challenge until the duration configured in [Challenge Passage](/waf/tools/challenge-passage/).

---

## Potential issues

Since the I'm Under Attack mode requires your browser to support JavaScript to display and pass the interstitial page, it is expected to observe impact on third party analytics tools.
