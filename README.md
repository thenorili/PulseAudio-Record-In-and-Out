### PulseAudio-Record-Output-and-Input
I have done it at last. "pacmd list-sources" shows that my stereo monitor's index=0 and my microphone's index=1. Adding this to the end of /etc/pulse/default.pa FINALLY permitted me to AT LAST record mic input and computer output.

## Add this to the end of /etc/pulse/default.pa or ~/.pulse/default.pa
## Ensure that the value of source=0 is your stereo monitor index & source=1 your mic input

  ## This sink mirrors monitored speaker output

load-module module-null-sink sink_name=OutSink
update-sink-proplist OutSink device.description=OutSink
load-module module-loopback source=0 sink=OutSink

  ## This sink mirrors mic input

load-module module-null-sink sink_name=MicSink
update-sink-proplist MicSink device.description=MicSink
load-module module-loopback source=1 sink=MicSink
