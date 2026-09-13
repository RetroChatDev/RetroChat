# Live Streaming & Spaces

RetroChat supports live audio and video inside communities.

## Community Spaces (audio)

Spaces are RetroChat's own audio-only rooms hosted inside a community.

- **Start a Space** from a community page. Set a title and go live.
- Listeners join in one tap. Tap **Raise Hand** to request the mic; hosts approve or decline.
- Hosts can mute speakers, remove participants, and end the Space.
- The participant list shows who is speaking, listening, or has their hand raised.

## Community Live (video)

Broadcast video from a phone camera or from professional software.

- **Go Live** in a community opens the camera preview. Choose front or rear camera and tap **Start**.
- **OBS / RTMP** streamers can copy the RTMP server URL and stream key from the same screen and push video from OBS Studio, Streamlabs, or any RTMP encoder.
- Viewers can react, chat, and tip during the stream.
- Streams can be recorded; recordings appear in the community's video library.

## Live overlay (OBS browser source)

Community managers can add a RetroChat **Live overlay** as an OBS browser source (1920×1080, transparent). The overlay shows the community name, live status, linked token ticker, a recent-trades ticker, and any active raid countdown.

On the community live page:

1. Open **Live overlay**.
2. Tap **Copy OBS URL** and paste it as a Browser Source in OBS.
3. Use **Preview** to check the layout, or **Rotate key** if the URL was shared and you need a new one.

The overlay URL is tokenized. Anyone with the current URL can display the overlay, so rotate the key if it leaks.

## Raid kit

While a community is live, managers can start a timed **raid** that sends viewers to a target:

- Another RetroChat community that is live now.
- A Solana token mint (opens Scanner).
- An X handle, tweet, or `x.com` URL.
- A custom URL.

Set a duration (1–60 minutes; presets include 1, 2, 5, 10, 15, and 30). Viewers see a banner with the countdown and a **Follow raid** button. You can update the remaining time or **End raid** early.

Optionally leave **Ping holder chat** on so the token-gated holder room is notified when the raid starts. Viewers can also get a live-raid notification — see [Notifications](NOTIFICATIONS.md).

Raids are a coordination tool. They do not move funds.

## Holder chat ping

From the community menu or live page, managers with a holder room can **Ping holder chat**: write a short message (up to 500 characters) and optionally notify **@everyone** in that room. Use it for go-live, raids, or launches. See [Communities & Feed](COMMUNITIES_AND_FEED.md).

## Live page

The **Live** tab lists currently live streams across RetroChat.

## Soundtrack and Radio

Hosts can pick a [Live Radio](LIVE_RADIO.md) station as Space soundtrack audio where the Space UI offers it. Pause Radio or Retro TV before going live so device audio does not overlap.

## Related guides

- [Live Radio](LIVE_RADIO.md)
- [Retro TV](RETRO_TV.md)
- [Communities & Feed](COMMUNITIES_AND_FEED.md)
- [Notifications](NOTIFICATIONS.md)
