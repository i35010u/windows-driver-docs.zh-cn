---
title: Microsoft USB 打印机驱动程序 (Usbprint.sys)
description: Usbprint.sys 是 USB 打印机的由 Microsoft 提供的设备驱动程序。 Usbprint.sys 配合 Usbmon.dll 端到端之间提供连接 USB 打印机和高级打印机驱动程序。
ms.assetid: 6fc1635d-b819-43ba-a549-2488995fa9b0
keywords:
- 打印机驱动程序 WDK USB
- USB 打印机 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e2e31e498f40d842d0d1fe343955babe1bc2485
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338384"
---
# <a name="microsoft-usb-printer-driver-usbprintsys"></a>Microsoft USB 打印机驱动程序 (Usbprint.sys)


Usbprint.sys 是 USB 打印机的由 Microsoft 提供的设备驱动程序。 Usbprint.sys 配合 Usbmon.dll 端到端之间提供连接 USB 打印机和高级打印机驱动程序。




与某些 USB 设备类的驱动程序，不同 Usbprint.sys 不"驱动器"打印机。 相反，Usbprint.sys 提供了更高级别的驱动程序可以控制打印机的通信管道。 由于是并行的打印机，则返回 true，USB 打印机需要打印机驱动程序以呈现打印作业，并且可能还需要用于管理与打印机高层次的沟通的语言监视器。

安装过程中的 USB 打印机，系统提供的 INF 文件，Usbprint.inf，获取从本地文件 Driver.cab Usbprint.sys。 Driver.cab 随操作系统一起安装，因为打印机安装程序通常不需要原始安装介质安装 Usbprint.sys。 有关 Usbprint.inf 详细信息，请参阅[打印机连接到 USB 端口](printer-connected-to-a-usb-port.md)。 有关 Driver.cab 详细信息，请参阅[打印机安装和插 Manager](printer-installation-and-the-plug-and-play-manager.md)。

本部分包含以下主题：

[USBPRINT 的编程注意事项](programming-considerations-for-usbprint.md)

 

 




