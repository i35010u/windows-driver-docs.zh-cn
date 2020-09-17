---
title: 访问适用于静态图像设备的内核模式驱动程序
description: 访问适用于静态图像设备的内核模式驱动程序
ms.assetid: f9216d3c-4930-4c26-8eac-6ee500b038e0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66f86fea14b8681c31accce2b9a7b7732e57a15b
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716792"
---
# <a name="accessing-kernel-mode-drivers-for-still-image-devices"></a>访问适用于静态图像设备的内核模式驱动程序





Microsoft 提供基于 WDM 的内核模式驱动程序，以支持连接到 SCSI 和 USB 总线的静止图像设备。 这两个驱动程序都支持即插即用设备，并提供服务，用于添加、删除、启动、停止和创建即插即用设备的注册表项。 此外，这两个驱动程序都提供对支持电源管理的设备的挂起和恢复操作。

用户模式静止图像微型驱动程序可以通过调用 Microsoft Windows SDK 文档) 中所述的 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea)、 **ReadFile**、 **WriteFile**和 [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) (来访问这些内核模式驱动程序。 **ReadFile** 和 **WriteFile** 用于块数据传输。 具体而言，将调用 **ReadFile** 来获取图像数据，并使用 **WriteFile** 将命令发送到接受作为数据流的命令的设备。

在调用 **ReadFile**、 **Writefile** 或 [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol)之前，微型驱动程序必须调用 [**IStiDeviceControl：： GetMyDevicePortName**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname) 以获取设备的端口名称，然后将该端口名称用作 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea)的参数。

[SCSI 驱动程序](scsi-driver.md)

[USB 驱动程序](usb-driver.md)

 

