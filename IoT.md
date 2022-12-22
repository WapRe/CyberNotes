<h2>IoT protocols</h2>
<p>
  We can break up IoT protocols into one of two types, an IoT data protocol or an IoT network protocol.<br>
  IoT data protocol commonly relies on the TCP/IP (Transmission Control Protocol/Internet Protocol) model,<br>
  and an IoT network protocol relies on wireless technology for communication.<br>
  Rather than relying on traditional TCP protocols, these protocols use wireless technology such as:<br>
  <ul><li>Wi-Fi, Bluetooth, ZigBee, and Z-Wave to transfer data and communicate between entities.</li></ul>
  Because data communication is the primary objective of IoT data protocols, they commonly take the form of a messaging protocol;<br>
  that is, the protocol facilities the sending and receiving of a message or payload between two parties.<br>
  Messaging protocols communicate between two devices through an independent server (”middleware”) or by negotiating a communication method amongst themselves.<br>
</p>
<h3>Popular protocols</h3>
<p>
  <table class="default">
  <tr>
    <th scope="row">Protocol</th>
    <th scope="row">Communication Method</th>
    <th scope="row">Description</th>
  </tr>
  <tr>
    <td>MQTT (Message Queuing Telemetry Transport)</td>
    <td>Middleware</td>
    <td>A lightweight protocol that relies on a publish/subscribe model to send or receive messages.</td>
  </tr>
  <tr>
    <td>CoAP (Constrained Application Protocol)</td>
    <td>Middleware</td>
    <td>Translates HTTP communication to a usable communication medium for lightweight devices</td>
  </tr>
  <tr>
    <td>AMQP (Advanced Message Queuing Protocol)</td>
    <td>Middleware</td>
    <td>Acts as a transactional protocol to receive, queue, and store messages/payloads between devices.</td>
  </tr>
  <tr>
    <td>DDS (Data Distribution Service</td>
    <td>Middleware</td>
    <td>A scalable protocol that relies on a publish/subscribe model to send or receive messages. </td>
  </tr>
  <tr>
    <td>HTTP (Hypertext Transfer Protocol)</td>
    <td>Device-to-Device</td>
    <td>Used as a communication method from traditional devices to lightweight devices or for large data communication.</td>
  </tr>
  <tr>
    <td>WebSocket </td>
    <td>Device-to-Device</td>
    <td>Relies on a client-server model to send data over a TCP connection.</td>
  </tr>
  </table>
</p>
<h2>Mosquitto</h2>
<h3>Commands</h3>
<p>
  We can use the mosquitto_sub (https://mosquitto.org/man/mosquitto_sub-1.html) client utility to subscribe to an MQTT broker.<br>
  Subscribing to a Topic:
  <ul>
    <li>mosquitto_sub -t device/ping : connecting to a localhost and subscribing to the topic, device/ping.</li>
    <li>mosquitto_sub -h example.thm -t device/thm : specify a remote broker using the -h flag, connecting to example.thm and subscribing to the topic, device/thm.</li>
  </ul>
  We can use the mosquitto_pub (https://mosquitto.org/man/mosquitto_pub-1.html) client utility to publish to an MQTT broker.<br>
  Publishing to a Topic:
  <ul>
    <li>mosquitto_pub -h example.thm -t device/info -m "This is an example" : Publishing to the topic, device/info on the host, example.thm with the message, "This is an example." </li>
      <ul><li>we need to include a -m or —message flag to denote our message/payload</li></ul>
  </ul>
  Other usefull flags:
  <ul>
    <li>-d: Enables debug messages.</li>
    <li>i or —id: Specifies the id to identify the client to the server.</li>
    <li>-p or —port: Specifies the port the broker is using. Defaults to port 1883</li>
    <li>-u or —username: Used to specify the username for authentication.</li>
    <li>-P or —password: Used to specify the password for authentication.</li>
    <li>—url: Used to specify username, password, host, port, and topic in one URL.</li>
  </ul>
</p>
