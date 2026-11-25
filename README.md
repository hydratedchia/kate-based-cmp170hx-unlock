# PWMVID and GPU0 tools

This repository documents an experimental setup for generating PWMVID signals and observing how an NVIDIA GA100 GPU responds. It starts at the hardware level with a custom PWMVID control board and STM32 firmware, adds host-side utilities to drive PWM waveform experiments during board bring-up, and pairs them with capture and analysis tools to see how GA100 GPU0 register states shift after each run.

| Path | What it contains |
| --- | --- |
| [`firmware/`](firmware/README.md) | STM32G431 application, custom USB bootloader, host utilities, and tests |
| [`driver/pwmvidctl/`](driver/pwmvidctl/README.md) | Operator CLI, sequence planner, calibration profiles, and waveform examples |
| [`gpu0-registers/`](gpu0-registers/README.md) | GA100 register maps, bounded capture engine, and offline state analysis |
| [`glitch-loop/`](glitch-loop/README.md) | Experiment-loop pseudocode and historical commanded waveforms |

## Offline checks

```sh
(cd firmware && sh tests/run_tests.sh && sh bootloader/tests/run_all.sh)
(cd driver/pwmvidctl && python3 -m unittest discover -s tests -v)
(cd gpu0-registers && cargo test --workspace --locked)
```

Building the STM32 images requires PlatformIO; see the firmware README for
build environments. Hardware bring-up requires the measurements in
[`firmware/docs/BENCH_ACCEPTANCE.md`](firmware/docs/BENCH_ACCEPTANCE.md).

I did not discover or create the methodology for this unlock, Kate is responisible for this original incredible work.  I improved and developed my own hardware device and improved upon some existing hardware features.  Feel free to submit issues or contact me via.

Original project material is licensed under [MIT](LICENSE). Third-party terms
and source notices are described in [LICENSING.md](LICENSING.md).
