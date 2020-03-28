---
title: 间接显示驱动程序模型概述
description: 间接显示驱动程序模型旨在提供简单的用户模式驱动程序模型，以支持未连接到传统 GPU 显示输出的监视器。
ms.assetid: E2E64500-5F99-42A7-8945-B496026EA142
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75b124798a900a4b185975f582cf5dc79e64a9e2
ms.sourcegitcommit: 7135ca169cc274543fbe170330c054ee18573134
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2020
ms.locfileid: "80367629"
---
# <a name="indirect-display-driver-model-overview"></a>间接显示驱动程序模型概述


间接显示驱动程序模型旨在提供简单的用户模式驱动程序模型，以支持未连接到传统 GPU 显示输出的监视器。 例如，通过 USB 连接到电脑的转换器，具有常规（VGA，DVI，HDMI，DP 等）监视器。

## <a name="span-iddriver_implementationspanspan-iddriver_implementationspanspan-iddriver_implementationspandriver-implementation"></a><span id="Driver_Implementation"></span><span id="driver_implementation"></span><span id="DRIVER_IMPLEMENTATION"></span>驱动程序实现


间接显示驱动程序模型是作为 UMDF 类扩展实现的。 该驱动程序是设备的 UMDF 驱动程序，它使用 IddCx （间接显示驱动程序类扩展）公开的功能与 windows 图形子系统交互。

## <a name="span-idindirect_display_driver_functionalityspanspan-idindirect_display_driver_functionalityspanspan-idindirect_display_driver_functionalityspanindirect-display-driver-functionality"></a><span id="Indirect_Display_Driver_Functionality"></span><span id="indirect_display_driver_functionality"></span><span id="INDIRECT_DISPLAY_DRIVER_FUNCTIONALITY"></span>间接显示驱动程序功能


因为间接显示驱动程序是 UMDF 驱动程序，所以它负责所有 UMDF 功能，如设备通信、电源管理、即插即用等。IddCx 提供了一个接口，以通过以下方式与 Windows 图形子系统交互：

1. 创建表示间接显示设备的图形适配器
2. 与系统连接并断开的报表监视器
3. 提供已连接监视器的说明
4. 提供可用的显示模式
5. 支持其他显示功能，如硬件鼠标光标、伽玛、I2C 通信和受保护的内容
6. 处理桌面映像以在监视器上显示，因为间接显示驱动程序是会话0中运行的一个 UMDF 驱动程序，该驱动程序在用户会话中没有任何运行的组件，因此任何驱动程序不稳定都不会影响整个系统的稳定性。

## <a name="span-iduser_mode_modelspanspan-iduser_mode_modelspanspan-iduser_mode_modelspanuser-mode-model"></a><span id="User_Mode_Model"></span><span id="user_mode_model"></span><span id="USER_MODE_MODEL"></span>用户模式模型


间接显示驱动程序是一种仅限用户模式的模型，不支持内核模式组件，因此驱动程序可以使用任何 DirectX API 来处理桌面映像。 事实上，IddCx 提供了在 DirectX 图面中进行编码的桌面映像。

**请注意**  间接显示器驱动程序应该构建为通用 windows 驱动程序，以便它可以在多个 windows 平台上使用。

 

在生成时，UMDF 间接显示驱动程序将声明生成它的 IddCx 的版本，并确保在加载驱动程序时加载正确版本的 IddCx。

以下各节介绍间接显示驱动程序模型：

[IddCx 对象](iddcx-objects.md)
 
## <a name="sample-code"></a>示例代码

Microsoft 提供了位于[Windows 驱动程序示例 GitHub](https://github.com/microsoft/Windows-driver-samples/tree/master/video/IndirectDisplay)上的间接显示驱动程序的示例实现。 此示例演示如何连接监视器、如何响应模式集，以及如何接收帧。

 





