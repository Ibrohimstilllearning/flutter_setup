# How to setup Flutter in Linux ubuntu

### Berikut adalah langkah - langkah setup flutter di dalam Linux Mint(Ubuntu)
> [!WARNING]
> Ini adalah penginstalan yang dikhususkan pada distro linux, anda bisa cari tutorial atau menggunakan AI apabila anda menggunakan distro selain ini. 

---
> 1. Menginstal Dependensi
Silahkan ikuti Instruksi dibawah:

```
sudo apt update
sudo apt install curl git unzip xz-utils zip libglu1-mesa -y

```
---
> 2. Download Flutter SDK

```
mkdir -p ~/development
cd ~/development

# Download versi terbaru dari https://flutter.dev/docs/get-started/install/linux
# Contoh (cek versi terbaru di situs):
wget https://storage.googleapis.com/flutter_infra_release/releases/stable/linux/flutter_linux_3.x.x-stable.tar.xz

tar xf flutter_linux_*.tar.xz

```
> Atau akses link ini apabila tidak ingin manual: [Flutter SDK](https://flutter.dev/docs/get-started/install/linux)
---
> 3. Menambah Flutter ke PATH

Edit `~/.bashrc` (atau `~/.zshrc` kalau pakai zsh):
```
nano ~/.bashrc
```
Kemudian scroll ke paling bawah dan tambahkan ini di paling bawah:
```
export PATH="$HOME/development/flutter/bin:$PATH"
```
Kemudian exit dari nano dengan `Ctrl+X` tekan `Y` kemudian `Enter`.

Reload Nano:
```
source ~/.bashrc
```
Kemudian cek dengan `flutter --version`.

---
> 4. Install JDK17 Temurin
```
sudo apt install openjdk-17-jdk -y
```
Cek
```
java -version
# harus muncul: openjdk 17 ... Temurin
```
---
> 5. Menginstal command line tools tanpa Android Studio GUI (Lebih ringan dibanding menginstal Android Studio)

Karena kamu pakai VS Code, nggak perlu install Android Studio full. Cukup command line tools aja buat SDK-nya.

```
mkdir -p ~/Android/Sdk/cmdline-tools
cd ~/Android/Sdk/cmdline-tools

# Download cmdline-tools
wget https://dl.google.com/android/repository/commandlinetools-linux-11076708_latest.zip
unzip commandlinetools-linux-*.zip

# Rename folder (wajib, flutter butuh nama persis "latest")
mv cmdline-tools latest
```
---
> 6. Tambahkan Android ke PATH
```
nano ~/.bashrc
```
Tambahkan di paling bawah:
```
export ANDROID_HOME="$HOME/Android/Sdk"
export PATH="$ANDROID_HOME/cmdline-tools/latest/bin:$PATH"
export PATH="$ANDROID_HOME/platform-tools:$PATH"
export PATH="$ANDROID_HOME/emulator:$PATH"

```
Kemudian exit dari nano dengan `Ctrl+X` tekan `Y` kemudian `Enter`.

Reload Nano:
```
source ~/.bashrc
```
---
> 7. Install SDK + Emulator via sdkmanager
```
# Accept licenses dulu
yes | sdkmanager --licenses

# Install komponen yang dibutuhkan
sdkmanager "platform-tools" \
           "platforms;android-35" \
           "build-tools;35.0.0" \
           "emulator" \
           "system-images;android-35;google_apis;x86_64"
```
Ukurannya Sekitar 1-2gb total.

---
> 8. Buat AVD (emulator)
```
avdmanager create avd \
  -n flutter_emulator \
  -k "system-images;android-35;google_apis;x86_64" \
  --device "pixel_6"
```
lalu jalankan
```
emulator -avd flutter_emulator &
```
---
> 9. Install Flutter & Dart extension di VS Code

Buka VS Code → Extensions (Ctrl+Shift+X) → cari:
Flutter (by Dart Code) → Install
Itu sudah include Dart otomatis.

---
> 10. Config Chrome

Karena saya disini menggunakan brave maka executor saya pakai brave
```
echo 'export CHROME_EXECUTABLE="/usr/bin/brave-browser"' >> ~/.bashrc
source ~/.bashrc
```
---
> 11. Linux Toolchain

Nggak perlu difix kalau kamu cuma develop Android. Error itu nggak ngeblock flutter run. Tapi kalau mau beresin tampilannya:
```
sudo apt install clang cmake ninja-build libgtk-3-dev -y
```
---
> 12. Accept Flutter licenses dan cek
```
flutter doctor --android-licenses
# ketik 'y' semua

flutter doctor
```

Idealnya semua `[✓]` kecuali bagian Xcode (itu khusus macOS, skip aja).

---

### Cara Menjalankan Emulator
> Jalankan Emulator
```
emulator -avd flutter_emulator &
```
---
> Cek Device apakah terdeteksi
```
flutter devices
```
---
> Test Run Project
```
flutter create test_app
cd test_app
flutter run
```
---

# SELESAI!!!!










