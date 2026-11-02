# Free-Space Optical Communication (FSO) Implementation

## Aim: 
To implement and analyze a free space optical communication link using a laser/LED transmitter and photodiode/APD receiver.

## Apparatus/Software Required:
Python Colab

## Theory:
	FSO uses light beams to transmit data through free space instead of fiber.
	Performance depends on distance, alignment, and atmospheric attenuation.
	Received power decreases exponentially with distance.

## Formula:
Loss=10⋅〖log⁡〗_10 (P_in/P_out )

## 1
## Setup the Transmitter
Info
Prepare the optical source for transmission.
	Use a Laser/LED source
	Mount it on an optical bench
	Ensure stable power supply

## 2
## Align the Optical Path
Warning
Proper alignment ensures maximum received signal.
	Place transmitter and receiver in line of sight
	Adjust using lenses/mirrors if needed
	Minimize beam divergence

## 3
## Connect the Receiver
Setup the photodiode/APD to detect the optical signal.
	Mount detector opposite to transmitter
	Connect to oscilloscope for signal observation
	Record received power

## 4
## Measure Received Power
Collect data at different distances.
Loss = 10 log10(Pin / Pout)
	Vary distance (1 m, 5 m, 10 m, etc.)
	Note received power in µW
	Calculate link loss

## 5
## Plot Graphs
Visualize performance of FSO link.
	Plot Received Power vs Distance
	Observe exponential decay trend
	Compare with theoretical model

## 6
## Conclude Results
Success
Summarize findings of the experiment.
	Reliable communication up to ~10 m indoors
	Loss increases with distance
	Alignment critical for performance

## Sample Output
Graph: Received Power vs Distance (decay curve)

<img width="630" height="467" alt="image" src="https://github.com/user-attachments/assets/0ec8bb24-ddfb-4d3a-b0f2-a5b661798ad4" />
<img width="672" height="466" alt="image" src="https://github.com/user-attachments/assets/2a113e54-2433-4072-ba62-16539939e93a" />
<img width="672" height="461" alt="image" src="https://github.com/user-attachments/assets/448e0d3f-a834-4e14-953f-4d429b7a9996" />

## Python Code
```

import numpy as np
import matplotlib.pyplot as plt

# Parameters
L = 2
lam, lam0 = 1550, 550
V = np.linspace(0.1, 20, 100)
R = np.linspace(0, 50, 100)

# Kruse model
def q(v):
    if v > 50: return 1.6
    if v > 6: return 1.3
    return 0.585 * v**(1/3) + 0.34

# 1. Attenuation vs visibility
Q = np.array([q(v) for v in V])
A = 4.343 * (3.91 / V) * (lam/lam0)**(-Q) * L

plt.figure()
plt.plot(V, A)
plt.xlabel("Visibility (km)")
plt.ylabel("Atmospheric Attenuation (dB)")
plt.title("FSO Attenuation vs Visibility (Kruse Model)")
plt.grid()
plt.show()

# 2. Rain attenuation
rain = 1.076 * R**0.67

plt.figure()
plt.plot(R, rain)
plt.xlabel("Rain Rate (mm/hr)")
plt.ylabel("Rain Attenuation (dB/km)")
plt.title("Rain Attenuation in FSO Link")
plt.grid()
plt.show()

# 3. Attenuation vs wavelength
W = np.linspace(800, 1600, 100)
A_w = [4.343 * (3.91/2) * (w/lam0)**(-q(2)) * L for w in W]

plt.figure()
plt.plot(W, A_w)
plt.xlabel("Wavelength (nm)")
plt.ylabel("Attenuation (dB)")
plt.title("Attenuation vs Wavelength (Fog Condition)")
plt.grid()
plt.show()

# Insertion loss
Pin, Pout = 1, 0.8
print("Insertion Loss =", round(10*np.log10(Pin/Pout), 2), "dB")
print("Result: FSO atmospheric attenuation simulated.")
```

## Output
<img width="571" height="455" alt="image" src="https://github.com/user-attachments/assets/f545e62b-2945-4389-a94c-8cd39d8e26eb" />
<img width="562" height="455" alt="image" src="https://github.com/user-attachments/assets/5ecb8def-d646-4356-99be-78427b9b0222" />
<img width="563" height="455" alt="image" src="https://github.com/user-attachments/assets/509103c9-fcb9-44d6-9266-9b4289f46477" />

  
## Result
