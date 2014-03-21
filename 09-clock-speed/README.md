#Clock speed

A practical exercise to support episode 9 of the Cambridge GCSE Computing MOOC.

![](./images/cover.jpg "Cover Image")

##Introduction

This exercise assumes that at least one Raspberry Pi is available; however it is scalable to use many simultaneously.  There are two objectives: to demonstrate that clock speed affects computer performance, and to show that overclocking generates extra heat in the CPU.  A stop watch can also be used here.

The exercise consists of running two (or more) experiments where a Pi is programmed to count from zero to one million. The only variable in the tests will be changing the clock speed of the CPU.  Students will be required to time how long this takes manually, and monitor the CPU temperature during the test.

## Step 0: Setting Up your Pi

First check that you have all the parts you need to get your Raspberry Pi set up and working.

- Raspberry Pi
- Micro USB power adaptor
- An SD card with Raspbian already set up through NOOBS
- USB keyboard
- USB mouse
- HDMI cable
- A monitor or TV

###Activity Checklist:

1.	Place the SD card into the slot of your Raspberry Pi. It will only fit one way so be careful not to break the card. 
2.	Next connect the HDMI cable from the monitor (or TV) to the HDMI port on the Pi and turn on your monitor. 
3.	Plug the USB keyboard and mouse into the USB ports on the Pi.
4.	Plug in the micro USB power supply and you should see some text appear on your screen.
5.  When prompted to login type:

    ```
    Login: pi
    Password: raspberry
    ```


##Step 1: Set the clock speed

To configure the clock speed of your Raspberry Pi enter the following command:

`sudo raspi-config`

Select option `7 Overclock`.  You will see a warning about reducing the lifetime of your Raspberry Pi by doing this. While this is true, it will only have an effect if you leave a Raspberry Pi permanently overclocked.  You can reset the overclock back to `None` after this experiment is over using the same command.

This experiment works best with one Pi running with no overclock and one running on Turbo overclock (1000 Mhz).

Select the desired clock speed and press Enter, then go down to Finish and reboot the Pi.

##Step 2: Run the count

A simple Python script can be used to perform the counting; alternatively, a compiled C binary will also work.  Below is an example Python script.  This should be run from the command prompt outside of the X desktop.

Enter the following command to create a blank Python file with nano (a text editor program):

`nano count.py`

Enter the following Python code, or copy and paste it:

```python
#!/usr/bin/python
num = 0
while num <= 1000000:
	print num
	num += 1
```

Press `Ctrl - O` to save and `Ctrl - X` to quit.  Next, make the file executable with the following command:

`chmod +x count.py`

Now you’re ready to begin the count.  This should be treated like a race with a 'ready, set, go' start.  The expected result is that the Pi with the higher clock speed will reach one million first. To run the count program, enter the following command:

`./count.py`

##Step 3: Monitor the CPU temperature

The CPU temperature can now be monitored by logging in again on a separate getty terminal with `ALT-F2` and using the `watch` command with `vcgencmd`.

`watch -n 1 /opt/vc/bin/vcgencmd measure_temp`

Pupils can then switch between the count and the temperature monitor using `ALT-F1` and `ALT-F2`.

The count to one million will take over ten minutes to complete, which should be enough for the CPU temperature to settle into a stable value.  If two experiments can be run simultaneously side by side, the students should be able to observe which count is ahead and which is behind and the differences in temperature.

The results should show that the higher overclock completes the count first, but has a higher CPU temperature.  The time requirement of the experiment can be adjusted by changing the count from one million to a lower value such as 200000.
