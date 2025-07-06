# --- Script PowerShell untuk mengunduh cloudflared-windows-386.exe ---

# URL file yang akan diunduh
$DOWNLOAD_URL = "https://github.com/cloudflare/cloudflared/releases/download/2025.7.0/cloudflared-windows-386.exe"

# Nama file output yang akan disimpan
$OUTPUT_FILENAME = "cloudflared-windows-386.exe"

Write-Host "`nSedang mengunduh $($OUTPUT_FILENAME) dari:`n$($DOWNLOAD_URL)`n"

# Gunakan Invoke-WebRequest (alias 'curl' di PowerShell) untuk mengunduh file
# -Uri: URL sumber
# -OutFile: Path dan nama file tujuan
# -UseBasicParsing: Direkomendasikan untuk Invoke-WebRequest agar lebih konsisten
#                  dan menghindari error parser HTML pada beberapa kasus.
try {
    Invoke-WebRequest -Uri $DOWNLOAD_URL -OutFile $OUTPUT_FILENAME -UseBasicParsing -ErrorAction Stop
    
    # Pengecekan tambahan: pastikan file benar-benar ada setelah diunduh
    if (Test-Path $OUTPUT_FILENAME) {
        Write-Host "`n=========================================================================" -ForegroundColor Green
        Write-Host "$($OUTPUT_FILENAME) BERHASIL diunduh!" -ForegroundColor Green
        Write-Host "File tersimpan di: $(Get-Location)" -ForegroundColor Green
        Write-Host "=========================================================================" -ForegroundColor Green
    } else {
        throw "File tidak ditemukan setelah proses unduh selesai."
    }

} catch {
    Write-Host "`n=========================================================================" -ForegroundColor Red
    Write-Host "GAGAL mengunduh $($OUTPUT_FILENAME)." -ForegroundColor Red
    Write-Host "Error: $($_.Exception.Message)" -ForegroundColor Red
    Write-Host "Pastikan: " -ForegroundColor Red
    Write-Host "1. Ada koneksi internet." -ForegroundColor Red
    Write-Host "2. URL unduhan ($($DOWNLOAD_URL)) masih valid dan tidak berubah." -ForegroundColor Red
    Write-Host "=========================================================================" -ForegroundColor Red
}

Write-Host "`nTekan Enter untuk melanjutkan..."
$null = Read-Host
