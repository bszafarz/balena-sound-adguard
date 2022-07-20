# balena sound & adguard



## Deployment

I have deployed this project using balena-cli

1. Change working directory to root of the repo (cd balena-sound-adguard)
2. Check name of fleet to which you will push code

``❯ balena fleets``

``ID      NAME          SLUG                          DEVICE TYPE  ONLINE DEVICES DEVICE COUNT``

``1950375 adguard-sound szafarz_bartosz/adguard-sound raspberrypi3 1              1``

3. Run push command and give balena some time to build release and deploy it on your fleet's devices

``❯ balena push adguard-sound``

4. I have done some customisation using device variables as shown below
   ![](Screenshot%20from%202022-07-19%2022.37.34.png "Device variables")
   
   Here is an overwiew of each property
   | Property                   | Target service    | Value         | Comment                                                                       |
   |----------------------------|-------------------|---------------|-------------------------------------------------------------------------------|
   | BLUETOOTH_DEVICE_NAME      | bluetooth         | Yamaha AS-301 | Name of device brodcasted via Bluetooth                                       |
   | SOUND_DEVICE_NAME          | spotify           | Yamaha AS-301 | Name of device brodcasted via Spotify-connect                                 |
   | SOUND_DEVICE_NAME          | airplay           | Yamaha AS-301 | Name of device brodcasted via Airplay                                         |
   | SOUND_MODE                 | sound-supervisor  | STANDALONE    | Mode of multiroom feature (1)                                                 |
   | SOUND_SPOTIFY_BITRATE      | spotify           | 320           | Default bitrate used by app (2)                                               |
   | SOUND_SPOTIFY_ENABLE_CACHE | spotify           | true          | Any value enable the cache so I've choosed "true" for readability             |
   | SOUND_SUPERVISOR_PORT      | All services      | 8080          | By default supervisor use port 80 however that port was needed for AdGuard    |
   | SOUND_VOLUME               | sound-supervisor	| 100           | Override of default 75 (3)                                                    |
   | TZ                         | adguard           | Europe/Warsaw | Polish time zone for AdGuard                                                  |
   
   1  I use single device hence the multiroom server and client services were excluded from code - if needed simply add it from balena-sound repo
   
   2  According to some documentation I've read some time ago, the 320 is the highest value supported by spotify
   
   3  Not sure if it works but it is worth of try