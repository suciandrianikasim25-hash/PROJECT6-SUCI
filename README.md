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
