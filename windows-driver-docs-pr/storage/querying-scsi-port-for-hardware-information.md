---
title: 查询 SCSI 端口以获取硬件信息
description: 查询 SCSI 端口以获取硬件信息
ms.assetid: 2f3adc40-6e5a-4a70-8298-60359b77f04f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7396a044933a1a211aa8651815660b1029e5d8b9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386290"
---
# <a name="querying-scsi-port-for-hardware-information"></a>查询 SCSI 端口以获取硬件信息


## <span id="ddk_querying_scsi_port_for_hardware_information_kg"></span><span id="DDK_QUERYING_SCSI_PORT_FOR_HARDWARE_INFORMATION_KG"></span>


存储类驱动程序和其他更高级别的驱动程序可以查询 SCSI 端口有关的功能的设备的信息和查询属性请求通过主机总线适配器 ([**IOCTL\_存储\_查询\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_query_property))。 查询属性请求是旧系统中查询和功能请求的即插即用等效项 ([**IOCTL\_SCSI\_获取\_查询\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ni-ntddscsi-ioctl_scsi_get_inquiry_data)并[ **IOCTL\_SCSI\_获取\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ni-ntddscsi-ioctl_scsi_get_capabilities))。 对于存储设备 SCSI 端口返回存储设备描述符 ([**存储\_设备\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_device_descriptor)) 包含 SCSI 查询数据或非 SCSI 等效项，以及承载的适配器 SCSI 端口返回存储适配器说明符 ([**存储\_适配器\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_adapter_descriptor)) 包含的功能和限制的数据。

更高级别的驱动程序必须通过[**存储\_属性\_查询**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_property_query) SCSI 端口与查询属性请求的结构。 如果已设置的更高级别的驱动程序**QueryType**的存储空间的成员\_属性\_查询到**StorageAdapterProperty**，SCSI 端口返回存储适配器描述符。 如果已设置更高级别的驱动程序**QueryType**成员添加到**StorageDeviceProperty**，SCSI 端口返回存储设备描述符。

如果更高级别的驱动程序发送的查询属性请求对与适配器的 FDO IRP **QueryType**设置为**StorageDeviceProperty**，SCSI 端口无法正常工作 IRP。 如果类驱动程序会将此 IRP 发送到设备的 PDO **QueryType**设置为**StorageAdapterProperty**，SCSI 端口转发到适配器 FDO IRP。

有关存储设备描述符和存储适配器描述符的详细说明，请参阅[存储类驱动程序 GetDescriptor 例程](storage-class-driver-s-getdescriptor-routine.md)，并参考页[**存储\_属性\_查询**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_property_query)， [**存储\_设备\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_device_descriptor)，和[ **存储\_适配器\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_adapter_descriptor)。

 

 




