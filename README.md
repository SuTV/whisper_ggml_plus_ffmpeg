# Whisper GGML Plus FFmpeg

FFmpeg-based audio converter extension for [whisper_ggml_plus](https://pub.dev/packages/whisper_ggml_plus).

## Overview

This package provides a seamless way to handle various audio formats (MP3, MP4, AAC, etc.) by automatically converting them to the required **16kHz Mono WAV** format for the Whisper engine.

By decoupling FFmpeg from the core engine, you can now use any version of FFmpeg (full, https, etc.) in your main application without any dependency conflicts.

## Getting Started

### 1. Add dependencies

Add both the core engine and this FFmpeg extension to your `pubspec.yaml`:

```yaml
dependencies:
  whisper_ggml_plus: ^1.3.0
  whisper_ggml_plus_ffmpeg: ^1.0.0
```

### 2. Register the converter

Call `WhisperFFmpegConverter.register()` once during your application initialization (e.g., in `main()`).

```dart
import 'package:whisper_ggml_plus/whisper_ggml_plus.dart';
import 'package:whisper_ggml_plus_ffmpeg/whisper_ggml_plus_ffmpeg.dart';

void main() {
  // This connects FFmpeg to the Whisper engine
  WhisperFFmpegConverter.register();
  runApp(MyApp());
}
```

## Usage

Once registered, the `WhisperController.transcribe` method will automatically detect non-WAV files and use FFmpeg to convert them before inference.

```dart
final controller = WhisperController();

final result = await controller.transcribe(
    model: model,
    audioPath: 'recording.mp3', // Automatic conversion happens here!
);
```

## Why use this package?

1. **No Library Conflicts**: Solve the "multiple ffmpeg libraries" error in Flutter by choosing your own FFmpeg version.
2. **Boilerplate Free**: No need to manually write FFmpeg commands and session handlers.
3. **Lightweight Core**: Keep your app small if you already have pre-processed 16kHz WAV files.

## License

MIT License
