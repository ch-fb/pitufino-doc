# NMEA0183 $PPITA Sentence for Autopilot Status

Pitufino’s firmware version V1.5.3 introduced the (proprietary) NMEA0183 sentence $PPITA to transmit autopilot status (mode, locked heading and locked wind angle). This sentence can be used (ideally together with the standard sentences $HDG for compass heading and $RSA for rudder angle) to implement an autopilot display. Note, this sentence is **not** meant for controlling an autopilot.


## Sentence format

    $PPITA,a,x.x,a,x.x*hh<CR><LF>
           |  |  |  |
           |  |  |  |_locked wind angle in degrees [0-360)
           |  |  |_M (magnetic) or T (true)
           |  |_locked heading in degrees [0-360)
           |_pilot mode:
             S (STBY)
             A (AUTO)
             W (WIND)
             N (NAV)
             U (Unknown or OFF)

## Examples (without checksum)

    $PPITA,W,92.0,M,305.0
means, the pilot is in WIND (or vane) mode with a set wind angle of 305 degrees (= 55 degrees on the port side) and it currently steers a heading of 92 degrees magnetic.
 
 

    $PPITA,A,92.0,T,
means, the pilot is in AUTO mode, holding a heading of 92 degrees true. In this mode the wind angle is not relevant and may be a null field (empty field).
