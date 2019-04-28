---
title: 验证容器 ID 的实现
description: 验证容器 ID 的实现
ms.assetid: 961f3c69-8010-4bf5-9bdf-cc01ff40546a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08d19affafef1fb3c9b1074b94af348d86aeaffb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339321"
---
# <a name="verifying-the-implementation-of-container-ids"></a>验证容器 ID 的实现


从 Windows 7 开始，可以看到已连接到设备和打印机用户界面 (UI) 中的计算机的所有设备。 设备显示为它们以物理方式显示给用户，这是作为单个"部分的塑料"支持一个或多个函数。 在 UI 中显示的图标表示该设备的主要功能。

若要充分利用设备和打印机用户界面提供的新功能，设备必须正确实现容器 Id。

若要验证设备符合容器 ID 要求的最简单方法是打开的设备和打印机用户界面，以查看设备的显示方式。 如果容器 ID 要求设备符合，只有一个图标应为该设备，显示在设备和打印机用户界面。

下面的屏幕截图显示了附加的 USB 键盘和鼠标的计算机的设备和打印机用户界面。 请注意，只有一个图标会显示对于每个设备。

![设备和打印机窗口显示有关 usb 键盘和鼠标的图标的屏幕截图](images/containerid-7.png)

在此示例中，鼠标连接到台式计算机上的 USB 端口。 但是，只显示一个实例的鼠标的物理设备。 因此，此设备正确地实现容器 ID 要求。

具有一个主函数或"容器"，物理设备由设备和打印机用户界面中的某个对象表示。 在此示例中，鼠标不包含 Microsoft **ContainerID**操作系统描述符或序列号。 因此，插即用 (PnP) 管理器通过使用鼠标可移动功能生成容器 ID 值。

有关可移动设备功能的详细信息，请参阅[从可移动设备功能生成的容器 Id](container-ids-generated-from-the-removable-device-capability.md)。

 

 





