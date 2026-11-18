#!/bin/bash

# কালার কোড ডিফাইন করা (হ্যাকার গ্রিন ও নিয়ন লুক)
GREEN="\033[1;32m"
CYAN="\033[1;36m"
RED="\033[1;31m"
YELLOW="\033[1;33m"
NC="\033[0m" # No Color

clear
echo -e "${GREEN}"
echo "██     ██  ██████  ██      ███████  █████  ██████  "
echo "██     ██ ██    ██ ██      ██      ██   ██ ██   ██ "
echo "██  █  ██ ██    ██ ██      █████   ███████ ██████  "
echo "██ ███ ██ ██    ██ ██      ██      ██   ██ ██   ██ "
echo " ███ ███   ██████  ███████ ██      ██   ██ ██   ██ "
echo -e "${NC}"
echo -e "${CYAN}   [WOLFARM-TOOLS] :: ADVANCED WEB CLONER V1.0${NC}"
echo -e "${YELLOW}   >>> Operated by Arman Hossen <<${NC}"
echo -e "${YELLOW}--------------------------------------------------${NC}"

# ইউজার থেকে টার্গেট ইউআরএল ইনপুট নেওয়া
echo -n -e "${GREEN}[?] Enter Target Website URL (e.g., https://example.com): ${NC}"
read target_url

# ডোমেইন এক্সট্রাক্ট করা
domain=$(echo "$target_url" | awk -F/ '{print $3}')

if [ -z "$domain" ]; then
    echo -e "${RED}[!] Invalid URL! Exiting...${NC}"
    exit 1
fi

echo -e "\n${CYAN}[*] Initializing WOLFARM secure socket...${NC}"
sleep 1
echo -e "${CYAN}[*] Fetching target: $target_url${NC}"

# ফোল্ডার তৈরি ও টাইম কাউন্ট শুরু
mkdir -p ~/wolfarm_clones/$domain
cd ~/wolfarm_clones/$domain

# সময় হিসাব করার জন্য শুরু করার সময় রেকর্ড করা
start_time=$(date +%s)

echo -e "\n${YELLOW}[!] Downloading source code & assets to mobile storage...${NC}"
wget -q -r -k -p -U "Mozilla/5.0 (Windows NT 10.0; Win64; x64)" "$target_url"

# কাজ শেষ হওয়ার সময় রেকর্ড করা
end_time=$(date +%s)
elapsed_time=$((end_time - start_time))

# স্টোরেজে সেভ করা
mkdir -p ~/storage/shared/Download/WolfarmClones
cp -r ~/wolfarm_clones/$domain ~/storage/shared/Download/WolfarmClones/

echo -e "\n=================================================="
echo -e "${GREEN}[✔] OPERATION SUCCESSFUL!${NC}"
echo -e "${GREEN}[✔] Files saved to: Download/WolfarmClones/$domain${NC}"
echo -e "${CYAN}⏱ Time taken: ${elapsed_time} seconds${NC}"
echo -e "${YELLOW}    Tool Developed & Operated by Arman Hossen   ${NC}"
echo -e "==================================================${NC}"
