# ntrip_ros
NTRIP client, imports RTCM streams to ROS topic

This was forked from github.com/tilk/ntrip_ros

The CORS correction server that I am using does not have the /n/r characters. So I parsed out individual messages and published each one on the /rtcm ROS topic.
It would crash with IncompleteRead error. I added patch at top of file.
But the connection had closed and it would crash again. I ended up detecting zero length data and closing and reopening the data stream.
It continues on without a glitch.

You can generate the require $GPGGA message at this site. https://www.nmeagen.org/ Set a point near where you want to run and click "Generate NMEA file". Cut and paste the $GPGGA message into the launch file.

I intend to use it with https://github.com/ros-agriculture/ublox_f9p

It may also require this package: https://github.com/tilk/rtcm_msgs

A similar NTRIP client (may be better than mine) is here: https://github.com/dayjaby/ntrip_ros

# How to setup Septentrio GPS as a base station
- Log into the web broweser settings page (just enter the ip address in a browser)
- GNSS > Position - change from Rover to Static

![static or rover](https://user-images.githubusercontent.com/6209386/170068329-66113e18-df13-4a15-a042-93108ccd9f65.jpg)

- Communication > NTRIP Caster - New mount point - edit mount point

![edit mount point](https://user-images.githubusercontent.com/6209386/170068612-e29bff70-60b6-4d7b-9d65-44a91da57a06.jpg)

- In edit mount point click Configure Output - Change Enable Local Server to On

- Corrections > Corrections Output - Click New RTCM3 output - NTRIP server - NTR2: NTRIP to lcas|Internal caster (lcas = name of mount point)

- Corrections > NTRIP - New NTRIP server

![new ntrip server](https://user-images.githubusercontent.com/6209386/170069278-21925b84-35a1-4cc5-a570-5dce2eb38b5f.jpg)




