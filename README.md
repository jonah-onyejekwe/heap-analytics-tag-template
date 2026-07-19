# Heap Analytics Tag — Unofficial GTM Template

A community-built Google Tag Manager custom tag template that lets you implement
Heap Analytics tracking directly inside GTM — no custom HTML or JavaScript required.

---

## Overview

This template gives you access to the core Heap Analytics client-side APIs through
a simple point-and-click interface inside Google Tag Manager. Whether you need to
identify users, track custom events, attach properties, or send pageviews, everything
is configurable through the tag UI without touching a line of code.

> **This is an unofficial community template and is not affiliated with or endorsed by Heap.**

---

## Supported Tag Types

| Tag Type | What It Does |
|---|---|
| **Identify** | Assigns a unique identity to a user |
| **Track Event** | Sends a custom event, with optional properties |
| **Add User Properties** | Attaches properties at the user level |
| **Add Event Properties** | Attaches global properties to all subsequent events |
| **Remove Event Property** | Stops a specific event property from being attached |
| **Clear Event Properties** | Removes all stored event properties |
| **Page View** | Sends a pageview hit with optional metadata |
| **Add Pageview Properties** | Attaches custom properties to the current pageview |

---

## Requirements

- An active [Heap Analytics](https://heap.io) account
- The Heap base snippet must already be loaded on your site before this tag fires
- A Google Tag Manager web container

---

## Installation

### Option 1 — Import from GitHub

1. Download the `.tpl` file from this repository.
2. In Google Tag Manager, go to **Templates** in the left navigation.
3. Under **Tag Templates**, click **New**.
4. Click the **More Actions** menu (⋮) in the top right and select **Import**.
5. Select the downloaded `.tpl` file.
6. Click **Save**.

The template will now appear under the **Custom** section when creating a new tag.

### Option 2 — Community Template Gallery

> Once approved, this template will be available directly inside GTM.

1. In Google Tag Manager, click **Tags → New**.
2. Click **Tag Configuration** and then **Discover more tag types in the Community Template Gallery**.
3. Search for **Heap Analytics Tag Unofficial**.
4. Click the template and select **Add to workspace**.
5. Configure the tag and save.

---

## Setup

Before configuring the tag, make sure the Heap snippet is installed and loading
on your site. You can find your snippet inside your Heap account settings.

Once the template is installed:

1. Go to **Tags → New** in your GTM container.
2. Click **Tag Configuration** and select **Heap Analytics Tag** from the Custom section.
3. Choose the **Heap Analytics Tag Type** that matches what you want to do.
4. Fill in the fields for that tag type (see the configuration guide below).
5. Set your trigger.
6. Save and publish.

---

## Configuration Guide

### Identify

Use this to assign a persistent unique identity to a user — typically after login.

| Field | Description |
|---|---|
| **User ID** | The unique identifier for the user, such as an email address, user ID, or username. Must be a non-generic, truly unique value — passing values like `undefined` or `null` will merge unrelated user profiles. |

> [Heap Identify API reference →](https://developers.heap.io/reference/identify)

---

### Track Event

Use this to send a named custom event to Heap, such as a button click, form
submission, or purchase.

| Field | Description |
|---|---|
| **Event Name** | The name of the event you want to track. |
| **Include Event Properties** | Enable this to attach key-value properties to the event. |
| **Event Properties table** | Add one row per property. Enter the property name in the left column and its value in the right column. |

---

### Add User Properties

Use this to attach persistent properties to the current user's profile, such as
account tier, company name, or database attributes. These properties are stateless —
only the most recent value is stored.

| Field | Description |
|---|---|
| **User Properties table** | Add one row per property. Enter the property name in the left column and its value in the right column. |

> [Heap Add User Properties API reference →](https://developers.heap.io/reference/adduserproperties)

---

### Add Event Properties

Use this to attach global key-value pairs that will be appended to all subsequent
events fired by the user during their session. Useful for stateful context like
login status or subscription plan.

| Field | Description |
|---|---|
| **Event Properties table** | Add one row per property. Enter the property name in the left column and its value in the right column. |

> [Heap Add Event Properties API reference →](https://developers.heap.io/reference/addeventproperties)

---

### Remove Event Property

Use this to stop a specific event property from being attached to subsequent events.
This is typically used after calling **Add Event Properties** when that context is
no longer relevant.

| Field | Description |
|---|---|
| **Event Property Name** | The exact name of the event property you want to remove. |

> [Heap Remove Event Property API reference →](https://developers.heap.io/reference/removeeventproperty)

---

### Clear Event Properties

Removes all event properties that have been stored in the current session cookie,
ensuring that properties added by a future **Add Event Properties** call are always
fresh and relevant.

No additional fields are required. This tag type executes immediately when fired.

> [Heap Clear Event Properties API reference →](https://developers.heap.io/reference/cleareventproperties)

---

### Page View

Sends a pageview hit to Heap. By default, the template will automatically detect
the current page URL, page title, and referrer. Each of these can optionally be
overridden manually.

| Field | Description |
|---|---|
| **Manually Pass Page URL** | Enable to override the detected page URL with a custom value. |
| **Page URL Variable** | The variable or value to use as the page URL when manual override is on. |
| **Manually Pass The Page Title** | Enable to override the detected page title with a custom value. |
| **Page Title Variable** | The variable or value to use as the page title when manual override is on. |
| **Manually Pass The Previous Page Value** | Enable to override the detected referrer with a custom value. |
| **Previous Page URL Variable** | The variable or value to use as the previous page when manual override is on. |
| **Include Page Properties** | Enable to attach additional key-value properties to this pageview. |
| **Page Properties table** | Add one row per property. Enter the property name in the left column and its value in the right column. |

---

### Add Pageview Properties

Attaches custom properties to the current pageview. Useful for enriching pageview
data with context such as page category or content type.

| Field | Description |
|---|---|
| **Page Properties table** | Add one row per property. Enter the property name in the left column and its value in the right column. |

> [Heap API Reference →](https://developers.heap.io/docs/api-reference)

---

## Triggering Recommendations

| Tag Type | Recommended Trigger |
|---|---|
| Identify | Custom event fired after successful login or user resolution |
| Track Event | The specific interaction trigger (e.g. click, form submit) |
| Add User Properties | DOM Ready or Window Loaded, after user data is available |
| Add Event Properties | DOM Ready or Window Loaded, early in the page lifecycle |
| Remove Event Property | Trigger tied to logout or state change |
| Clear Event Properties | Fire before **Add Event Properties** on the same page |
| Page View | DOM Ready or a History Change trigger for SPAs |
| Add Pageview Properties | DOM Ready, after page context is resolved |

---

## Testing & Validation

1. Enable **GTM Preview Mode** before publishing.
2. Browse your site and trigger the relevant interactions.
3. In the GTM Preview panel, confirm the tag fires with a ✅ status.
4. Open your browser's developer console and check for `[Heap Analytics]` log
   entries — enable **Console Log** in the Optional Configuration section of the
   tag if you don't see them.
5. In your Heap dashboard, go to **Live View** to confirm events and properties
   are arriving in real time.

---

## Optional Configuration

| Field | Description |
|---|---|
| **Enable Console Log** | When checked, diagnostic messages are logged to the browser console and GTM Preview Mode for each tag execution. Useful during development and QA. Disable before going to production. |

---

## Troubleshooting

**The tag fires but nothing appears in Heap**
Make sure the Heap base snippet is loading before this tag fires. Use a DOM Ready
or Window Loaded trigger, or set the Heap snippet tag to fire before this one using
tag sequencing.

**User profiles are being merged unexpectedly**
This is almost always caused by the **Identify** tag receiving a non-unique value
such as `undefined`, `null`, or a generic placeholder. Check the value your User ID
variable is resolving to in GTM Preview Mode before publishing.

**Page URL, title, or referrer is incorrect**
If automatic detection is picking up the wrong value — common on single-page
applications — enable the manual override options and pass the correct GTM
variable for each field.

**Event properties are carrying over between sessions**
Use the **Clear Event Properties** tag type, configured to fire early in the page
lifecycle, before your **Add Event Properties** tag fires.

**Console log shows `heap object not found`**
The Heap snippet has not loaded at the time this tag fires. Adjust your trigger
timing or use tag sequencing to ensure Heap initialises first.

---

## Notes & Limitations

- This template requires the Heap base snippet to be independently installed on
  your website. The template does not load the snippet itself.
- Heap's `addPageviewProperties` API is designed to be called within a Heap adapter
  for natural pageviews. When used via GTM, ensure it fires at the right point in
  the page lifecycle.
- All field values passed through GTM variables are resolved at the time the tag
  fires. Ensure your variables are populated before the trigger condition is met.
- Custom and Community Templates are supported on web containers only. Mobile
  container support is not available.

---

## License

This project is licensed under the [Apache 2.0 License](LICENSE).

---

## Contributing

Contributions, bug reports, and feature suggestions are welcome.
Please open an issue or submit a pull request.

---

## Developed With ❤️ By Jonah Onyejekwe

**[View Jonah Onyejekwe On LinkedIn](https://www.linkedin.com/in/your-linkedin-url)**
