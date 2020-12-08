---
title: GPIO 控制器要求清单
description: 本主题概述向 Windows 公开的常规用途 IO (GPIO) 控制器设备的硬件、固件和软件要求。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 313a6a085a8871490ed5e3afab3fbe2bf9647d35
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803347"
---
# <a name="gpio-controller-requirements-checklist"></a>GPIO 控制器要求清单


本主题概述向 Windows 公开的常规用途 IO (GPIO) 控制器设备的硬件、固件和软件要求。

## <a name="gpio-controller-hardware-requirements"></a>GPIO 控制器硬件要求


-   GPIO 控制器集成到 SoC (未通过 SPB 总线) 连接。

    提高模拟 ActiveBoth 的可靠性。

-   支持级别模式中断。

    这两种模拟功能都是必需的。

-   支持高和低中断极性。

    这两种模拟功能都是必需的。

-   可以在运行时重新设计中断极性。

    这两种模拟功能都是必需的。

## <a name="gpio-controller-firmware-requirements"></a>GPIO 控制器固件要求


-   GPIO 控制器 \_ CRS 包含控制器中所有 pin bank 的所有资源。
-   GPIO 控制器 \_ CRS 资源排序提供银行到系统中断映射。
-   \_对于任何 GPIO 发出信号的 ACPI 事件，AEI 方法和事件方法 (s)  (\_ Exx、 \_ Lxx 或 \_ .evt) 存在。
-   \_如果连接到控制器的任何 ActiveBoth 中断都断言逻辑高而不是逻辑低，则会包含 GPIO 控制器 DSM。
-   \_为每个 GPIO 控制器实现 REG 方法，并防止使用 GeneralPurposeIO OpRegions （如果 \_ REG 指示区域处理程序不可用）。
-   对于需要 debouncing 的任何中断，GPIOInt 资源描述符中都包含了反应反超时。

## <a name="gpio-controller-driver-requirements"></a>GPIO 控制器驱动程序要求


-   支持 GpioClx 与 GPIO 控制器驱动程序之间的接口版本2：

    -   实现 [*客户端 \_ QueryEnabledInterrupts*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_enabled_interrupts) 回调函数。 这极大地有助于诊断中断风暴。
    -   如果在 [**控制器 \_ 基本 \_ 信息**](/windows-hardware/drivers/ddi/gpioclx/ns-gpioclx-_client_controller_basic_information)结构中设置了 **BankIdlePowerMgmtSupported** 标志，则 GPIO 控制器驱动程序必须实现 [*客户端 \_ SaveBankHardwareContext*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_save_bank_hardware_context)和 [*客户端 \_ RestoreBankHardwareContext*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_restore_bank_hardware_context)回调函数，并且这些函数必须相应地保存/还原银行上下文，包括中断的掩码/未屏蔽状态。 请注意，在调用此函数时不保证中断，但如果它们仍处于连接状态，则保证它们被屏蔽。
    -   如果在 **控制器 \_ 基本 \_ 信息** 结构中设置了 **DeviceIdlePowerMgmtSupported** 标志，则 [*客户端 \_ StartController*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_start_controller)和 [*客户端 \_ StopController*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_stop_controller)回调函数必须正确保存/还原所有银行的上下文，包括中断的掩码/未屏蔽状态。 请注意，在调用此函数时不保证中断，但如果它们仍处于连接状态，则保证它们被屏蔽。
-   在 **控制器 \_ 基本 \_ 信息** 结构中设置 **EmulateDebouncing** 标志。 这会显著提高中断受到静电放电 (如按钮、插头等) 设备的干扰抗干扰性。
-   在 **控制器的 \_ 基本 \_ 信息** 结构中设置 **EmulateActiveBoth** 标志，并实现 [*客户端 \_ ReconfigureInterrupt*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_reconfigure_interrupt)回调函数。 这可确保 ActiveBoth 中断的可靠边缘检测。

 

