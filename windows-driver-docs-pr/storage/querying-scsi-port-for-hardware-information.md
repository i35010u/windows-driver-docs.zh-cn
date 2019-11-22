---
title: 查询 SCSI 端口以获取硬件信息
description: 查询 SCSI 端口以获取硬件信息
ms.assetid: 2f3adc40-6e5a-4a70-8298-60359b77f04f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cefec842b0c88ad27a6ffc32fa83fcfadb12c94
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842721"
---
# <a name="querying-scsi-port-for-hardware-information"></a>查询 SCSI 端口以获取硬件信息


## <span id="ddk_querying_scsi_port_for_hardware_information_kg"></span><span id="DDK_QUERYING_SCSI_PORT_FOR_HARDWARE_INFORMATION_KG"></span>


存储类驱动程序和其他更高级别的驱动程序可以通过查询-属性请求（[**IOCTL\_存储\_query\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)）查询 SCSI 端口，以获取有关设备和主机总线适配器功能的信息。 查询属性请求是旧系统中查询和功能请求的 PnP 等效项（[**IOCTL\_scsi\_获取\_查询\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_get_inquiry_data)和[**IOCTL\_SCSI\_获取\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_get_capabilities)). 对于存储设备，SCSI 端口返回存储设备描述符（[**存储\_设备\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_device_descriptor)），其中包含 SCSI 查询数据或非 SCSI 等效项; 对于主机适配器，scsi 端口返回包含功能和限制数据的存储适配器描述符（[**存储\_适配器\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_adapter_descriptor)）。

更高级别的驱动程序必须使用查询属性请求将[**存储\_属性\_查询**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_property_query)结构传递到 SCSI 端口。 如果较高级别的驱动程序**已将存储**\_属性\_查询设置为**StorageAdapterProperty**，则 SCSI 端口返回存储适配器描述符。 如果较高级别的驱动程序已将**QueryType**成员设置为**StorageDeviceProperty**，则 SCSI 端口将返回存储设备描述符。

如果较高级别的驱动程序将查询属性请求 IRP 发送到适配器的 FDO，并将**QueryType**设置为**StorageDeviceProperty**，则 SCSI 端口将无法使用 irp。 如果类驱动程序在**QueryType**设置为**StorageAdapterProperty**的情况下将此 irp 发送到设备的 PDO，SCSI 端口会将 IRP 转发到适配器 FDO。

有关存储设备描述符和存储适配器描述符的详细说明，请参阅[存储类驱动程序的 GetDescriptor 例程](storage-class-driver-s-getdescriptor-routine.md)，以及[**存储\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_property_query)的参考页面\_查询，[**存储\_设备\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_device_descriptor)和[**存储\_适配器\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_adapter_descriptor)。

 

 




