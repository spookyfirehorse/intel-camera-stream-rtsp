         ffmpeg -hwaccel vdpau   -fflags nobuffer -flags low_delay -hide_banner  -strict experimental  \
         -f pulse   -i alsa_input.pci-0000_00_0e.0.analog-stereo  -f v4l2   -i /dev/video0  \
        -c:v libx264 -b:v 1M  -preset ultrafast -tune zerolatency -maxrate 1M -minrate 1M -bufsize 500k  -bf 0   \
        -filter:v  fps=fps=source_fps:round=near  -threads $(nproc)  -max_muxing_queue_size 9999     -flush_packets 0  \
         -c:a  libfdk_aac -eld_sbr 1   -vbr 0  -b:a 32k -fps_mode:v cfr  -ac 1    -ar 48000   -f rtsp -rtsp_transport udp rtsp://localhost:8566/mystream
