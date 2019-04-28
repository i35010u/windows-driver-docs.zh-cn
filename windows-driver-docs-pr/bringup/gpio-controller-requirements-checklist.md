---
title: GPIO 控制器要求清单
description: 本主题总结了硬件、 固件和软件要求的常规用途 IO (GPIO) 控制器设备向 Windows 公开的。
ms.assetid: 8097F391-ABF0-44A6-94D2-243AFBA3F984
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07b0b5f9818c99a5c3f28bc8f14a84e957415ac7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337586"
---
# <a name="gpio-controller-requirements-checklist"></a>GPIO 控制器要求清单


本主题总结了硬件、 固件和软件要求的常规用途 IO (GPIO) 控制器设备向 Windows 公开的。

## <a name="gpio-controller-hardware-requirements"></a>GPIO 控制器硬件要求


-   GPIO 控制器已集成到 SoC （存储总线未连接）。

    提高可靠性模拟 ActiveBoth。

-   支持级别模式下中断。

    所需的模拟 ActiveBoth 和 Debounce 仿真功能。

-   支持高和低中断极性。

    所需的模拟 ActiveBoth 和 Debounce 仿真功能。

-   在运行时，可以通过编程方式重新设置中断极性。

    所需的模拟 ActiveBoth 和 Debounce 仿真功能。

## <a name="gpio-controller-firmware-requirements"></a>GPIO 控制器固件要求


-   GPIO 控制器\_CRS 控制器中包括所有 pin 银行的所有资源。
-   GPIO 控制器\_CRS 资源排序提供银行系统中断映射。
-   \_AEI 方法和事件的方法 (\_Exx， \_Lxx 或\_EVT) 存在任何 GPIO 信号 ACPI 事件。
-   GPIO 控制器\_如果任何 ActiveBoth 中断连接到的控制器包含的 DSM 添加逻辑而不是逻辑高低。
-   实现\_REG 方法针对每个 GPIO 控制器，如果阻止使用 GeneralPurposeIO OpRegions \_REG 指示区域处理程序不可用。
-   Debounce 超时包括在需要 debouncing 任何中断的 GPIOInt 资源描述符。

## <a name="gpio-controller-driver-requirements"></a>GPIO 控制器驱动程序要求


-   支持第 2 版 GpioClx 和 GPIO 控制器驱动程序之间的接口：

    -   实现[*客户端\_QueryEnabledInterrupts* ](https://msdn.microsoft.com/library/windows/hardware/dn265184)回调函数。 这有很大帮助诊断中断风暴。
    -   如果**BankIdlePowerMgmtSupported**中设置了标志[**控制器\_BASIC\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh439358)结构 GPIO 控制器驱动程序必须实现[*客户端\_SaveBankHardwareContext* ](https://msdn.microsoft.com/library/windows/hardware/hh439419)并[*客户端\_RestoreBankHardwareContext*](https://msdn.microsoft.com/library/windows/hardware/hh439414)回调函数和这些函数必须保存/还原银行上下文，相应地包括其屏蔽/解除屏蔽的中断状态。 请注意，不能保证中断要断开连接时调用此函数，但如果它们仍保持连接，可确保将要屏蔽。
    -   如果**DeviceIdlePowerMgmtSupported**中设置了标志**控制器\_BASIC\_信息**结构[*客户端\_StartController* ](https://msdn.microsoft.com/library/windows/hardware/hh439424)并[*客户端\_StopController* ](https://msdn.microsoft.com/library/windows/hardware/hh439430)回调函数必须保存/还原所有银行的上下文相应地，包括其屏蔽/解除屏蔽的中断状态。 请注意，不能保证中断要断开连接时调用此函数，但如果它们仍保持连接，可确保将要屏蔽。
-   设置**EmulateDebouncing**中的标志**控制器\_BASIC\_信息**结构。 这会大大提高其中断可能会有所静电放电 （如按钮、 插入，等等） 的设备的干扰 immunity。
-   设置**EmulateActiveBoth**中的标志**控制器\_BASIC\_信息**结构，并实现[*客户端\_ReconfigureInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/hh698243)回调函数。 这可确保 ActiveBoth 中断的可靠边缘检测。

 

 




