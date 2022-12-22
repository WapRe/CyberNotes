<h2>Docker</h2>
<p>
  /.dockerenv : in the root directory to check if there is any in the machine<br>
</p>
<h3>RTSP server with docker</h3>
<p>
  docker run : to run a container <br>
  --rm : to run a 1-time container, it does not save, it gets deleted after using it. <br>
  -it : to open a sudo TTY and see the output<br>
  -- network=host : tells to use the same network interfaces that our host is using, instead of the container.<br>
  aler9/rtsp-simple-server : image to use (?)<br>
  <ul><li>root@ip-10-10-61-111:~# docker run --rm -it --network=host aler9/rtsp-simple-server<br>
2022/12/22 17:56:50 INF rtsp-simple-server v0.20.4<br>
<b><i>2022/12/22 17:56:50 INF [RTSP] listener opened on :8554 (TCP), :8000 (UDP/RTP), :8001 (UDP/RTCP)</i></b><br>
2022/12/22 17:56:50 INF [RTMP] listener opened on :1935<br>
    2022/12/22 17:56:50 INF [HLS] listener opened on :8888</li></ul>
 We just created a RTSP server to listen!
</p>
