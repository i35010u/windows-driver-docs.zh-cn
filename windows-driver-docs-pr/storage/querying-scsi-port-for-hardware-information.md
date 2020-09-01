---
title: 查询 SCSI 端口以获取硬件信息
description: 查询 SCSI 端口以获取硬件信息
ms.assetid: 2f3adc40-6e5a-4a70-8298-60359b77f04f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35557c18e2a4791bcd998e5040d59a667bcddc70
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185096"
---
# <a name="querying-scsi-port-for-hardware-information"></a>查询 SCSI 端口以获取硬件信息


## <span id="ddk_querying_scsi_port_for_hardware_information_kg"></span><span id="DDK_QUERYING_SCSI_PORT_FOR_HARDWARE_INFORMATION_KG"></span>


存储类驱动程序和其他更高级别的驱动程序可以通过查询属性请求 ([**IOCTL \_ 存储 \_ 查询 \_ 属性**](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)) 来查询 SCSI 端口，以获取有关设备和主机总线适配器功能的信息。 查询属性请求是旧系统中查询和功能请求的 PnP 等效项 ([**IOCTL \_ scsi \_ 获取 \_ 查询 \_ 数据**](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_get_inquiry_data) 和 [**ioctl \_ scsi \_ get \_ 功能**](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_get_capabilities)) 。 对于存储设备，SCSI 端口返回存储设备描述符 ([**存储设备 \_ \_ 描述符**](/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_device_descriptor)) 包含 SCSI 查询数据或非 SCSI 等效项; 对于主机适配器，scsi 端口返回存储适配器描述符 ([**存储 \_ 适配器 \_ 描述符**](/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_adapter_descriptor)) 包含功能和限制数据。

更高级别的驱动程序必须使用 QUERY 属性请求将 [**存储 \_ 属性 \_ 查询**](/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_property_query) 结构传递到 SCSI 端口。 如果较高级别的驱动程序已将存储属性查询的 **QueryType** 成员设置 \_ \_ 为 **StorageAdapterProperty**，则 SCSI 端口将返回存储适配器描述符。 如果较高级别的驱动程序已将 **QueryType** 成员设置为 **StorageDeviceProperty**，则 SCSI 端口将返回存储设备描述符。

如果较高级别的驱动程序将查询属性请求 IRP 发送到适配器的 FDO，并将 **QueryType** 设置为 **StorageDeviceProperty**，则 SCSI 端口将无法使用 irp。 如果类驱动程序在 **QueryType** 设置为 **StorageAdapterProperty**的情况下将此 irp 发送到设备的 PDO，SCSI 端口会将 IRP 转发到适配器 FDO。

有关存储设备描述符和存储适配器描述符的详细说明，请参阅 [存储类驱动程序的 GetDescriptor 例程](storage-class-driver-s-getdescriptor-routine.md)，以及 [**存储 \_ 属性 \_ 查询**](/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_property_query)、 [**存储 \_ 设备 \_ 描述符**](/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_device_descriptor)和 [**存储 \_ 适配器 \_ 描述符**](/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_adapter_descriptor)的参考页。

 

