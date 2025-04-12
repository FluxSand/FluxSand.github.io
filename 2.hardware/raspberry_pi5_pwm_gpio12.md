---
title: raspberry_pi5_pwm_gpio12
layout: default
parent: Hardware
nav_order: 1
---

# Raspberry Pi 5 GPIO12 Output PWM Configuration Flow (for Buzzer/LED)

## 📁 System Configuration Flow

### 1. Edit Configuration File

Open Configuration File（Raspberry Pi OS usually use `/boot/firmware/config.txt`）：

```bash
sudo nano /boot/firmware/config.txt
```

### 2. Add PWM Configuration (⚠️Add at the end of the file, don't put it in a section like '[cm5]')

```ini
dtoverlay=pwm,pin=12,func=4,clock=50000000
```

- `pwm`: Represent using single-channel PWM overlay
- `pin=12`: Select GPIO12（physical pin 32）
- `func=4`：Select ALT4 mode (PWM0_0 feature of GPIO12)
- `clock=50000000`：Specifies a PWM input clock of 50MHz

### 3. Reboot System

```bash
sudo reboot
```

---

## 🧪 PWM Control Command

After rebooting, execute the following commands in turn to enable the PWM signal output (3kHz, 50% duty cycle):

```bash
# export pwm0 channel
echo 0 | sudo tee /sys/class/pwm/pwmchip0/export
sleep 0.1

# set PWM parameters
echo 333333 | sudo tee /sys/class/pwm/pwmchip0/pwm0/period
echo 166666 | sudo tee /sys/class/pwm/pwmchip0/pwm0/duty_cycle

# enable PWM output
echo 1 | sudo tee /sys/class/pwm/pwmchip0/pwm0/enable
```

> Example configuration is 3kHz frequency (period 333,333ns), 50% duty cycle (166,666ns)

---

## ✅ Methods for Successful Verification (Optional)

- ✅ The buzzer functions well
- ✅ The LEDs flash or dimly brighten
- ✅ GPIO12 average voltage measured by multimeter ≈ 1.6V (duty cycle 50%)
- ✅ Command 'gpioinfo |.' grep GPIO12' shows that the pin is in an active or used state

---

## 🛠 Optional: Automation Scripts (enable_pwm12.sh)

```bash
#!/bin/bash

echo 0 | sudo tee /sys/class/pwm/pwmchip0/export
sleep 0.1
echo 333333 | sudo tee /sys/class/pwm/pwmchip0/pwm0/period
echo 166666 | sudo tee /sys/class/pwm/pwmchip0/pwm0/duty_cycle
echo 1       | sudo tee /sys/class/pwm/pwmchip0/pwm0/enable

echo "✅ GPIO12 is outputting a 3kHz PWM waveform"
```

How to use:：

```bash
chmod +x enable_pwm12.sh
./enable_pwm12.sh
```

---
