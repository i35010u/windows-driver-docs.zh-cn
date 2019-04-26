---
title: 间接显示驱动程序模型概述
description: 间接显示驱动程序模型旨在提供简单的用户模式驱动程序模型，以支持未连接到传统的 GPU 显示输出的监视器。
ms.assetid: E2E64500-5F99-42A7-8945-B496026EA142
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3be4062bb6e9d2e9664ae6dfacf61507a0a46184
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325056"
---
# <a name="indirect-display-driver-model-overview"></a>间接显示驱动程序模型概述


间接显示驱动程序模型旨在提供简单的用户模式驱动程序模型，以支持未连接到传统的 GPU 显示输出的监视器。 例如，硬件保护装置连接到通过已连接到它的常规 （VGA、 DVI、 HDMI 等 DP） 监视器的 USB PC。

## <a name="span-iddriverimplementationspanspan-iddriverimplementationspanspan-iddriverimplementationspandriver-implementation"></a><span id="Driver_Implementation"></span><span id="driver_implementation"></span><span id="DRIVER_IMPLEMENTATION"></span>驱动程序实现


间接显示器驱动程序模型实现为 UMDF 类扩展。 该驱动程序是设备的 UMDF 驱动程序，并于接口，windows 图形子系统使用 IddCx （间接显示驱动程序类扩展） 所公开的功能。

## <a name="span-idindirectdisplaydriverfunctionalityspanspan-idindirectdisplaydriverfunctionalityspanspan-idindirectdisplaydriverfunctionalityspanindirect-display-driver-functionality"></a><span id="Indirect_Display_Driver_Functionality"></span><span id="indirect_display_driver_functionality"></span><span id="INDIRECT_DISPLAY_DRIVER_FUNCTIONALITY"></span>间接显示驱动程序的功能


由于间接显示器驱动程序是 UMDF 驱动程序，它负责所有 UMDF 功能，例如设备的通信、 电源管理、 插等。IddCx 提供间接显示器驱动程序，以按以下方式与 Windows 图形子系统进行交互的接口：

1. 创建表示间接显示设备的图形适配器
2. 报表监视正在连接和断开连接系统
3. 提供连接的监视器的说明
4. 还提供了可用的显示模式
5. 支持其他显示功能，如硬件鼠标光标、 gamma、 I2C 通信和受保护的内容
6. 进程桌面映像来在监视器上显示，因为间接显示驱动程序是在会话 0 中运行的 UMDF 驱动程序，它不具有任何组件的用户会话中运行，因此任何驱动程序不稳定将不会影响整个系统的稳定性。

## <a name="span-idusermodemodelspanspan-idusermodemodelspanspan-idusermodemodelspanuser-mode-model"></a><span id="User_Mode_Model"></span><span id="user_mode_model"></span><span id="USER_MODE_MODEL"></span>用户模式下模型


间接显示器驱动程序是使用内核模式组件不支持以用户模式唯一模式，因此驱动程序是可以使用任何 DirectX API 以便处理桌面映像。 实际上，IddCx 提供桌面图像进行编码 DirectX 图面中。

**请注意**  间接显示器驱动程序应生成为通用 windows 驱动程序，以便在多个 Windows 平台上使用它。

 

生成时，在 UMDF 间接显示器驱动程序声明的 IddCx 构建时所针对的版本并 OS 确保在加载驱动程序加载 IddCx 的正确版本。

以下部分介绍间接显示器驱动程序模型：

[IddCx 对象](iddcx-objects.md)
 

 





