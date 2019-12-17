### PulseAudio-Record-Output-and-Input

I have conquered pulseaudio. With this I can record input and output in one stream while both are in use e.g. by discord.

Adding this to the end of /etc/pulse/default.pa FINALLY permitted me to AT LAST record mic input and computer output.

The programs I use are pavucontrol and audio-recorder {source of "User defined audio source" set to OutSink and MicSink}.

# Add this to the end of /etc/pulse/default.pa or ~/.pulse/default.pa

# Ensure that the value of source=0 is your stereo monitor index & source=1 is your mic input via "pacmd list-sources"

  # This sink mirrors monitored speaker output

load-module module-null-sink sink_name=OutSink

update-sink-proplist OutSink device.description=OutSink

load-module module-loopback source=0 sink=OutSink

  # This sink mirrors mic input

load-module module-null-sink sink_name=MicSink

update-sink-proplist MicSink device.description=MicSink

load-module module-loopback source=1 sink=MicSink
