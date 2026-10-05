# Release Checklist: SMS Code Flow

**Instructions:** Use this checklist for a quick verification of the SMS code functionality during the release cycle. Do not use this for deep functional testing.

- [ ] Code arrives on the device within 30 seconds.
- [ ] Code automatically expires after 120 seconds.
- [ ] Entering a third consecutive wrong code cancels the transfer and blocks further attempts.
- [ ] Code entered after the 120-second expiry window is strictly rejected.
- [ ] Requesting a new SMS code successfully resets the 120-second expiration timer.
- [ ] Tapping the "Confirm" button twice quickly debits the account only once.
- [ ] SMS text is grammatically correct and displays properly in KZ, RU, and EN localizations.
- [ ] The customer's daily transfer total updates correctly immediately after the SMS confirmation.