# PROJECT6-SUCI
# TUGAS 1 BASIC RECOVERY
# SCRIPT 1 - MEMBUAT SIMULASI DRIVE D
# Isi script
~~~
@echo off
title SETUP SIMULASI DATA RECOVERY
echo ===========================================
echo         MEMBUAT SIMULASI DRIVE D
echo ===========================================
echo.

:: Lokasi di Desktop
set base=C:\Users\asus\Desktop\SimulasiDrive_D

:: Membuat folder utama SimulasiDrive_D
echo Membuat folder utama SimulasiDrive_D...
mkdir "%base%" >nul 2>&1

echo Membuat struktur folder dan file...
echo.

for /l %%i in (1,1,10) do (

    echo Membuat Folder_%%i ...
    mkdir "%base%\Folder_%%i\SubFolder_A"
    mkdir "%base%\Folder_%%i\SubFolder_B"
    mkdir "%base%\Folder_%%i\SubFolder_C"

    :: ========== SUBFOLDER A ==========
    echo PDF dummy file > "%base%\Folder_%%i\SubFolder_A\dokumen_%%i_A.pdf"
    echo CSV dummy file > "%base%\Folder_%%i\SubFolder_A\data_%%i_A.csv"
    echo TXT dummy file > "%base%\Folder_%%i\SubFolder_A\catatan_%%i_A.txt"
    echo DOCX dummy file > "%base%\Folder_%%i\SubFolder_A\laporan_%%i_A.docx"
    echo BAT dummy file > "%base%\Folder_%%i\SubFolder_A\aplikasi_%%i_A.bat"

    :: ========== SUBFOLDER B ==========
    echo file B1 > "%base%\Folder_%%i\SubFolder_B\file_b1_%%i.txt"
    echo file B2 > "%base%\Folder_%%i\SubFolder_B\file_b2_%%i.csv"
    echo file B3 > "%base%\Folder_%%i\SubFolder_B\file_b3_%%i.docx"
    echo file B4 > "%base%\Folder_%%i\SubFolder_B\file_b4_%%i.py"
    echo file B5 > "%base%\Folder_%%i\SubFolder_B\file_b5_%%i.jpg"

    :: ========== SUBFOLDER C ==========
    echo file C1 > "%base%\Folder_%%i\SubFolder_C\file_c1_%%i.txt"
    echo file C2 > "%base%\Folder_%%i\SubFolder_C\file_c2_%%i.ini"
    echo file C3 > "%base%\Folder_%%i\SubFolder_C\file_c3_%%i.pdf"
    echo file C4 > "%base%\Folder_%%i\SubFolder_C\file_c4_%%i.xml"
    echo file C5 > "%base%\Folder_%%i\SubFolder_C\file_c5_%%i.csv"
    echo file C6 > "%base%\Folder_%%i\SubFolder_C\file_c6_%%i.py"

    :: ========== FILE LUAR SUBFOLDER ==========
    echo database dummy file > "%base%\Folder_%%i\database_%%i.db"
    echo config dummy file > "%base%\Folder_%%i\config_%%i.ini"
)

echo.
echo ===========================================
echo       SETUP SELESAI ! DATA DIBUAT
echo ===========================================
echo Lihat di C:\Users\asus\Desktop\SimulasiDrive_D
echo.
pause
~~~
# SCRIPT 2 - PROCESS RECOVERY DATA
# Isi script 
~~~
@echo off
echo ===============================================
echo               PROCESS RECOVERY DATA
echo ===============================================
echo.

:: Lokasi sumber (folder simulasi drive D)
set sumber=C:\Users\asus\Desktop\SimulasiDrive_D

:: Lokasi tujuan (folder simulasi drive C)
set root=C:\Users\asus\Desktop\SimulasiDrive_C

:: Membuat folder utama SimulasiDrive_C jika belum ada
if not exist "%root%" mkdir "%root%"

:: Format tanggal dan waktu
set yr=%date:~10,4%
set mo=%date:~4,2%
set dy=%date:~7,2%
set hr=%time:~0,2%
set mn=%time:~3,2%

:: Hilangkan spasi pada jam
set hr=%hr: =0%

set tujuan=%root%\DataRecovery_%yr%%mo%%dy%_%hr%%mn%

:: Lokasi file log
set logfile=%root%\recovery_log.txt

:: Buat folder tujuan recovery
mkdir "%tujuan%" >nul 2>&1

echo Menyalin file dari:
echo %sumber%
echo ke:
echo %tujuan%
echo.

echo Membuat file log...
echo RECOVERY LOG > "%logfile%"
echo Tanggal: %date%  Waktu: %time% >> "%logfile%"
echo Sumber: %sumber% >> "%logfile%"
echo Tujuan: %tujuan% >> "%logfile%"
echo ---------------------------------------- >> "%logfile%"

:: SALIN ISI FOLDER (PERBAIKAN UTAMA)
xcopy "%sumber%\*" "%tujuan%\" /E /H /C /I /Y >> "%logfile%"

echo ---------------------------------------- >> "%logfile%"
echo Recovery selesai >> "%logfile%"

echo.
echo ===============================================
echo            RECOVERY SELESAI !!!
echo ===============================================
echo Log File: %logfile%
echo.

pause
~~~
# TUGAS 2 MODIFIKASI SCRIPT
# Isi script
~~~
@echo off

setlocal enabledelayedexpansion
echo ===============================================
echo               PROCESS RECOVERY DATA
echo ===============================================
echo.

:: Lokasi sumber (folder simulasi drive D)
set sumber=C:\Users\asus\Desktop\SimulasiDrive_D

:: Lokasi tujuan (folder simulasi drive C)
set root=C:\Users\asus\Desktop

:: Membuat folder utama SimulasiDrive_C jika belum ada
if not exist "%root%" mkdir "%root%"

:: Format tanggal dan waktu
set yr=%date:~10,4%
set mo=%date:~4,2%
set dy=%date:~7,2%
set hr=%time:~0,2%
set mn=%time:~3,2%

:: Hilangkan spasi pada jam
set hr=%hr: =0%

set tujuan=%root%\DataRecovery_%yr%%mo%%dy%_%hr%%mn%
mkdir "%tujuan%"

echo Folder Recovery: %tujuan%
echo. 

:: Hitung Jumlah File PDF dan DOCX
set count=0
for /r "%sumber%" %%f in (*.pdf *.docx) do (
set /a count+=1
)

echo total file ditemukan: %count%
echo.

:: Proses Recovery
set num=0
for /r "%sumber%" %%f in (*.pdf *.docx) do (
set /a num+=1
echo [!num!/%count%] Menyalin: %%~nxf

:: Buat folder tujuan sama persis dengan sumber
set "rel=%%~dpf"
set "rel=!rel:%sumber%=!"
if not exist "%tujuan%!rel!" mkdir "%tujuan%!rel!"

:: Salin file
xcopy "%%f" "%tujuan%!rel!" >nul 2>&1

:: Verifikasi ukuran file
for %%A in ("%%f") do set size1=%%~zA
for %%B in ("%tujuan%!rel!%%~nxf") do set size2=%%~zB

if "!size1!"=="!size2!" (
	echo Verifikasi: OK
  ) else (
	echo Verifikasi: Gagal
  )
)

echo.
echo Membuat File ZIP...
set zipfile=%root%\DataRecovery_%yr%%mo%%dy%_%hr%%mn%.zip
echo Membuat zip: %zipfile%

:: ZIP PAKAI POWERSHELL (built-in Windows)
powershell -command "Compress-Archive -Path '%tujuan%\*' -DestinationPath '%zipfile%'"

echo.
echo ===============================================
echo            TUGAS 2 SELESAI !!!
echo ===============================================
echo hasil ZIP: %zipfile%.zip
echo.
pause
~~~
# TUGAS 3 SKENARIO ADVANCED
# Isi script
~~~
@echo off
title ADVANCED DATA RECOVERY SYSTEM
color 0B

set BASE=%USERPROFILE%\Desktop
set SOURCE=%BASE%\SimulasiDrive_D
set DEST_BASE=%BASE%\SimulasiDrive_C

:MENU
cls
echo ==========================================================
echo                ADVANCED DATA RECOVERY SYSTEM
echo ==========================================================
echo Source Folder: %SOURCE%
echo Destination:   %DEST_BASE%
echo ==========================================================
echo  1. Selective Backup (Pilih Folder)
echo  2. Incremental Backup (Hanya file baru/berubah)
echo  3. Scheduled Backup (Backup tiap X menit)
echo  4. Email Notification (Notifikasi Gmail)
echo  5. Exit
echo ==========================================================
set /p opc=Masukkan pilihan (1-5): 

if %opc%==1 goto SELECTIVE
if %opc%==2 goto INCREMENTAL
if %opc%==3 goto SCHEDULE
if %opc%==4 goto EMAIL
if %opc%==5 exit
goto MENU


:SELECTIVE
cls
echo ---- SELECTIVE BACKUP ----
echo Folder tersedia:
dir "%SOURCE%" /b
echo.
set /p FOLDER=Ketik nama folder yang ingin di-backup: 

set DEST=%DEST_BASE%\Selective_%FOLDER%_%date:~-4%%date:~4,2%%date:~7,2%_%time:~0,2%%time:~3,2%
mkdir "%DEST%"

xcopy "%SOURCE%\%FOLDER%" "%DEST%" /E /H /C /I /Y

echo SELESAI! Backup selective tersimpan di:
echo %DEST%
pause
goto MENU


:INCREMENTAL
cls
echo ---- INCREMENTAL BACKUP ----
set DEST=%DEST_BASE%\IncrementalBackup
mkdir "%DEST%"

robocopy "%SOURCE%" "%DEST%" /E /XO /LOG:%DEST%\incremental_log.txt

echo SELESAI! Incremental backup berjalan.
pause
goto MENU


:SCHEDULE
cls
echo ---- SCHEDULED BACKUP ----
set /p interval=Backup berulang setiap berapa menit?: 
echo Jalankan CTRL + C untuk menghentikan proses.
timeout 3 > nul

:LOOP
set TS=%date:~-4%%date:~4,2%%date:~7,2%_%time:~0,2%%time:~3,2%
set DEST=%DEST_BASE%\Schedule_%TS%
mkdir "%DEST%"
xcopy "%SOURCE%" "%DEST%" /E /H /C /I /Y

echo ----- Backup dilakukan pada %TS% -----
timeout %interval% * 60 > nul
goto LOOP


:EMAIL
cls
echo ---- EMAIL NOTIFICATION ----
set /p email=Masukkan email Gmail tujuan: 
set /p pesan=Tulis pesan singkat notifikasi: 

C:\Program Files\PowerShell\7\pwsh.exe-Command "Send-MailMessage -To '%email%' -From '%email%' -Subject 'Backup Selesai' -Body '%pesan%' -SmtpServer 'smtp.gmail.com' -Port 587 -UseSsl -Credential (New-Object System.Management.Automation.PSCredential('%email%', (Read-Host 'Password email Gmail' -AsSecureString)))"

echo Email notifikasi dikirim sukses!
pause
goto MENU
~~~
