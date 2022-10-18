# Thinkfan installation (P14s)

> **Note:** The number and names of the sensors may differ between Lenovo notebook models. They must be adapted for the respective notebook model. The present configuration is for a Lenovo P14s notebook.


## Arch Linux

1. Install **thinkfan** (AUR) and **lm_sensors**.
Note that the thinkfan package installs /usr/lib/modprobe.d/thinkpad_acpi.conf, which contains 

    ```config
    options thinkpad_acpi fan_control=1
    ```

    So fan control is enabled by default.

2. Now, load the module by typing:

    ```bash
    modprobe thinkpad_acpi
    ```

    ```bash
    cat /proc/acpi/ibm/fan
    ```

3. Check, if the hwmon exists used in the thinkfan.conf exists.  */sys/class/hwmon* may have *hwmon@0..n* monitor directories. To check if the hwmon exists *cat /hwmon@***x***/name*. The number of indices is can be read by checkin how many *temp***x***_input* and *temp***x***_label* file exists.

4. Change the hwmon settings in the thinkfan.conf if necessary.  Afterwards copy the *thinkfan.conf* to */etc/thinkfan.conf*

    ```bash
    sudo cp thinkfan.conf /etc/thinkfan.conf
    ```

5. Configure thinkfan to use the newly created file

    ```bash
    echo 'THINKFAN_ARGS="-c /etc/thinkfan.conf"' | sudo tee -a /etc/default/thinkfan
    ```

6. Finally, enable the thinkfan.service by typing

    ```bash
    sudo systemctl enable thinkfan.service
    ```

    ```bash
    sudo systemctl start thinkfan.service
    ```  

## Ubuntu

1. Enable fan control

    ```bash
    echo 'options thinkpad_acpi fan_control=1' | sudo tee /lib/modprobe.d/thinkpad_acpi.conf
    ```

2. Install thinkfan package

    ```bash
    sudo apt install thinkfan
    ```

3. do steps 3-6 from Arch Linux.  Keep in mind, that the hwmon settings may differ between Arch Linux and Ubuntu.
