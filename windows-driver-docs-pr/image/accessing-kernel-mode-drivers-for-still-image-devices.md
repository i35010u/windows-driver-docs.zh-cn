---
title: 访问适用于静态图像设备的内核模式驱动程序
description: 访问适用于静态图像设备的内核模式驱动程序
ms.assetid: f9216d3c-4930-4c26-8eac-6ee500b038e0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa0ffce7def107a1e63677b607513abd868100fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566969"
---
# <a name="accessing-kernel-mode-drivers-for-still-image-devices"></a>访问适用于静态图像设备的内核模式驱动程序





Microsoft 提供了基于 WDM 的内核模式驱动程序以支持仍映像设备连接到 SCSI 和 USB 总线。 这两个驱动程序支持插设备和提供服务的添加、 删除、 启动、 停止和创建插设备的注册表项。 此外，这两个驱动程序提供挂起和继续支持电源管理的设备的操作。

用户模式下仍映像微型驱动程序可以访问这些内核模式驱动程序通过调用[ **CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858)， **ReadFile**， **WriteFile**，和[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216) （Microsoft Windows SDK 文档中所述）。 **ReadFile**并**WriteFile**用于块数据传输。 具体而言， **ReadFile**调用以获取图像数据，并**WriteFile**用于将命令发送到接受命令用作数据流的设备。

然后再调用**ReadFile**， **Writefile**或[ **DeviceIoControl**](https://msdn.microsoft.com/library/windows/desktop/aa363216)，微型驱动程序必须调用[ **IStiDeviceControl::GetMyDevicePortName** ](https://msdn.microsoft.com/library/windows/hardware/ff542944)若要获取设备的端口名称，然后使用该端口名称作为参数[ **CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858)。

[SCSI 的驱动程序](scsi-driver.md)

[USB 驱动程序](usb-driver.md)

 

 




