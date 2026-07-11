MiniDeluxe
==========

Light-weight Ham Radio Deluxe drop-in replacement for feeding PowerSDR into HRD

What's new in this version
--------------------------

This version adds support for the newer Ham Radio Deluxe Rig Control protocol observed in recent HRD clients.

MiniDeluxe can now expose two independent HRD TCP listeners at the same time:

- Legacy HRD protocol listener, preserving the original MiniDeluxe behavior and compatibility with older clients.
- New HRD protocol listener, intended for newer HRD clients that use the updated command vocabulary.

Both listeners share the same radio state, so frequency and mode changes remain synchronized.

By default:

- Legacy protocol port: `7809`
- New HRD protocol port: `7810`
- New protocol context id: `179`
- New protocol radio name: `SMART SDR`

These values can be changed in the MiniDeluxe options window under the `HRD Protocols` tab.

Available information in the new HRD protocol
---------------------------------------------

The new protocol listener currently supports the information needed for HRD clients to identify the radio and track the core operating state:

- Radio context id
- Radio name
- VFO A frequency
- VFO B frequency setting support
- Current mode
- Mode list
- AGC text
- AGC list
- Basic dropdown metadata
- Basic button metadata
- Basic slider metadata

Implemented new-protocol commands include:

- `get context`
- `get radios`
- `[id] get dropdowns`
- `[id] get buttons`
- `[id] get sliders`
- `[id] get freqx`
- `[id] get dropdown-list {Mode}`
- `[id] get dropdown-text {Mode}`
- `[id] get dropdown-list {AGC}`
- `[id] get dropdown-text {AGC}`
- `[id] set dropdown Mode <mode> <index>`
- `[id] set frequencies-hz <vfoa> <vfob>`

The mode list exposed to new HRD clients is:

```text
LSB,USB,CWL,CW,FM,AM,DIGU,DIGL
```

`CW` is presented as a plain CW mode to the HRD client and mapped internally to the appropriate CAT mode used by MiniDeluxe/PowerSDR.

Current limitations
-------------------

Button and slider controls are advertised as metadata only in this version. Their write behavior is intentionally left as a stub until more packet captures confirm the exact syntax used by HRD for controls such as:

- TX
- Split
- NR
- RF power

The legacy HRD protocol behavior is preserved as closely as possible for existing MiniDeluxe users.

Please visit the wiki for more information: https://github.com/krisp/MiniDeluxe/wiki
