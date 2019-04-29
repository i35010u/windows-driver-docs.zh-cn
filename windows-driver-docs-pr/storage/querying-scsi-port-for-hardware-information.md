---
title: 查询 SCSI 端口以获取硬件信息
description: 查询 SCSI 端口以获取硬件信息
ms.assetid: 2f3adc40-6e5a-4a70-8298-60359b77f04f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e567adf2764ba2962acc8fad0d13eb6091ad30d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360872"
---
# <a name="querying-scsi-port-for-hardware-information"></a>查询 SCSI 端口以获取硬件信息


## <span id="ddk_querying_scsi_port_for_hardware_information_kg"></span><span id="DDK_QUERYING_SCSI_PORT_FOR_HARDWARE_INFORMATION_KG"></span>


存储类驱动程序和其他更高级别的驱动程序可以查询 SCSI 端口有关的功能的设备的信息和查询属性请求通过主机总线适配器 ([**IOCTL\_存储\_查询\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff560590))。 查询属性请求是旧系统中查询和功能请求的即插即用等效项 ([**IOCTL\_SCSI\_获取\_查询\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff560509)并[ **IOCTL\_SCSI\_获取\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff560502))。 对于存储设备 SCSI 端口返回存储设备描述符 ([**存储\_设备\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff566971)) 包含 SCSI 查询数据或非 SCSI 等效项，以及承载的适配器 SCSI 端口返回存储适配器说明符 ([**存储\_适配器\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff566346)) 包含的功能和限制的数据。

更高级别的驱动程序必须通过[**存储\_属性\_查询**](https://msdn.microsoft.com/library/windows/hardware/ff566997) SCSI 端口与查询属性请求的结构。 如果已设置的更高级别的驱动程序**QueryType**的存储空间的成员\_属性\_查询到**StorageAdapterProperty**，SCSI 端口返回存储适配器描述符。 如果已设置更高级别的驱动程序**QueryType**成员添加到**StorageDeviceProperty**，SCSI 端口返回存储设备描述符。

如果更高级别的驱动程序发送的查询属性请求对与适配器的 FDO IRP **QueryType**设置为**StorageDeviceProperty**，SCSI 端口无法正常工作 IRP。 如果类驱动程序会将此 IRP 发送到设备的 PDO **QueryType**设置为**StorageAdapterProperty**，SCSI 端口转发到适配器 FDO IRP。

有关存储设备描述符和存储适配器描述符的详细说明，请参阅[存储类驱动程序 GetDescriptor 例程](storage-class-driver-s-getdescriptor-routine.md)，并参考页[**存储\_属性\_查询**](https://msdn.microsoft.com/library/windows/hardware/ff566997)， [**存储\_设备\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff566971)，和[ **存储\_适配器\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff566346)。

 

 




