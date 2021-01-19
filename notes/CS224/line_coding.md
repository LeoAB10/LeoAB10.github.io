---
title: CS 224 - Computer Networks
layout: post
---

## Line Coding

Line coding is the process of converting data into signal. At the sender's end we convert sequence of bits into digital signal and at the receiver's end the signal is recreated into bits by decoding the signal.

### Multiple types of line codes

#### Non-Return to Zero (NRZ)
In this line coding 1 is represented by a positive voltage and 0 by a negative voltage.
<div align="center">
<img src="https://upload.wikimedia.org/wikipedia/commons/5/55/NRZcode.png" alt="NRZ">
</div>

The problem with NRZ is that a sequence of several consecutive 1s or 0s means the signal stays constant for a long period of time. There are two problems caused by continuous long strings of 0s or 1s.

The first problem is known as *clock recovery* problem. The clock recovery problem is that both the sender and receiver's clocks have to be precisely synchronized in order for the receiver to recover the same bits the sender transmits. The receiver tries to synchronize it's clock using the received signal-*The Clock Recovery Process*. Whenever the signal changes from 1 to 0 or 0 to 1, then the receiver knows it is at a clock cycle boundary and it can resynchronize itself. However, a long period of time without any change in signal leads to *clock drift*. Thus clock recovery depends on having a lot of transitions in the signal.

The second problem is known as *baseline wander*. During the signal transfer the receiver keeps and average of the signal it has received so far and then compare the incoming signal with the average to distinguish between low and high signal. Whenever the signal is significantly lower than the average the receiver concludes that it's a 0; similarly when the signal is much higher than the average the receiver interprets it to be a 1. And when there are too many consecutive 0s or 1s the average voltage wanders from the baseline (hence the name), making it more difficult to detect significant change in the signal.

One approach that addresses this problem is called *non-return to zero inverted* (NRZI). In this encoding the sender makes a transition from current signal to encode a 1 and stays at the current signal to encode a 0. This solves problem of consecutive 1s.
<img src="https://upload.wikimedia.org/wikipedia/commons/e/e4/NRZI_example.png" alt="NRZI">
