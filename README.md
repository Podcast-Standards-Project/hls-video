# HLS Video Podcast Demo

A demonstration of using HLS (HTTP Live Streaming) video in podcast RSS feeds through the `podcast:alternateEnclosure` tag.

## Demo Links

- **📺 Live Demo**: https://podcast-standards-project.github.io/hls-video/
- **📡 Demo RSS Feed**: https://podcast-standards-project.github.io/hls-video/feed.xml

## What We're Trying to Accomplish

Traditional podcast RSS feeds are audio-first, but many creators now produce video content alongside their audio. Current solutions often require separate feeds or force users to choose between audio and video. 

Our proposed solution uses the `podcast:alternateEnclosure` tag to offer **both audio and HLS video streams within a single RSS feed**. This "audio-first" approach:

- ✅ Maintains compatibility with existing podcast apps (they'll use the audio)
- ✅ Enables video streaming in apps that support HLS
- ✅ Should allow listeners to seamlessless switch between audio and video modes
- ✅ Uses adaptive bitrate streaming (no large file downloads)
- ✅ Automatically adjusts video quality based on connection speed
- ✅ Keeps podcasting open and RSS-based

[Read more about our plans for HLS and video podcasting](https://podstandards.org/2025/05/27/a-new-paradigm-for-video-podcasts-hls-streaming/)

## The Technical Approach

### RSS Feed Structure

Each episode includes a traditional audio enclosure followed by an alternate video enclosure:

```xml
<enclosure url="https://media.transistor.fm/346d955d/8ba0f3fb.mp3" 
           length="27892766" 
           type="audio/mpeg"/>

<podcast:alternateEnclosure type="application/x-mpegURL" 
                           length="0" 
                           bitrate="2500000" 
                           height="1080" 
                           lang="en" 
                           title="HD Video Stream" 
                           rel="alternate">
    <podcast:source uri="https://customer-wr8fi2zppse29pbk.cloudflarestream.com/18e048e0c31c0c238b46ddf581b25174/manifest/video.m3u8"/>
</podcast:alternateEnclosure>
```

### Key Attributes

- `height="1080"` - Video resolution indicator
- `rel="alternate"` - Marks this as alternative content to the primary audio
- `.m3u8` URL - Points to the HLS manifest playlist

## About HLS (HTTP Live Streaming)

HLS is an adaptive bitrate streaming protocol developed by Apple that:

- Breaks media into small segments (typically 2-10 seconds each)
- Allows streaming without downloading entire files
- Automatically adjusts quality based on bandwidth
- Works across most modern browsers and devices
- Provides a superior user experience compared to progressive download

## Technical Notes

- This demo uses **Cloudflare Stream** for video hosting and HLS delivery
- The RSS feed follows the [Podcast Namespace](https://podcastindex.org/namespace/1.0) specification
- Podcast apps that support `podcast:alternateEnclosure` can offer video playback

## Why This Matters

Video podcasting shouldn't require abandoning RSS or forcing creators into proprietary platforms. This approach keeps podcasting **open, distributed, and creator-controlled** while enabling modern streaming video experiences.

## Contributing

This is an open demonstration of a proposed standard. We welcome feedback, improvements, and real-world testing from app developers.

**Specifically** we'd love to see some apps support HLS video streaming.

---

*Part of the [Podcast Standards Project](https://podstandards.org/)*
