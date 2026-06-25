# M2 Technical Reference ![MODAQ M2 Tech Ref](img/m2_icon.png#right)
This section contains details on some of the core M2 functions and nodes, as well as deeper discussions on some of the technical considerations.


## ROS2 Nodes
The M2 Reference Design includes the following nodes. Click on the item to expand its description.

<details>
    <summary>Node: m2_supervisor_node</summary>
    <br>This node manages a number of MODAQ's core functionality, which include system logger, email alerts, and rate limiter (snoozer) <br><br> 
    <b>Package: </b>m2_supervisor<br>
    <b>Alias: </b>M2Supervisor<br>
    <b>Configuration Parameters: </b>
    <ul>
    <li>log file path</li>
    <li>log file size limit</li>
    <li>SMTP settings</li> 
    <li>distribution email lists (2x)</li>
    <li>analyzed topics</li>
    <li>email snooze interval</li>
    </ul>
    <b>Publishers: </b>/system_messenger<br>
    <b>Subscriptions: </b>/system_messenger<br>
</details>
<details>
    <summary>Node: bag_recorder_node</summary>
    <br>Node description<br><br>
    <b>Package: </b>bag_recorder<br>
    <b>Alias: </b>N/A<br>
    <b>Configuration Parameters: </b>
    <ul>
    <li>IP address</li>
    </ul>
    <b>Publishers: </b>/system_messenger<br>
    <b>Subscriptions: </b>/system_messenger, /ain, /do, /din, /rtd, /bag_control<br>
</details>
<details>
    <summary>Node: labjack_ain_reader</summary>
    <br>Reads up to 8 AI channels simultaneously from a single Labjack T8. This node uses a configurable timer to fetch (poll) channel reads from the T8.<br><br>
    <b>Package: </b>labjack_t8_ros2<br>
    <b>Alias: </b>LabjackAINSlow<br>
    <b>Configuration Parameters: </b>
    <ul>
    <li>IP address</li>
    <li>sample rate</li>
    <li>topic name</li>
    </ul>
    <b>Publishers: </b>/system_messenger, /ain_slow<br>
    <b>Subscriptions: </b>none<br>
</details>
<details>
    <summary>Node: labjack_ain_streamer</summary>
    <br>Streams up to 8 AI channels from a single Labjack T8. This node sets the T8 to stream data continuously at rates up to 40 kHz. Channel reads are simultaneous. To better manage network resources for high speed streams, data transfers are batched by the ScansPerRead parameter.<br><br>
    <b>Package: </b>labjack_t8_ros22<br>
    <b>Alias: </b>LabjackAINFast<br>
    <b>Configuration Parameters: </b>
    <ul>
    <li>IP address</li>
    <li>sample rate</li>
    <li>scans per read</li>
    <li>topic name</li>
    </ul>
    <b>Publishers: </b>/system_messenger, /ain_fast<br>
    <b>Subscriptions: </b>none<br>
</details>
<details>
    <summary>Node: labjack_dac_writer</summary>
    <br>Controls one or more analog outputs on the T8. Output voltage can be adjusted between 0-10 VDC or ±10v with the LJTick-DAC<br><br>
    <b>Package: </b>labjack_t8_ros2<br>
    <b>Alias: </b>LabjackDAC<br>
    <b>Configuration Parameters: </b>
    <ul>
    <li>IP address</li>
    <li>channel selection</li>
    <li>topic name</li>
    </ul>
    <b>Publishers: </b>/system_messenger<br>
    <b>Subscriptions: </b>/LJ_Ctl_Pub<br>
</details>
<details>
    <summary>Node: labjack_do_node</summary>
    <br>Switches one or more digital output (logic level) channels on the T8 high or low.<br><br>
    <b>Package: </b>labjack_t8_ros2<br>
    <b>Alias: </b>LabjackDO<br>
    <b>Configuration Parameters: </b>
    <ul>
    <li>IP address</li>
    <li>topic name</li>
    </ul>
    <b>Publishers: </b>/system_messenger<br>
    <b>Subscriptions: </b>/do<br>
</details>
<details>
    <summary>Node: labjack_dio_reader</summary>
    <br>Reads the logic state of one or more DIO channels.<br><br>
    <b>Package: </b>labjack_t8_ros2<br>
    <b>Alias: </b>LabjackDIN<br>
    <b>Configuration Parameters: </b>
    <ul>
    <li>IP address</li>
    <li>topic name</li>
    </ul>
    <b>Publishers: </b>/system_messenger, /din<br>
    <b>Subscriptions: </b>none<br>
</details>
<details>
    <summary>Node: adnav_driver</summary>
    <br>Manages configuration and initialization of the Advanced Navigation GNSS Compass and publishes its data.<br><br>
    <b>Package: </b>adnav_gnss_compass<br>
    <b>Alias: </b>AdnavCompass<br>
    <b>Configuration Parameters: </b>too many to list here<br>
    <b>Publishers: </b>/system_messenger, /nav<br>
    <b>Subscriptions: </b>none<br>
</details>
<details>
    <summary>Node: xsens_mti_node</summary>
    <br>Manages configuration and initialization of the Xsens MTi-G-710 and publishes its data. This is a 3rd party package cloned from <a href="https://github.com/cnicho35/bluespace_ai_xsens_ros_mti_driver" target="_blank">here</a>.  This can work with other Xsens inertial sensors too.<br><br>
    <b>Package: </b>bluespace_ai_xsens_ros_mti_driver<br>
    <b>Alias: </b>XsensINS<br>
    <b>Configuration Parameters: </b>too many to list here<br>
    <b>Publishers: </b>/system_messenger, /imu/acceleration<br>
    <b>Subscriptions: </b>none<br>
</details>
<details>
    <summary>Node: ed582_driver</summary>
    <br>Reads up to four channels of RTD temperature measurements from a Brainbox ED-582. This is adapted from a 3rd party API available <a href="https://www.brainboxes.com/faq/how-do-i-use-cpp-to-communicate-with-my-remote-io-module" target="_blank">here</a>.<br><br>
    <b>Package: </b>ed582<br>
    <b>Alias: </b>RTDed582<br>
    <b>Configuration Parameters: </b>
    <ul>
    <li>IP address</li>
    <li>sample rate</li>
    <li>topic name</li>
    </ul>
    <b>Publishers: </b>/system_messenger, /rtd<br>
    <b>Subscriptions: </b>none<br>
</details>
<details>
    <summary>Node: m2_control</summary>
    <br>This node can read directives published by the HMI and/or incorporate control logic and publish actions for digital or analog output channels.<br><br>
    <b>Package: </b>m2_control<br>
    <b>Alias: </b>M2Control<br>
    <b>Configuration Parameters: </b>
    <ul>
    <li>IP address</li>
    <li>sample rate</li>
    <li>topic name</li>
    </ul>
    <b>Publishers: </b>/system_messenger, /dac, /do<br>
    <b>Subscriptions: </b>/hmi_ctl<br>
</details>
<details>
    <summary>Node: rosbridge_websocket</summary>
    <br>This node creates a bridge between ROS2 and a websocket that is used to subscribe to and publish topics from a webpage using roslibjs. This is a lightly modified version of rosbridge_server from the <a href="https://github.com/RobotWebTools/rosbridge_suite" target="_blank">rosbridge_suite</a> github repo.<br><br>
    <b>Package: </b>rosbridge_server_m2<br>
    <b>Alias: </b>Rosbridge<br>
    <b>Configuration Parameters: </b>none<br>
    <b>Publishers: </b>/hmi_ctl<br>
    <b>Subscriptions: </b>/din, /ain_slow, /rtd<br>
</details>

## Real-Time

A real-time system is one that assures certain deadlines are met reliably within expected time constraints. See this <a href="https://en.wikipedia.org/wiki/Real-time_computing" target="_blank">Wikipedia article</a> for a more complete definition.  

!!! tip "Recommended Reading"

    <a href="https://shuhaowu.com/blog/2022/01-linux-rt-appdev-part1.html" target="_blank">This</a> series of blog posts by Shuhao Wu is an excellent, easy to read distillation of numerous resources on real-time computing. This is highly recommended reading to provide context to some of the topics that will be discussed in this section.

Using a real-time architecture and approach in MODAQ allows better management of sources of latency and reduction of jitter. What this means in practical terms is that certain time-critical loops, processes, or functions can execute deterministically and that variation in timing of successive iterations is kept low.  

### Latency

Opening Task Manager in Windows or the equivalent in in other operating systems (OS), there may be hundreds of processes listed that are all vying for a slice of the CPU's time. These include things like device drivers, software updaters, user software, malware detectors, and lots of other things that comprise the modern computing experience. With fast, multi-core processors, these appear to be seamlessly juggled, usually with little delay apparent to the user. This is all managed by the scheduler and it tries to be fair as it doles out access to a CPU core. Under critical analysis, an application may have to wait a non-deterministic amount of time for that CPU attention- and that wait time might vary considerably for each request. This variation may be only a few milliseconds (or longer) but for DAQs running loops hundreds or several thousand times per second, that's an eternity. 
 
A properly configured real-time stack offers the software developer some tools to better manage how the real-time code gets its CPU time by preempting lower priority processes (jumping to the head of the line). The end effect is that the real-time code should experience less of this source of latency.

!!! info

    <b>Determinism</b>
    <p>
    A deterministic real-time system should complete a task within a bound time period in a consistent and repeatable manner. 

Different real-time approaches yield better or worse maximum latency periods. Specific project requirements or use-cases often dictate the maximum acceptable latency for a particular application. This is most common for safety-critical systems, such as an anti-lock brake controller, where missing a deadline can result in disaster. These will often be associated with terms such as "guaranteed" or "hard" real-time. From a system architecture and software development standpoint, achieving this level of latency and determinism is difficult and probably not practical nor even necessary for a DAQ such as M2. 

However, in the space between extremely low latency, safety-critical, real-time systems and general purpose operating systems without real-time support, there is <a href="https://wiki.linuxfoundation.org/realtime/start" target="_blank">Real-Time Linux</a>. Or, more correctly, the PREEMPT_RT patch for Linux kernels.   

### Real-Time Linux 

Linux with the PREEMPT_RT patch has been successfully used in various industries such as automotive, space, and industrial automation for years and by organizations including National Instruments, NASA, and SpaceX.[^1][^2] This lends confidence that it's appropriate for M2 applications.

At the time of writing, it appears that the mainline Linux kernel is expected to gain real-time support[^3] in a coming release. Until that happens, it's necessary to <a href="https://docs.ros.org/en/humble/Tutorials/Miscellaneous/Building-Realtime-rt_preempt-kernel-for-ROS-2.html" target="_blank">manually compile the kernel with the PREEMPT_RT patch</a> or find a distribution for an already patched RT kernel.   

### Validating RT Performance

Once a patched kernel has been installed and the necessary changes to BIOS have been made, it's necessary to conduct some tests on the system to validate the 'as-built' latency performance. 

A very useful tool for this is provided by intel: <a href="https://eci.intel.com/docs/3.3/development/performance/benchmarks.html#about-rtpm" target="_blank">RTPM</a>. This tool will evaluate the settings on your computer to ensure they are optimized for real-time performance. It also will conduct several tests that will characterize your real-time performance.

## Precision Time Protocol

The promise of PTP is that all connected PTP-aware devices will be synchronized and reference-time accurate to 100's, if not 10's of nanoseconds- without drift. By comparison, <a href="https://en.wikipedia.org/wiki/Network_Time_Protocol" target="_blank">Network Time Protocol</a> (NTP), which is what most consumer computers and laptops use as a time reference, can at best achieve 10's of milliseconds accuracy. While NTP accuracy might be perfectly acceptable to some and often better than a real time clock (which can drift <a href="https://www.best-microcontroller-projects.com/ppm.html" target="-blank">several seconds a day</a>), it's a ~6 order of magnitude difference in accuracy as compared to PTP. If a quality time reference is not available, samples taken from input modules on the same DAQ controller will be disciplined by the same clock and will likely be <i>precisely</i> timestamped relative each other, but may not be <i>accurate</i> to actual time (i.e. UTC) . 

Where the real power of PTP is realized is in synchronizing samples taken by disparate systems. These can be DAQs on the same subnet, sharing the same master clock or systems completely disconnected from each other and separated miles apart. As long as each system is disciplined to a healthy PTP reference clock, the samples will be synchronized to the aforementioned nanosecond time precision. This is a boon for distributed architectures and system design flexibility, allowing multi-controller synchronization without physical interconnections. 

In our experience, PTP implementation either works magically or is a real bear. It does help to have some knowledge of networking and configuring managed switches. PTP requires the following for optimal performance:

1. PTP time server
2. PTP-capable endpoints (e.g. M2 controller, ethernet based devices)
3. PTP services configured and running on the endpoints
4. PTP-capable network switch

These items need to be properly configured, otherwise the PTP performance may be degraded or non-existent. For instance, we've found that some cheap consumer unmanaged switches (such as the <a href="https://www.netgear.com/business/wired/switches/unmanaged/gs305/" target="_blank">Netgear GS305</a>) will pass PTP packets, however the observed PTP performance degrades to microsecond accuracy with large standard deviations. This is still pretty good and better than NTP, but not ideal and possibly not reliable. 

The linux support for PTP can be installed using `sudo apt install linuxptp`. This enables the ptp4l tool which allows user interaction with the PTP hardware clocks on your controller's NIC.

## Parsing MCAP Files
The mcap file format was designed by Foxglove  and they also developed a GUI software that is able to process these data files and output plots, tables and other useful visualizers. For information on this GUI viewer, please see [Useful Links](links.md#ubuntu).

To analyze the data, we recommend using the rosbags python package which is also able to parse the mcap files and generate numpy arrays which can be used for data analysis. This can be installed with pip: `pip install rosbags`

Example Python code for parsing mcap files:
```py
from rosbags.rosbag2 import Reader
from rosbags.serde import deserialize_cdr
import numpy as np
from matplotlib import pyplot as plt
from pathlib import Path
from rosbags.typesys import Stores, get_types_from_msg, get_typestore

import os

def get_all_file_names(folder_path):
    try:
        # List all files in the given folder
        file_names = os.listdir(folder_path)
        # Filter out directories, only keep files and return their full paths
        file_paths = [os.path.join(folder_path, file) for file in file_names if os.path.isfile(os.path.join(folder_path, file))]
        
        # Generate the modaq_messages/msg/{FILE_NAME} strings
        modaq_messages = [f"modaq_messages/msg/{os.path.splitext(file)[0]}" for file in file_names if os.path.isfile(os.path.join(folder_path, file))]        
        return file_paths, modaq_messages
    except Exception as e:
        print(f"An error occurred: {e}")
        return [], []


# Example usage
folder_path = r"C:\MODAQ\MODAQ2-RD-Dev\src\modaq_messages\msg"
file_names, message_types = get_all_file_names(folder_path)
print(file_names, message_types)
typestore = get_typestore(Stores.ROS2_HUMBLE)
add_types = {}

for i, name in enumerate(file_names):
    print("name: ", name)
    msgpath = Path(name)
    msgdef = msgpath.read_text(encoding='utf-8')
    print(msgdef)
    add_types.update(get_types_from_msg(msgdef, message_types[i]))

typestore.register(add_types)
# create reader instance and open for reading
last_time = 0
last_timer = 0
dt_ros = []
dt = []

with Reader(r"./") as reader:
    # Topic and msgtype information is available on .connections list.
    for connection in reader.connections:
        print(connection.topic, connection.msgtype)

    # Iterate over messages.

    for connection, timestamp, rawdata in reader.messages():
        if connection.topic == '/ain_flap':
            msg = typestore.deserialize_cdr(rawdata, connection.msgtype)
            time = (msg.header.stamp.sec + (msg.header.stamp.nanosec/1e9))
            
            dt_ros.append(time-last_time)
            last_time = time
            

            
plt.plot(np.array(dt_ros)[100::])
plt.show()
```

## ADCs
While there's an abundance of really good analog to digital converters (ADCs) on the market, one of our biggest challenges was finding one suitable for our requirements. 

- 24 bit
- Simultaneous sampling
- At least 4 channels
- Channel-to-channel isolation
- Anti-aliasing filter
- Not dependent on a particular vendor's controller (i.e. non-proprietary)
- Ready to go, with simple ethernet or USB interfacing
- Works with linux




## 4-20 mA Current Loops
One or more of the 8 analog inputs available on the RD could be allocated for measuring outputs from devices that signal using a current loop. The 4-20 mA current loop would be converted to 1-5 volts using a 250 Ω (or 2-10 VDC using a 500 Ω) precision shunt resistor connected across the positive and negative input terminals of the voltage channel. 

Alternatively, M2 supports using current loop interface modules with digital outputs (<a href="https://store.ncd.io/product/4-channel-4-20-ma-current-loop-receiver-16-bit-ads1115-i2c-mini-module/" target="_blank">example 1</a>, <a href="https://store.ncd.io/product/4-channel-i2c-4-20ma-current-receiver-with-i2c-interface/" target="_blank">example 2</a>), which is not included in the RD specification, but available upon request.

![](img/passive_cl.png)<br>
![](img/active_cl.png)<br>
It's important to note that there are 2 types of current loops: passive and active. Passive devices (such as some pressure transducers) require an external source driving the current loop, while active devices provide the driving source internally. The M2 RD supports active loops through the shunt resistor method mentioned in the first paragraph. Passive circuits can be made active with the addition of a power supply. The example 1 link for the optional current loop interface works with passive devices.

## Heading

Getting a reliable estimate of heading on a fixed or semi-stationary device can be tricky. Devices that rely on Earth's magnetic field need to be calibrated in-situ and have the proper magnetic declination correction applied. 

Since a calibration procedure generally requires rotating the sensor 360° in one or more axis, this is often difficult or near impossible once the sensor is mounted on the device (WEC, buoy, etc). It's easier to calibrate the compass prior to installation, however this is not effective, since the magnetic field will most likely be distorted by the presence of hard and soft iron sources near the mounting location. 

This leads to our decision to include the Advanced Navigation GNSS Compass in the M2 RD design specification. It avoids the issues associated with magnetic compasses by using dual GPS antennas to achieve 0.2° heading performance. Because of the antennas, it needs a clear view of the sky- which might not be possible in some use-cases. Therefore, the magnetic heading from the Xsens INS can be used instead. 

If very precise heading estimates are required in your application and GPS is not an option, we suggest looking at some gyrocompass options, such as the ring laser or fiber optic gyros. 

[^1]: https://www.linux.com/news/in-the-trenches-with-thomas-gleixner-real-time-linux-kernel-patch-set/
[^2]: https://ntrs.nasa.gov/api/citations/20200002390/downloads/20200002390.pdf
[^3]: https://arstechnica.com/gadgets/2024/09/real-time-linux-is-officially-part-of-the-kernel-after-decades-of-debate/