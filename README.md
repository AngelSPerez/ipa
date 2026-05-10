## Guía completa: Instalar IPA en iPhone desde Fedora Linux

### 1️⃣ Instalar dependencias
```bash
sudo dnf install -y libimobiledevice usbmuxd ldc dub clang openssl-devel git
```

### 2️⃣ Descargar AltServer
```bash
cd ~/Downloads && \
wget https://github.com/NyaMisty/AltServer-Linux/releases/download/v0.0.5/AltServer-i586 -O AltServer && \
chmod +x ./AltServer
```

### 3️⃣ Obtener UDID del iPhone
```bash
idevice_id -l
```

### 4️⃣ Compilar Anisette Server
```bash
cd ~/Downloads && \
git clone https://github.com/Dadoum/anisette-v3-server.git && \
cd anisette-v3-server && \
DC=ldc2 dub build --build-mode allAtOnce -b release --compiler=ldc2
```

### 5️⃣ Correr Anisette Server
```bash
cd ~/Downloads/anisette-v3-server && ./anisette-v3-server &
```
Espera hasta ver **"Listening for requests on http://0.0.0.0:6969/"**

### 6️⃣ Instalar IPA
```bash
cd ~/Downloads && \
ALTSERVER_ANISETTE_SERVER=http://127.0.0.1:6969 ./AltServer -u TU_UDID -a tu@apple.com -p tuContraseña tuapp.ipa
```

### 7️⃣ Confiar en el iPhone
**Ajustes → General → VPN y gestión del dispositivo → Tu Apple ID → Confiar**

### 8️⃣ Activar modo desarrollador
**Ajustes → Privacidad y seguridad → Modo desarrollador → Activar**

---

### ⚠️ Notas importantes
- El paso 4 solo se hace **una vez**
- El paso 5 debe hacerse **cada vez** que reinicies la PC antes de instalar
- Si tienes verificación en dos pasos AltServer te pedirá el código directamente
- El IPA debe compilarse en **release** con `flutter build ipa --release --no-codesign`
