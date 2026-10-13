### compile cmd
* AB4
b 1 -DCONFIG_SECURE_PLATFORM_DEVELOPMENT=1 -DBUILD_PRODUCT_ID=AB4
b.bat 1 -DBUILD_PRODUCT_ID=AB4 to build for test environment with cybersecurity enabled using virtual efuse, WiFi enabled
* SHE
b.bat 2 -DCONFIG_SECURE_PLATFORM_DEVELOPMENT=1 -DBUILD_PRODUCT_ID=SHE
* Thunderstorm
b 1 -DBUILD_PRODUCT_ID=TVF (not support cyber security)
b 2 -DCONFIG_SECURE_PLATFORM_DEVELOPMENT=1 -DBUILD_PRODUCT_ID=TVF
b 2 -DCONFIG_SECURE_PLATFORM_PRODUCTION=1 -DBUILD_PRODUCT_ID=TVF
* Product ID
  AB2: NRX Bridge
  AB4: MPS Bridge
  MC4: Recon mobile cooling
  TVF: Thunderstorm

* IDF
 idf.py reconfigure

### Dev flash cmd
esptool --chip esp32s3 --port=COM6 --baud=921600 --before=default_reset --after=no_reset write_flash --flash_mode dio --flash_freq 40m --flash_size keep --force --no-compress --encrypt 0 .\bin\AB4_v1.0.0-rc.3-full.bin

esptool --chip esp32 --port=COM8 --baud=921600 --before=default_reset --after=no_reset write_flash --flash_mode dio --flash_freq 40m --flash_size keep --force --no-compress --encrypt 0 .\bin\SHE_v2.2.2-full.bin

### Dev erase cmd
* esptool --chip esp32 --port=COM8 --baud=921600 --before=default_reset --after=no_reset erase_flash --force

* other
HMI 2.0
flash vendor:
20h : N/A
flash devID:
4017h
QUAD;64Mbit
crystal:
40 Mhz

### Monitor cmd
log保存到文件，不异常退出
set PYTHONIOENCODING=utf-8:replace & idf.py -p COM43 monitor --disable-auto-color 2>&1 >> "C:\Users\test\Desktop\F_log\2.txt"

### 标准格式化文件
clang-format -i ./lib/v2/*.c ./lib/v2/*.h
clang-format -style=file -i ./DICMApplication/AB2/source/nmea2k_service/source/nmea2k_service.c
clang-format -style=file -i ./DICMFramework\DICMCore/DICMConnectors/source/nmea2k/lib/common/nmea_pgn_n2k.c
 
# 永久生效（zsh，Mac 默认）
echo "export IDF_PATH=~/esp/esp-idf" >> ~/.zshrc
echo "alias get_idf='. \$IDF_PATH/export.sh'" >> ~/.zshrc
source ~/.zshrc

### 20260818
* Secure boot Dev board can't erase
* 