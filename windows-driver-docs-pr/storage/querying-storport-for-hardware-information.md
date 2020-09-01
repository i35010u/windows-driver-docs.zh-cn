---
title: 查询 Storport 以获取硬件信息
description: 查询 Storport 以获取硬件信息
ms.assetid: 1e807e42-d03f-44be-a0a4-8187e2d5667a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa58c62ca41c524c0c84755594f313abd394daae
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184373"
---
# <a name="querying-storport-for-hardware-information"></a>查询 Storport 以获取硬件信息


存储类驱动程序和其他更高级别的驱动程序可以通过查询属性请求 ([**IOCTL \_ 存储 \_ 查询 \_ 属性**](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)) 来查询 Storport 的设备和主机总线适配器功能的信息。 查询属性请求是旧系统中查询和功能请求的 PnP 等效项 ([**IOCTL \_ scsi \_ 获取 \_ 查询 \_ 数据**](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_get_inquiry_data) 和 [**ioctl \_ scsi \_ get \_ 功能**](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_get_capabilities)) 。 对于存储设备，Storport 返回存储设备描述符 ([**存储 \_ 设备 \_ 描述符**](/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_device_descriptor)) 包含 SCSI 查询数据或非 SCSI 等效项，而对于主机适配器 storport，返回存储适配器描述符 (包含功能和限制数据的存储) [** \_ 适配器 \_ **](/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_adapter_descriptor) 描述符。

更高级别的驱动程序必须使用查询属性请求将 [**存储 \_ 属性 \_ 查询**](/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_property_query) 结构传递到 Storport。 如果较高级别的驱动程序已将**存储 \_ 属性 \_ 查询**的**PropertyId**成员设置为**StorageAdapterProperty**，则 Storport 返回存储适配器描述符。 如果较高级别的驱动程序已将 **PropertyId** 成员设置为 **StorageDeviceProperty**，则 Storport 返回存储设备描述符。

如果较高级别的驱动程序将查询属性请求 IRP 发送到适配器的 FDO，并将 **PropertyId** 设置为 **StorageDeviceProperty**，则 STORPORT 将无法使用 irp。 如果类驱动程序将此 IRP 发送到 **PropertyId** 设置为 **StorageAdapterProperty**的设备的 PDO，则 Storport 会将 IRP 转发到适配器 FDO。

有关存储设备描述符和存储适配器描述符的详细说明，请参阅 [存储类驱动程序的 GetDescriptor 例程](storage-class-driver-s-getdescriptor-routine.md)，以及 [**存储 \_ 属性 \_ 查询**](/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_property_query)、 [**存储 \_ 设备 \_ 描述符**](/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_device_descriptor)和 [**存储 \_ 适配器 \_ 描述符**](/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_adapter_descriptor)的参考页。

 

