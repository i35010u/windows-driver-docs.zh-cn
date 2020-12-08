---
title: Windows 98 核心组件
description: Windows 98 核心组件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aef58338075ff87e0a526878867c5deab894666f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826343"
---
# <a name="windows-98-core-components"></a>Windows 98 核心组件





在 MIcrosoft Windows 98 上，静止图像核心组件如下图所示。

![阐释 windows 98 core 组件的示意图](images/stiwin98.png)

在服务器端，三个核心组件与 *sti.dll* 进行通信： *stimon.exe*、 *sti \_ci.dll* 和 *sticpl.cpl*。 这些组件分别为静止图像事件监视器、类安装程序和扫描仪和照相机控制面板应用程序。 仅当安装或删除了新的静止映像设备，并且调用 *sticpl.cpl* 时才会调用 *Sti \_ci.dll* 。

*Stimon.exe* 处理事件并与 *sti.dll* 通信，后者又与一个或多个用户模式的静止映像驱动程序 (USDs) ，该驱动程序在此图的左侧标记为 USD1、USD2 和 USD3。 每个用户模式驱动程序都与一种类型的内核模式驱动程序通信，具体取决于设备的总线连接。 对于 USB 设备，用户模式静止映像驱动程序与 noncomposite usb 设备的复合 usb 设备和 *usbscan.sys* 的 *usbscn9x.sys* 通信;对于 SCSI 设备，用户模式驱动程序与 *scsiscan.sys* 和 *scsimap.sys* 通信。

在客户端应用程序端，IHV 必须提供一个 TWAIN 数据源，该数据源在上图中显示为 " *供应商 ds*"，这是此组件的通用名称。 TWAIN 数据源是 TWAIN 扫描体系结构的一个组件，可与客户端上 *sti.dll* 的实例进行通信。 接下来， *sti.dll* 与 (USD1) 中的用户模式静止映像驱动程序通信，该驱动程序与前面讨论过的某个内核模式驱动程序通信。

 

 




