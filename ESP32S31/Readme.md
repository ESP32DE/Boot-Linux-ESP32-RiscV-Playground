A brand new [Dual Core Risc V ](https://github.com/espressif/esp-idf/blob/904c94ba3a1e4d5e112d79db2346ccf9be7a585b/.gitlab/ci/host-test.yml#L40) with an extra Low Power Core SoC from Espressif
combines [the radio power](https://github.com/espressif/esp-idf/blob/0b8e7b0efa6285bafd13806978243d1e34931dd8/components/soc/esp32s31/include/soc/interrupts.h#L139-L152) of the S3 and the interface diversity of the P4 and mixes the whole thing on top of the high-end with an incredible [62 in/out gpio's](https://github.com/espressif/esp-idf/blob/0b8e7b0efa6285bafd13806978243d1e34931dd8/components/soc/esp32s31/include/soc/gpio_num.h#L18-L80)
if that's not the inux candidate at all, what a Risc V beast. [IDF is only giving us](https://github.com/espressif/esp-idf/tree/master/components/soc/esp32s31) a glimpse at this point.

```

#define SOC_CPU_CORES_NUM               (2U)
#define SOC_INT_CLIC_SUPPORTED          1        // RISC-V CLIC interrupt controller
#define SOC_LP_CORE_SUPPORTED           1        // Dedicated Low-Power core
#define SOC_HP_CPU_HAS_MULTIPLE_CORES   1
#define SOC_CPU_HAS_FPU                 1        // Hardware Floating Point Unit
#define SOC_CPU_HAS_PIE                 1        // Position-Independent Executable coprocessor

```

high-performance RISC-V core (HP domain) + ultra-low-power RISC-V core (LP domain)
Full ( RV32IMAFCP ) baseline + modern extensions (CLIC, PMP, FPU, PIE, branch predictor, hardware loops)

```
#define SOC_GPIO_PIN_COUNT                 63
#define SOC_GPIO_IN_RANGE_MAX           62
#define SOC_GPIO_OUT_RANGE_MAX          62
#define SOC_GPIO_VALID_GPIO_MASK        (0x7FFFFFFFFFFFFFFF)   // 63 bits set
```

Highest GPIO count of any Espressif chip ever released (S3 = 45, P4 = 56, S31 wins with 63)

4× high-performance UARTs
System timer (2 counters, 3 alarms)
eFuse with key-purpose field
Flash encryption (XTS-AES-128/256)
Full LP-IO subsystem (independent clock, independent wakeup)
Deep-sleep wakeup on GPIO0–7
40 MHz XTAL support
Shared I/D cache with write-back and freeze
Physical Memory Protection (PMP) with 128-byte granularity

Native RISC-V RV32IMAFCP + CLIC + PMP

Let's wait with bated breath to see what else is to come;

The ESP32-S31 is a real, high-end RISC-V monster with 63(62) GPIOs and a modern heterogeneous dual-core design. It is currently in the early bring-up phase in ESP-IDF master (Dec 2025), but the hardware capabilities are already fully defined and vastly superior to the ESP32-S3. Massive thanks to the espressifer who pulled the real soc_caps.h — this is the smoking gun the community has been waiting for!




