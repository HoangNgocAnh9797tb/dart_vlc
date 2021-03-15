# dart_vlc

 [WIP] Bringing power of :film_strip: VLC to Flutter & Dart apps on Windows & Linux (presently).

<table>
<tr>
  <td>
    <img src="https://github.com/alexmercerind/dart_vlc/blob/assets/dart_vlc_0.PNG?raw=true"></img>
  </td>
  <td>
    <img src="https://github.com/alexmercerind/dart_vlc/blob/assets/dart_vlc_1.PNG?raw=true"></img>
  </td>
</tr>
</table>

## :: Installation

```yaml
dependencies:
  ...
  dart_vlc: ^0.0.1
```

## :book: Documentation

Create a new `Player` instance.
```dart
Player player = await Player.create(id: 69420);
```

Create a single `Media`.
```dart
Media media0 = Media.file(
  new File('C:/music.mp3')
);

Media media1 = Media.network(
  'https://alexmercerind.github.io/music.aac'
);

Media media2 = await Media.asset(
  'assets/music.ogg'
);
```

Open `Media` or `Playlist` into a `Player` instance.
```dart
player.open(
  new Playlist(
    medias: [
      Media.file(new File('C:/music0.mp3')),
      Media.file(new File('C:/music1.mp3')),
      Media.file(new File('C:/music2.mp3')),
    ],
  ),
  autoStart: true, //default
);
```

Create a list of `Media`s using `Playlist`.
```dart
Playlist playlist = new Playlist(
  medias: [
    Media.file(new File('C:/music.mp3')),
    await Media.asset('assets/music.ogg'),
    Media.network('https://alexmercerind.github.io/music.aac'),
  ],
);
```

Control playback.
```dart
player.play();
player.seek(Duration(seconds: 30));
player.pause();
player.playOrPause();
player.stop();
```

Set playback volume & rate.
```dart
player.setVolume(0.5);

player.setRate(1.25);
```

Listen to playback events.

(Same can be retrieved directly from `Player` instance without having to rely on stream).

```dart
player.currentStream.listen((CurrentState state) {
  // state.index;
  // state.media;
  // state.medias;
  // state.isPlaylist;
});
```

```dart
player.positionStream.listen((PositionState state) {
  // state.position;
  // state.duration;
});
```

```dart
player.playbackStream.listen((PlaybackState state) {
  // state.isPlaying;
  // state.isSeekable;
  // state.isCompleted;
});
```

```dart
player.generalStream.listen((GeneralState state) {
  // state.volume;
  // state.rate;
});
```

## :pushpin: Progress

:white_check_mark: Done

- `Media` playback from file.
- `Media` playback from network.
- `Media` playback from assets.
- `play`/`pause`/`playOrPause`/`stop`.
- Multiple `Player` instances.
- `Playlist`.
- `next`/`back`/`jump` for playlists.
- `setVolume`.
- `setRate`.
- `seek`.
- Events.
- Automatic fetching of headers, libs & shared libraries.
- Changing VLC version from CMake.
- Event streams.
  - `Player.currentState`
    - `index`: Index of current media in `Playlist`.
    - `medias`: List of all opened `Media`s.
    - `media`: Currently playing `Media`.
    - `isPlaylist`: Whether a single `Media` is loaded or a `Playlist`.
  - `Player.positionState`
    - `position`: Position of currently playing media in `Duration`.
    - `duration`: Position of currently playing media in `Duration`.
  - `Player.playbackState`
    - `isPlaying`.
    - `isSeekable`.
    - `isCompleted`.
  - `Player.generalState`
    - `volume`: Volume of current `Player` instance.
    - `rate`: Rate of current `Player` instance.

:negative_squared_cross_mark: Under progress (irrespective of order)...

- Device enumeration.
- `add`/`insert` `Media` to `Playlist` during playback.
- Retrieving metadata of a file.
- FFI version of the library for plain Dart applications.
- Linux version.
- Embeding video inside the Flutter window.
- Supporting live streaming links.
- Bringing project on other platforms like Android/iOS.
- Supporting native volume control/lock screen notifications.

## :blue_heart: Support

Consider supporting the project by either/and:
- Starring the repository, to get this hardwork noticed.
- Buying me a coffee.

<a href="https://www.buymeacoffee.com/alexmercerind"><img src="https://img.buymeacoffee.com/button-api/?text=Buy me a coffee&emoji=&slug=alexmercerind&button_colour=FFDD00&font_colour=000000&font_family=Cookie&outline_colour=000000&coffee_colour=ffffff"></a>

## :sparkles: Contributions

The code in the project is very nicely arranged, I have added comments wherever I felt necessary.

Contributions to the project are open, it will be appreciated if you discuss the bug-fix/feature-addition in the issues first.

## :page_facing_up: License

Copyright (C) 2021, Hitesh Kumar Saini.

This library & work under this repository is licensed under GNU Lesser General Public License v2.1.

## :scroll: Acknowledgements

Thanks to [@DomingoMG](https://github.com/DomingoMG) for the donation & testing of the project.

## :eyes: Spoilers

Currenty video playback is also supported out of the box, but it doesnt show inside Flutter window.


<img src="https://github.com/alexmercerind/dart_vlc/blob/assets/dart_vlc_2.PNG?raw=true"></img>

## :safety_pin: Vision

There aren't any media (audio or video) playback libraries for Flutter on Windows/Linux yet. So, this project is all about that.
As one might be already aware, VLC is one of the best media playback tools out there.

So, now you can use it to play audio or video [WIP] files from Flutter Desktop app.

The API style of this project is highly influenced by [assets_audio_player](https://github.com/florent37/Flutter-AssetsAudioPlayer) due to its completeness. This project will serve as a base to add Windows & Linux support to already existing audio playback libraries like [just_audio](https://github.com/ryanheise/just_audio) and [assets_audio_player](https://github.com/florent37/Flutter-AssetsAudioPlayer).

Although, the mentioned repositories above are for audio playback, video playback is also a part of consideration for this project.

Thanks to the [VideoLAN](https://www.videolan.org) team for creating [libVLC](https://github.com/videolan/vlc) & [libVLC++](https://github.com/videolan/libvlcpp).