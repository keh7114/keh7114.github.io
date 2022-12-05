# keh7114.github.io

Project 3 - Cloud VPN Docker Project 
CYB-3353-01
Karlie Hanson

Source used for Wireguard Setup:
https://thematrix.dev/setup-wireguard-vpn-server-with-docker/

Installing Wireguard:

After creating a new droplet in DigitalOcean with the preferred settings, open the console to begin the Wireguard installation process.

First, create the Wireguard directory by using the command mkdir -p ~/wireguard/

Next, create a subdirectory in the wireguard directory by using mkdir -p ~/wireguard/config/

Now install docker-compose with the command sudo apt install docker-compose

Then, nano into the docker-compose.yml file by typing nano ~/wireguard/docker-compose.yml

now we can copy and paste this portion of code into the docker-compose.yml file:

version: '3.8'
services:
  wireguard:
    container_name: wireguard
    image: linuxserver/wireguard
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/Chicago
      - SERVERURL=143.198.50.203
      - SERVERPORT=51820
      - PEERS=pc1,pc2,phone1
      - PEERDNS=auto
      - INTERNAL_SUBNET=10.0.0.0
    ports:
      - 51820:51820/udp
    volumes:
      - type: bind
        source: ./config/
        target: /config/
      - type: bind
        source: /lib/modules
        target: /lib/modules
    restart: always
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    sysctls:
      - net.ipv4.conf.all.src_valid_mark=1
      
  Make sure to update TZ to reflect your current timezone as well as update the serverURL to your droplet's public IP address.
      
   Finally press control + X + Y to save the file and press enter to exit
      
   Now, we enter into wireguard by using the command cd ~/wireguard/
      
   To view the QR codes, use the command docker-compose logs -f wireguard
      
   Download the WireGuard app on your phone and use the QR code scanner to scan one of the QR codes
      
   Activate the VPN on the app in order to turn it on
      
   To test the VPN on your personal computer:
      
   Begin by using the command cd wireguard
      
   Next cd into the config file by using cd config
      
   Lastly, enter into the peer_pc1/ file by using the command cd peer_pc1/
      
   Once you are into those files you can use cat peer_pc1.conf
      
   After all of the information is done being printed, copy and paste it into your preferred text editor and save the file with the name of your          choice ending in .conf
      
   Place that new .conf file into Wireguard and your VPN is complete all you need to do is activate it
      
   To test that your VPN works on both your phone and computer, visit IPLeak.com in your web browser.
      
   
![IMG_3352](https://user-images.githubusercontent.com/60195646/205529630-77159964-a935-4b65-b8a4-160c3b087882.jpeg)
![IMG_3351](https://user-![IMG_3355](https://user-images.githubusercontent.com/60195646/205529640-14733f6e-c0b7-4934-b9d1-ca8aaa8c7f2f.jpeg)
images.githubusercontent.com/60195646/205529636-24c6c88e-1179-4e1f-a9cf-9af2a14c17b3.jpeg)
![IMG_3350](https://user-images.githubusercontent.com/60195646/205529643-f0c85351-69f7-40f8-a189-ffa28c826866.jpeg)
<img width="872" alt="Screen Shot 2022-12-04 at 7 23 16 PM" src="https://user-images.githubusercontent.com/60195646/205529646-383f46b8-c491-4cf1-a36a-70858e213bdb.png">
