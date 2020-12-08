---
title: 验证容器 ID 的实现
description: 验证容器 ID 的实现
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20b6e198dc57f431aa084ca43c14fe483682d194
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840955"
---
# <a name="verifying-the-implementation-of-container-ids"></a>验证容器 ID 的实现


从 Windows 7 开始，你可以在 "设备和打印机" 用户界面 (UI ") 中查看连接到计算机的所有设备。 设备会以物理方式显示给用户，这就是一种支持一个或多个功能的 "塑料片"。 UI 中显示的图标表示设备的主要功能。

若要利用设备和打印机 UI 提供的新功能，设备必须正确实现容器 Id。

验证设备是否符合容器 ID 要求的最简单方法是打开 "设备和打印机" UI，以查看设备的显示方式。 如果设备符合容器 ID 要求，则该设备的 "设备和打印机" UI 中应只显示一个图标。

以下屏幕截图显示了具有连接的 USB 键盘和鼠标的计算机的 "设备和打印机" UI。 请注意，每个设备只显示一个图标。

![显示 usb 键盘和鼠标图标的 "设备和打印机" 窗口的屏幕截图](images/containerid-7.png)

在此示例中，将鼠标连接到台式计算机上的 USB 端口。 但对于物理设备，只显示鼠标的一个实例。 因此，此设备会正确实现容器 ID 要求。

在 "设备和打印机" UI 中，具有一个主功能的物理设备或 "容器" 由一个对象表示。 在此示例中，鼠标不包含 Microsoft **ContainerID** 操作系统描述符或序列号。 因此，即插即用 (PnP) 管理器使用鼠标的可移动功能生成容器 ID 值。

有关可移动设备功能的详细信息，请参阅 [从可移动设备功能生成的容器 id](container-ids-generated-from-the-removable-device-capability.md)。

 

 





