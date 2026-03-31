# Technical Architect — Pulse D146

## Challenge: "Demonstration Only" Is Not a Scope — It's a Trap

### What I'm Challenging

The assumption that labeling AsyncStorage-based offline editing as "demonstration only" is an acceptable scope constraint. D140 resolved to ship with this feature and attach the label as a disclaimer. My position: the label doesn't mitigate the risk. It *hides* it.

### The Argument

Labels are for developers. Users don't read them.

When Louis shows Sprint 0 to his first beta artisan in Week 2, the feature will work exactly like a real offline editing system: enter changes, go offline, come back online, watch the queue process. The artisan has no idea this is "demonstration only." They see an app that works offline. They will use it that way — on job sites, in basements, in real workflows — because that's what the product showed them it does.

The artisan enters 3 client modifications offline. When connectivity returns, the retry queue fires. The conflict resolution strategy (server-wins, as agreed in D140) silently discards 2 of 3 changes. The artisan sees data disappear. Their reaction is not "this is a known demo limitation." Their reaction is: "this app loses my data."

That artisan now has a mental model. The app doesn't work offline for edits. They will work around it — by taking screenshots, by writing things down, by switching to a spreadsheet. By Month 3, they are not a mobile-first user. They are a workaround artist. And when Louis finally ships real offline sync in Sprint 2 or 3, that artisan has already decided the app doesn't work offline.

**"Demonstration only" features in a beta become permanent user habits.**

The compounding problem: Louis will hear positive feedback in Week 2. "Offline editing works great!" He won't hear about the data loss until it happens to a paying customer in Month 4 — when the "it was just a demo" context is long gone and the user has already concluded the product is unreliable.

### Recommended Resolution

Remove offline *editing* from Sprint 0 entirely. Not "demonstration only" offline editing. **No offline editing.**

Users may view cached client and job data offline. That's it. When they tap edit, they get a connectivity prompt. This is an honest scope constraint. It sets correct expectations: offline means "read what you cached, nothing more." No surprises when they return online.

This requires changing the D140 decision to remove the AsyncStorage retry queue for edits — keep it for reads only, or drop it entirely for Sprint 0 and add it back in Sprint 1 with proper conflict resolution.

### Why Louis Should Care

Because the first artisan who loses data to a "demonstration only" feature will never give the product a second chance. And Louis will never know it happened, or why they stopped using the app.

Trust erosion is asymmetric. You can spend 6 months building a feature. One bad first experience can unstick a user permanently. The label protects the team legally. It does not protect the product reputationally.

Ship an honest Sprint 0. No offline editing. No silent data loss. No surprises.

---

## Summary

| ID | Topic | My Position |
|----|-------|-------------|
| D140 | AsyncStorage offline editing | Remove entirely from Sprint 0; ship view-only offline cache instead of "demonstration only" editing |
| D144 | expo-sqlite cost estimate | (previously argued: real cost is 1.5–2.5 days, not +1 day) |
| D146 | "Demonstration only" labeling | Labeling does not protect the product; it hides the risk while forming bad user habits |
