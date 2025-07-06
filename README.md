@echo off
REM --- Script untuk mengunduh cloudflared-windows-386.exe ---

REM URL file yang akan diunduh
REM URL ini adalah untuk versi cloudflared 2025.7.0 khusus 386-bit Windows.
SET "DOWNLOAD_URL=https://github.com/cloudflare/cloudflared/releases/download/2025.7.0/cloudflared-windows-386.exe"

REM Nama file yang akan disimpan di komputer kamu
SET "OUTPUT_FILENAME=cloudflared-windows-386.exe"

echo.
echo Sedang mengunduh "%OUTPUT_FILENAME%" dari:
echo %DOWNLOAD_URL%
echo.

REM Menggunakan curl untuk mengunduh file
REM -L : Penting! Ini mengikuti redirect. Link GitHub Releases seringkali adalah redirect.
REM -O (huruf kapital O): Menyimpan file dengan nama yang sama seperti yang ada di URL remote.
curl -L -O %DOWNLOAD_URL%

REM --- Pengecekan Hasil Unduhan ---
IF %ERRORLEVEL% NEQ 0 (
    echo.
    echo =========================================================================
    echo GAGAL mengunduh "%OUTPUT_FILENAME%".
    echo Pesan error dari Curl mungkin terlihat di atas.
    echo Pastikan:
    echo 1. Ada koneksi internet.
    echo 2. URL unduhan (%DOWNLOAD_URL%) masih valid dan tidak berubah.
    echo =========================================================================
) ELSE (
    echo.
    echo =========================================================================
    echo "%OUTPUT_FILENAME%" BERHASIL diunduh!
    echo File tersimpan di direktori saat ini: %CD%
    echo =========================================================================
)

echo.
pause
