Hermes-Lite Python Module
=========================

This is a Python module to allow alternate command and control of a Hermes-Lite 2.0. It can be run before or at the same time as standard SDR software is in use. It is recommended to make any changes before standard SDR software is started. It uses port 1025. The purpose is to allow configuration of new, experimental or non-openhpsdr features. For example, setting the TX buffer latency, configuring the external clocks, and synchronizing multiple radios. It is not intended to replace standard SDR software. The intent is that useful features will eventually be adopted by standard SDR software once matured and proven here.

# Installation

 1. Install python3 with "sudo apt install python3" on Linux, see [here](https://www.python.org/) for other platforms.
 2. Download the hermeslite.py form this github repository
 3. Start interactive python3 with "python3 -i hermeslite.py"

This will discover any Hermes-Lite 2.0 on your network and create a hl object for the first unit found.

Future installation may use [pypl](https://pypi.org/). Future use may be from a web browser with [jupyter](https://jupyter.org/).

# Set TX Buffer Latency and PTT Hang Time

The code below will set the TX buffer latency to 20ms and the PTT hang time to 5ms.
```python
hl.config_txbuffer(20,5)
```

The TX buffer latency is how much time of samples to save in the TX buffer before beginning to transmit. You need to keep some samples in the buffer to smooth out any network UDP packet jitter. Start at 0 TX buffer latency (and 0 PTT hang time) and increase the latency until you find a value whic h stops any relay clicks.

The PTT hang time is how much time to wait when the TX buffer is empty before releasing the relays and exiting TX. A PTT hang time of 4 or 5ms can "hide" relay clicks, but there will still be clicks in your TX signal for the time when the buffer was empty.

# Use External Clock Input on CL1 of 76.8MHz

```python
hl.enable_cl1_direct()
```

# Update Gateware

## From File
```python
hl.update_gateware('somegatewarefileyoudownloaded.rbf')
```

## Latest Stable github hl2b5up
```python
hl.update_gateware_github()
```

## Specific github Version
```python
hl.update_gateware_github('testing/20200803_72p3/hl2b5up_main/hl2b5up_main.rbf')
```

# EEPROM MAC

```python
hl.set_eeprom_mac('ba:19')
hl.get_eeprom_mac()
hl.set_use_eeprom_mac()
##hl.clear_use_eeprom_mac()  ##Uncomment to disable eeprom_mac
```

# EEPROM IP

```python
hl.set_eeprom_ip('192.168.33.222')
hl.get_eeprom_ip()
hl.set_use_eeprom_ip()
##hl.clear_use_eeprom_ip()  ##Uncomment to disable eeprom_ip
```

# EEPROM Favor DHCP

```python
hl.set_favor_dhcp()
##hl.clear_favor_dhcp()  ##Uncomment to disable favor of dhcp
```


