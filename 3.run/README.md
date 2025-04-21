---
title: Build and Run
layout: default
has_children: false
nav_order: 4
---

# Usage

## Build

```bash
mkdir build
cd build
export CC=clang
export CXX=clang++
cmake -DCMAKE_BUILD_TYPE=Release ..
make
```

You can also use multi-core compilation for better performance:

```bash
make -j$(nproc)
```

## Run

```bash
sudo systemctl daemon-reexec
sudo systemctl daemon-reload
sudo systemctl enable fluxsand.service
sudo systemctl start fluxsand.service
```

You can check the service status or view logs using:

```bash
systemctl status fluxsand.service
journalctl -u fluxsand.service -f
```

## Unit Test

```bash
mkdir build
cd build
export CC=clang
export CXX=clang++
cmake -DCMAKE_BUILD_TYPE=Release -DTEST=True ..
make
```

example output:

```bash
> FluxSand
[TEST] Beep: 2093 Hz for 250 ms
[TEST] Beep: 2349 Hz for 250 ms
[TEST] Beep: 2637 Hz for 250 ms
Invalid BMP280 ID: Invalid argument
MPU9250 initialized. WHO_AM_I: 0x00
Error: MPU9250 connection failed (WHO_AM_I: 0x00): Invalid argument
MPU9250 calibration file not found. Using default values.
[UnitTest] Starting AHRS unit test...
[UnitTest] Quaternion: [q0=+1.0000, q1=+0.0071, q2=-0.0071, q3=+0.0000]
[UnitTest] Euler Angles (rad): [rol=+0.0141, pit=+6.2690, yaw=+6.2831]
[UnitTest] ✅ Test Passed: Orientation is correct at rest.
[Timing] Init & assignment     :     0.06 µs
[Timing] Update()              :     0.35 µs
[Timing] GetEulr()             :    18.44 µs
[Timing] Output                :   462.37 µs
[Timing] Verify                :    16.89 µs
[Timing] Total                 :   498.11 µs
Model Input Tensors:
  Name: input
  Shape: [1, 1500, 8]
Model Output Tensor:
  Name: dense_1
  Shape: [-1, 10]
Model initialized: /usr/local/share/FluxSand/model/model.onnx

[InferenceEngine::UnitTest] Starting inference timing test...
Run 01 →  56.328 ms | Result: Unrecognized
...
Run 50 →  36.727 ms | Result: Still

[Inference Timing Summary]
  Total Runs    : 50
  Min Time (ms) :  24.696
  Max Time (ms) :  56.817
  Avg Time (ms) :  45.146
[InferenceEngine::UnitTest] ✅ Timing test complete.
[CompGuiX::UnitTest] Starting GUI unit test...
[Test] Draw number 42 in portrait...
[Test] Draw time 12:34 in portrait...
[Test] Draw time 12:34 in landscape...
[Test] Render humidity icon...
[Test] Render temperature icon...
[Test] Enable sand...
[Test] Reset sand...
[Test] Disable sand...
[CompGuiX::UnitTest] ✅ Test complete.
[SandGrid::UnitTest] Starting sand grid test...
[Test] AddNewSand → ✅ Success
[Test] StepOnce → Particle count: 1 → 1
[Test] MoveSand(→down) → ✅ Success
[Test] Clear → Count after clear: 0
[Perf] Running StepOnce 100 times...
[Perf] StepOnce timing (µs): min =   1.94, max =  18.74, avg =   2.17
[SandGrid::UnitTest] ✅ Test complete.
[FluxSand::UnitTest] Starting application unit test...
  [Test] Simulating mode: 0
    → Run() completed in 7.83 ms
  [Test] Simulating mode: 1
    → Run() completed in 9.84 ms
  [Test] Simulating mode: 2
    → Run() completed in 9.68 ms
  [Test] Simulating mode: 3
Stopwatch started
    → Run() completed in 9.05 ms
  [Test] Simulating mode: 4
Timer started for 30 seconds
    → Run() completed in 5.09 ms
[FluxSand::UnitTest] ✅ All modes tested in 43.62 ms
```
