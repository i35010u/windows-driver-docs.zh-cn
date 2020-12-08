---
title: 间接显示驱动程序模型概述
description: 间接显示驱动程序模型提供了一个简单的用户模式驱动程序模型，用于支持未连接到传统 GPU 显示输出的监视器。
keywords:
- 间接显示驱动程序，WDK
- IDD，WDK
- 间接显示驱动程序模型
- IDD 模型
- 间接显示驱动程序实现
- IDD 实现
ms.date: 09/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: fa0b7f973b8875a35daa42f0d4ba4a805dd9d01b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839317"
---
# <a name="indirect-display-driver-overview"></a>间接显示驱动程序概述

间接显示驱动程序 (IDD) 模型提供了简单的用户模式驱动程序模型，以支持未连接到传统 GPU 显示输出的监视器。 例如，通过 USB 连接到电脑并连接到它的常规 (VGA、DVI、HDMI、DP 等) 的转换器。

## <a name="idd-implementation"></a>IDD 实现

IDD 是设备的第三方提供的 [UMDF](../wdf/umdf-driver-host-process.md) 驱动程序。 它使用由 [IddCx](/windows-hardware/drivers/ddi/iddcx/) 公开的功能 (间接显示驱动程序类扩展来开发) 通过以下方式与 windows 图形子系统交互：

* 创建表示间接显示设备的图形适配器
* 与系统连接并断开的报表监视器
* 提供已连接监视器的说明
* 提供可用的显示模式
* 支持其他显示功能，如硬件鼠标光标、伽玛、I2C 通信和受保护的内容
* 处理要显示在监视器上的桌面映像

由于 IDD 是一个 UMDF 驱动程序，因此它还负责实现所有 [UMDF](../wdf/overview-of-the-umdf.md) 功能，如设备通信、电源管理、即插即用等。

IDD 在 [会话 0](../wdf/session-zero-guidelines-for-umdf-drivers.md) 中运行，无需在用户会话中运行任何组件，因此任何驱动程序不稳定都不会影响整个系统的稳定性。

下图提供了体系结构概述。

![UMDF 体系结构内的间接显示驱动程序](images/idd_umdf_arch.png)

## <a name="user-mode-model"></a>用户模式模型

IDD 是仅限用户模式的模型，不支持内核模式组件。 因此，该驱动程序可以使用任何 DirectX Api 来处理桌面映像。 事实上，IddCx 提供了在 DirectX 图面中进行编码的桌面映像。

> [!NOTE]
>
> 驱动程序不应调用不适用于驱动程序使用的用户模式 Api，如 GDI、窗口化 Api、OpenGL 或 Vulkan。
>
> IDD 应该构建为 [通用 windows 驱动程序](../gettingstarted/writing-a-umdf-driver-based-on-a-template.md) ，以便它可以在多个 windows 平台上使用。

在生成时，UMDF IDD 会声明生成它的 IddCx 的版本，并确保在加载驱动程序时加载正确版本的 IddCx。

## <a name="iddcx-callback-and-function-naming-conventions"></a>IddCx 回调和函数命名约定

| 前缀 | 类型 | 说明 |
| ------ | ---- | ----- |
| **EVT_IDD_CX** \_*XXX* | IDD 回调函数 | IDDs 实现了 IddCx 特定的回调（如 [**EVT_IDD_CX_ADAPTER_COMMIT_MODES**](/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_adapter_commit_modes)）以及相关的 WDF 回调（如 [**EVT_WDF_DEVICE_D0_EXIT**](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)）。 |
| **IddCx**_Xxx_ | 函数 | 系统提供的、可调用 IDDs 的 IddCx 类扩展函数;例如， [**IddCxAdapterInitAsync**](/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxadapterinitasync)。 |
| **PFN_IDDCX** \_*XXX* | 指向 IddCx 函数的指针 | IDDs 不使用这些指针。 相反，驱动程序应使用 **IddCx**_Xxx_ 函数。 |

## <a name="sample-code"></a>示例代码

Microsoft 在 [Windows 驱动程序示例 GitHub](https://github.com/microsoft/Windows-driver-samples/tree/master/video/IndirectDisplay)上提供了一个示例 IDD 实现。 此示例演示如何连接监视器、如何响应模式集，以及如何接收帧。
