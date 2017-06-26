# polycast
I am following through Polycasts from Rob Dodson

### Polycast #14 (01)

### Polycast #15 (02) - Type Extension Element

### Polycast #16 (03) - Element API

### Polycast #17 (04) - Theming Elements
**::shadow and /deep/**
1. Break encapsulation (need specific `ids` to target elements)
2. Nerf potential perf. gains

### Polycast #18-19, #52 (05) - Polymer Starter Kit
[Material Palette](https://www.materialpalette.com)
[Offline Cookbook](https://jakearchibald.com/2014/offline-cookbook/)[intro to Service Worker](https://developers.google.com/web/fundamentals/getting-started/primers/service-workers)
```bash
polymer init
# choose starter-kit

polymer build # generate bundled/unbundled versions
# Bundled: gather all html files into one html file. Sharded using web components shard.
# Unbundled: seperate the source files. More bleeding edge folks.
# Vulganized html is a reduced HTML file and its dependent HTML Imports into one file


polymer serve build/bundled # run bundled version

```