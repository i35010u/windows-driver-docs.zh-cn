---
title: 间接显示驱动程序模型概述
description: 间接显示驱动程序模型旨在提供简单的用户模式驱动程序模型，以支持未连接到传统 GPU 显示输出的监视器。
ms.assetid: E2E64500-5F99-42A7-8945-B496026EA142
ms.date: 07/17/2020
ms.localizationpriority: medium
ms.openlocfilehash: 162732b980b5970b90459ccd53f4d1d97ffc1d29
ms.sourcegitcommit: 0d89fc46058efb2ebc6ed9bd8f638c3f8cc1a678
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2020
ms.locfileid: "86459209"
---
# <a name="indirect-display-driver-model-overview"></a>间接显示驱动程序模型概述

间接显示驱动程序（IDD）模型旨在提供简单的用户模式驱动程序模型，以支持未连接到传统 GPU 显示输出的监视器。 例如，通过 USB 连接到电脑的转换器连接了常规（VGA、DVI、HDMI、DP 等）监视器。

## <a name="idd-implementation"></a>IDD 实现

IDD 实现为[UMDF](/windows-hardware/drivers/wdf/getting-started-with-umdf-version-2)类扩展。 IDD 是开发人员提供的用于设备的 UMDF 驱动程序，它使用[IddCx](/windows-hardware/drivers/ddi/iddcx/) （间接显示驱动程序类扩展）公开的功能与 windows 图形子系统交互。

![UMDF 体系结构内的间接显示驱动程序](images/idd_umdf_arch.png)

## <a name="idd-functionality"></a>IDD 功能

由于 IDD 是一个 UMDF 驱动程序，因此它负责所有 UMDF 功能，如设备通信、电源管理、即插即用等。IDD 使用 IddCx 接口通过以下方式与 Windows 图形子系统交互：

* 创建表示间接显示设备的图形适配器
* 与系统连接并断开的报表监视器
* 提供已连接监视器的说明
* 提供可用的显示模式
* 支持其他显示功能，如硬件鼠标光标、伽玛、I2C 通信和受保护的内容
* 处理要显示在监视器上的桌面映像

IDD 在[会话 0](/windows-hardware/drivers/wdf/session-zero-guidelines-for-umdf-drivers)中运行，无需在用户会话中运行任何组件，因此任何驱动程序不稳定都不会影响整个系统的稳定性。

## <a name="user-mode-model"></a>用户模式模型

IDD 是仅限用户模式的模型，不支持内核模式组件。 因此，该驱动程序可以使用任何 DirectX Api 来处理桌面映像。 事实上，IddCx 提供了在 DirectX 图面中进行编码的桌面映像。 驱动程序不应调用不适用于驱动程序使用的用户模式 Api，如 GDI、窗口化 Api、OpenGL 或 Vulkan。

> [!NOTE]
>
> IDD 应该构建为[通用 windows 驱动程序](/windows-hardware/drivers/gettingstarted/writing-a-umdf-driver-based-on-a-template)，以便它可以在多个 windows 平台上使用。

在生成时，UMDF IDD 会声明生成它的 IddCx 的版本，并确保在加载驱动程序时加载正确版本的 IddCx。

以下各节介绍了 IDD 模型：

[IddCx 对象](iddcx-objects.md)  
[调试](indirect-display-debugging.md)

## <a name="sample-code"></a>示例代码

Microsoft 在[Windows 驱动程序示例 GitHub](https://github.com/microsoft/Windows-driver-samples/tree/master/video/IndirectDisplay)上提供了一个示例 IDD 实现。 此示例演示如何连接监视器、如何响应模式集，以及如何接收帧。
