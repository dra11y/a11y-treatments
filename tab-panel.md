# Dr. A11y's Tab Panel Treatment

## How to make a tab panel control accessible to screen reader users.

The original tab control panel code was taken from [this W3Schools: How To Create Tabs example](https://www.w3schools.com/howto/howto_js_tabs.asp).

### Diagnosis: Sick (Inaccessible) Tab Control
- User finds the buttons, but doesn't know what they will do when clicked.
- User does not know they are using a tab control.
- The screen reader is unable to indicate which tab is currently selected.
- When a button is clicked, nothing appears to happen for the screen reader user.
- The user cannot skip the remaining tabs after selecting one.
- There is no separation of the tab panel content from the rest of the page.

### Treatment
- Add `role="tablist"` and `aria-label="Cities"` to the button container to make it a tab group.
- To each tab `<button>` element:
  - Add `role="tab"` to change it from a button to a tab for screen readers.
  - Assign a unique DOM ID to each tab.
  - Add `aria-selected="true"` to the default active tab, and `aria-selected="false"` to the others.
- To each `<div class="tabcontent">` tab panel:
  - Add a `role="tabpanel"` attribute.
  - Add a `aria-labelledby="tab-1"` attribute, where `tab-1` is the DOM ID assigned to the corresponding tab button above.
  - Add a `tabindex="0"` attribute to allow keyboard focus on the content.
- In the JavaScript:
  - Set the `aria-selected` attribute on each button to `true` on the selected tab, `false` otherwise.
  - Set the focus to the appropriate `<div class="tabcontent">` tab panel after the tab is changed.
    - Make this happen asynchronously (with `setTimeout`) due to a glitch in some screen readers (VoiceOver on Mac).

### Prognosis: Treated, Healthy (Accessible) Tab Control
- The tab group is clearly delineated and announced to the user.
- The selected tab is clearly indicated.
- When clicked, the remaining tabs are skipped and focus changes to the tab panel content.
- The tab panel content is grouped separately from the page content, so it's clear when the user leaves the tab panel.
- It is easy for the user to get out of the tab panel and back to the tab group.

### Code
- [View **Sick** Tab Panel code on GitHub](https://github.com/dra11y/a11y-treatments/blob/main/tab-panel-sick.html)
- [View **Treated (Accessible)** Tab Panel code on GitHub](https://github.com/dra11y/a11y-treatments/blob/main/tab-panel-treated.html)
- [View **Treatment `diff`** on GitHub](https://github.com/dra11y/a11y-treatments/commit/3599e6)
