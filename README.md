name: Android APK Build

on:
  push:
    branches:
      - main
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: İş kurulumu
        uses: actions/checkout@v3

      - name: Ödeme deposu
        run: echo "Depo başarıyla klonlandı."

      - name: Projeyi aç
        run: unzip kaptan_app_project_v3.zip -d kaptan_app_project

      - name: JDK Kurulumu
        uses: actions/setup-java@v3
        with:
          distribution: 'temurin'
          java-version: '17'

      - name: APK oluştur
        run: |
          cd kaptan_app_project
          chmod +x ./gradlew
          ./gradlew assembleDebug

      - name: APK’yı yükle
        uses: actions/upload-artifact@v3
        with:
          name: Jarvis-App
          path: kaptan_app_project/app/build/outputs/apk/debug/app-debug.apk

      - name: Kurulum Sonrası JDK
        run: echo "JDK işlemleri tamamlandı."

      - name: İşi tamamla
        run: echo "✅ Jarvis APK başarıyla oluşturuldu!"
