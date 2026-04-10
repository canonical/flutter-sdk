# Flutter SDK for Workshop

A development environment for Flutter and Dart projects. It provides the
Flutter framework, the Dart SDK, and system dependencies for Linux desktop
development. The pub package cache is persisted on the host to speed up
dependency resolution across workshop updates.

---

## Reference workshop

A minimal workshop:

```yaml
# workshop.yaml
name: flutter-app
base: ubuntu@24.04
sdks:
  - name: flutter
    channel: latest/stable

actions:
  build: |
    cd my_app && flutter build linux
  run: |
    cd my_app && flutter run -d linux
  test: |
    cd my_app && flutter test
```

This demonstrates a basic Flutter workflow for Linux desktop apps with
persistent package caching.

---

## Using the SDK

### Prerequisites, project layout

1. No prerequisite SDKs are required.
2. Your Flutter project (with a `pubspec.yaml` file) should be in your
   project directory, or you can create one with `flutter create`.
3. On launch, the SDK configures `PATH` for both Flutter and Dart, installs
   Linux desktop build dependencies (clang, cmake, ninja, GTK), and runs
   `flutter precache` to download platform artifacts.

### Create and build a project

Once the workshop is ready:

```bash
workshop shell
flutter create --platforms=linux my_app
cd my_app
flutter build linux
```

The release binary is at
`my_app/build/linux/x64/release/bundle/my_app`.

### Run the app

```bash
workshop shell
cd my_app
flutter run -d linux
```

This launches the app on the Linux desktop. A display server (X11 or Wayland)
must be available—the SDK ships with the `desktop` plug for this purpose.

### Run tests

From within the workshop shell:

```bash
workshop shell
cd my_app
flutter test
```

### Verify from the command line

```bash
workshop shell
flutter --version
dart --version
flutter doctor -v
```

### Pub cache

Downloaded packages are stored in `~/.pub-cache`, which is mapped to the host
via the `pub-cache` mount plug. Subsequent builds reuse cached packages.

To see where the pub cache is stored on the host:

```bash
workshop info
```

---

## Plugs (resources this SDK consumes)

### `pub-cache`

- Interface: `mount`
- Workshop target: `/home/workshop/.pub-cache`
- Purpose: Persists Dart/Flutter package downloads between workshop updates.

## Slots (resources this SDK provides)

This SDK doesn't define any slots.

---

## Documentation and guidance

- [Flutter documentation](https://docs.flutter.dev/)
- [Dart documentation](https://dart.dev/guides)
- [Flutter Linux desktop](https://docs.flutter.dev/platform-integration/linux/building)
- [Workshop documentation](https://canonical-workshop.readthedocs-hosted.com/latest/)

---

## Community and support

- Flutter community: [Flutter Community](https://flutter.dev/community)
- Workshop forum:
  [Workshop Discourse](https://discourse.canonical.com/c/engineering/sdk/34)
- Please review our
  [Code of Conduct](https://ubuntu.com/community/ethos/code-of-conduct) before
  participating.

---

## Contributions

All contributions, including code, documentation updates, and issue reports,
are welcome!

- See `CONTRIBUTING.md` for guidelines.
- Open issues or pull requests on the official repository.

---

## License and copyright

Copyright 2025 Canonical Ltd.

This program is free software: you can redistribute it and/or modify it under
the terms of the
[GNU Lesser General Public License version 2.1 (LGPLv2.1)](https://www.gnu.org/licenses/old-licenses/lgpl-2.1.html)
as published by the Free Software Foundation.

This program is distributed in the hope that it will be useful, but WITHOUT ANY
WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE. See the GNU Lesser General Public License for more details.
