---
title: 硬件信息的查询 Storport
description: 硬件信息的查询 Storport
ms.assetid: 1e807e42-d03f-44be-a0a4-8187e2d5667a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27a746adc7e6fd5983e963906fd6ffc5e8344e42
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520954"
---
# <a name="querying-storport-for-hardware-information"></a>硬件信息的查询 Storport


存储类驱动程序和其他更高级别的驱动程序可以查询设备的功能信息 Storport 和查询属性请求通过主机总线适配器 ([**IOCTL\_存储\_查询\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff560590))。 查询属性请求是旧系统中查询和功能请求的即插即用等效项 ([**IOCTL\_SCSI\_获取\_查询\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff560509)并[ **IOCTL\_SCSI\_获取\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff560502))。 对于存储设备，Storport 返回存储设备描述符 ([**存储\_设备\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff566971)) 包含 SCSI 查询数据或非 SCSI 等效项，以及承载的适配器 Storport 返回存储适配器说明符 ([**存储\_适配器\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff566346)) 包含的功能和限制的数据。

更高级别的驱动程序必须通过[**存储\_属性\_查询**](https://msdn.microsoft.com/library/windows/hardware/ff566997) Storport 到与查询属性请求的结构。 如果已设置的更高级别的驱动程序**PropertyId**的成员**存储\_属性\_查询**到**StorageAdapterProperty**，Storport返回存储适配器描述符。 如果已设置更高级别的驱动程序**PropertyId**成员添加到**StorageDeviceProperty**，Storport 返回存储设备描述符。

如果更高级别的驱动程序发送的查询属性请求对与适配器的 FDO IRP **PropertyId**设置为**StorageDeviceProperty**，Storport 失败 IRP。 如果类驱动程序会将此 IRP 发送到设备的 PDO **PropertyId**设置为**StorageAdapterProperty**，Storport 将转发到适配器 FDO IRP。

有关存储设备描述符和存储适配器描述符的详细说明，请参阅[存储类驱动程序 GetDescriptor 例程](storage-class-driver-s-getdescriptor-routine.md)，并参考页[**存储\_属性\_查询**](https://msdn.microsoft.com/library/windows/hardware/ff566997)， [**存储\_设备\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff566971)，和[ **存储\_适配器\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff566346)。

 

 




