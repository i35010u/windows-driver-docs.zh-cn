---
title: Windows 98 核心组件
description: Windows 98 核心组件
ms.assetid: 59e2c077-c6f5-4965-891b-4601623ca47b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d32b49806477a1b3dcf10cb6bccd73b20a4421cd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563473"
---
# <a name="windows-98-core-components"></a>Windows 98 核心组件





MIcrosoft Windows 98 上仍的图像核心组件是在下图中所示。

![说明 windows 98 核心组件的关系图](images/stiwin98.png)

三个核心组件与服务器端的通信*sti.dll*: *stimon.exe*， *sti\_ci.dll*，和*sticpl.cpl*. 这些组件分别是静止图像事件监视器，类安装程序中和扫描仪和照相机控制面板应用程序。 *Sti\_ci.dll*仅当安装或删除，新的静态图像设备时，才调用并*sticpl.cpl*调用仅来执行配置零碎工作。

*Stimon.exe*处理事件，并与通信*sti.dll*，这反过来与其中一个进行通信或更多用户模式下仍图像 USD1、 USD2 和在此图左侧 USD3 标记为驱动程序 (USDs)。 每个用户模式驱动程序与一种类型的内核模式驱动程序，具体取决于设备的总线连接进行通信。 对于 USB 设备，用户模式下仍映像驱动程序与进行通信*usbscn9x.sys*复合 usb 设备并*usbscan.sys* noncomposite usb 设备的; 对于 SCSI 设备，用户模式驱动程序两个通信*scsiscan.sys*并*scsimap.sys*。

在客户端应用程序端，IHV 必须提供 TWAIN 数据源，为上图中所示*vendor.ds*，此组件有通用名称。 TWAIN 数据源组成部分 TWAIN 扫描体系结构，并与实例进行通信*sti.dll*客户端上。 依次*sti.dll*与用户模式下仍映像驱动程序进行通信 (USD1 图中的)，这与前面所述的内核模式驱动因素之一进行通信。

 

 




