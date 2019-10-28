---
title: 访问静止图像设备的内核模式驱动程序
description: 访问静止图像设备的内核模式驱动程序
ms.assetid: f9216d3c-4930-4c26-8eac-6ee500b038e0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1ae8d4ced83e66e002c6007f339fecf72614001
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840917"
---
# <a name="accessing-kernel-mode-drivers-for-still-image-devices"></a>访问静止图像设备的内核模式驱动程序





Microsoft 提供基于 WDM 的内核模式驱动程序，以支持连接到 SCSI 和 USB 总线的静止图像设备。 这两个驱动程序都支持即插即用设备，并提供服务，用于添加、删除、启动、停止和创建即插即用设备的注册表项。 此外，这两个驱动程序都提供对支持电源管理的设备的挂起和恢复操作。

用户模式静止图像微型驱动程序可以通过调用[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)、 **ReadFile**、 **WriteFile**和[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol) （如 Microsoft Windows SDK 文档中所述）访问这些内核模式驱动程序。 **ReadFile**和**WriteFile**用于块数据传输。 具体而言，将调用**ReadFile**来获取图像数据，并使用**WriteFile**将命令发送到接受作为数据流的命令的设备。

在调用**ReadFile**、 **Writefile**或[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)之前，微型驱动程序必须调用[**IStiDeviceControl：： GetMyDevicePortName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)以获取设备的端口名称，然后使用该端口名称作为参数到[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea).

[SCSI 驱动程序](scsi-driver.md)

[USB 驱动程序](usb-driver.md)

 

 




