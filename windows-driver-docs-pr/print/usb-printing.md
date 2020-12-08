---
title: Microsoft USB 打印机驱动程序 (Usbprint.sys)
description: Usbprint.sys 是 Microsoft 提供的 USB 打印机设备驱动程序。 Usbprint.sys 与 Usbmon.dll 配合使用来提供 USB 打印机和高级打印机驱动程序之间的端到端连接。
keywords:
- 打印机驱动程序 WDK，USB
- USB 打印机 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cc43939845d75b9724d73d976bdb652462783ee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835469"
---
# <a name="microsoft-usb-printer-driver-usbprintsys"></a>Microsoft USB 打印机驱动程序 (Usbprint.sys)


Usbprint.sys 是 Microsoft 提供的 USB 打印机设备驱动程序。 Usbprint.sys 与 Usbmon.dll 配合使用来提供 USB 打印机和高级打印机驱动程序之间的端到端连接。




与某些 USB 设备类驱动程序不同，Usbprint.sys 不会 "驱动" 打印机。 Usbprint.sys 提供了一种通信管道，更高级别的驱动程序可以通过该通道来控制打印机。 对于并行打印机，USB 打印机需要打印机驱动程序来呈现打印作业，并且可能还需要使用语言监视器来管理与打印机的高级通信。

安装 USB 打印机时，系统提供的 INF 文件 Usbprint 将从本地文件 Driver.cab 中获取 Usbprint.sys。 由于 Driver.cab 随操作系统一起安装，因此打印机安装程序通常不需要安装 Usbprint.sys 的原始安装介质。 有关 Usbprint 的详细信息，请参阅 [连接到 USB 端口的打印机](printer-connected-to-a-usb-port.md)。 有关 Driver.cab 的详细信息，请参阅 [打印机安装和即插即用管理器](printer-installation-and-the-plug-and-play-manager.md)。

本节包含下列主题：

[USBPRINT 编程注意事项](programming-considerations-for-usbprint.md)

 

 




