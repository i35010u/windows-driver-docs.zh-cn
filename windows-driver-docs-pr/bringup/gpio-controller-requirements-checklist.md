---
title: GPIO 控制器要求清单
description: 本主题概述向 Windows 公开的常规用途 IO （GPIO）控制器设备的硬件、固件和软件要求。
ms.assetid: 8097F391-ABF0-44A6-94D2-243AFBA3F984
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57bf8b8fa76b1c255398f0d31fb0411b51e3602f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834479"
---
# <a name="gpio-controller-requirements-checklist"></a>GPIO 控制器要求清单


本主题概述向 Windows 公开的常规用途 IO （GPIO）控制器设备的硬件、固件和软件要求。

## <a name="gpio-controller-hardware-requirements"></a>GPIO 控制器硬件要求


-   GPIO 控制器已集成到 SoC （未通过 SPB 总线连接）。

    提高模拟 ActiveBoth 的可靠性。

-   支持级别模式中断。

    这两种模拟功能都是必需的。

-   支持高和低中断极性。

    这两种模拟功能都是必需的。

-   可以在运行时重新设计中断极性。

    这两种模拟功能都是必需的。

## <a name="gpio-controller-firmware-requirements"></a>GPIO 控制器固件要求


-   GPIO 控制器 \_CRS 包含控制器中所有 pin 银行的所有资源。
-   GPIO 控制器 \_CRS 资源排序提供银行到系统中断映射。
-   对于 GPIO 发出信号的 ACPI 事件，\_AEI 方法和事件方法（\_Exx、\_Lxx 或 \_.EVT）存在。
-   如果连接到控制器的任何 ActiveBoth 中断都断言逻辑高而不是逻辑低，则 GPIO 控制器 \_DSM。
-   为每个 GPIO 控制器实现 \_REG 方法，并防止在 \_REG 指示区域处理程序不可用时使用 GeneralPurposeIO OpRegions。
-   对于需要 debouncing 的任何中断，GPIOInt 资源描述符中都包含了反应反超时。

## <a name="gpio-controller-driver-requirements"></a>GPIO 控制器驱动程序要求


-   支持 GpioClx 与 GPIO 控制器驱动程序之间的接口版本2：

    -   \_QueryEnabledInterrupts 回调函数实现[*客户端*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_enabled_interrupts)。 这极大地有助于诊断中断风暴。
    -   如果在[**控制器\_基本\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/ns-gpioclx-_client_controller_basic_information)结构中设置了**BankIdlePowerMgmtSupported**标志，则 GPIO 控制器驱动程序必须实现[*客户端\_SaveBankHardwareContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_save_bank_hardware_context)和[*客户端\_RestoreBankHardwareContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_restore_bank_hardware_context)回调函数，并且这些函数必须适当地保存/还原银行上下文，包括中断的掩码/未屏蔽状态。 请注意，在调用此函数时不保证中断，但如果它们仍处于连接状态，则保证它们被屏蔽。
    -   如果在**控制器\_基本\_信息**结构中设置了**DeviceIdlePowerMgmtSupported**标志，则[*客户端\_StartController*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_start_controller)和[*客户端\_StopController*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_stop_controller)回调函数必须适当保存/还原所有银行的上下文，包括中断的掩码/未屏蔽状态。 请注意，在调用此函数时不保证中断，但如果它们仍处于连接状态，则保证它们被屏蔽。
-   在控制器中设置**EmulateDebouncing**标志 **\_基本\_信息**结构。 这会显著提高中断受到静电放电（如按钮、插头等）的设备的干扰抗干扰性。
-   在控制器中设置**EmulateActiveBoth**标志 **\_基本\_信息**结构，然后实现[*客户端\_ReconfigureInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_reconfigure_interrupt)回调函数。 这可确保 ActiveBoth 中断的可靠边缘检测。

 

 




