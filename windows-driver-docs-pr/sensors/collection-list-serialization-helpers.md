---
title: 集合列表序列化帮助程序
description: V2 传感器驱动程序使用集合列表序列化帮助器函数来执行对传感器\_集合\_列表结构的序列化相关操作。
ms.assetid: 586FEDD7-6BA1-4E76-8E8D-E486F4711FAE
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 222df31c118d39464502c139fd0e96d5e6d2f608
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842531"
---
# <a name="collection-list-serialization-helpers"></a>集合列表序列化帮助程序


V2 传感器驱动程序使用集合列表序列化帮助器函数来执行对[**传感器\_集合\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)结构的序列化相关操作。

Helper 函数与传感器设备驱动程序软件接口（DDSI）一起使用。 由于这些帮助器函数是独立于体系结构的，因此可以安全地将它们用于跨进程边界进行数据传输。 例如，在调用 DeviceIoControl 时，可以安全地使用这些帮助器函数。

**SerializationBufferAllocate**

传感器 DDSI 的使用情况

-   分配一个序列化缓冲区，并返回一个指向缓冲区的指针。

备注

-   成功的缓冲区分配由状态\_"确定" 值指示。 否则，将返回相应的 NTSTATUS 错误代码。

**SerializationBufferFree**

传感器 DDSI 的使用情况

-   释放不再需要的序列化缓冲区。

备注

-   无。

**CollectionsListGetSerializedSize**

传感器 DDSI 的使用情况

-   检索序列化缓冲区的大小。

备注

-   缓冲区大小作为 ULONG 变量返回。

**CollectionsListSerializeToBuffer**

传感器 DDSI 的使用情况

-   将[**传感器\_集合\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)信息写入序列化缓冲区。

备注

-   成功的写入操作由状态\_"确定" 值指示。 否则，将返回相应的 NTSTATUS 错误代码。

**CollectionsListAllocateBufferAndSerialize**

传感器 DDSI 的使用情况

-   分配序列化缓冲区，然后将[**传感器\_集合\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)信息写入缓冲区。

备注

-   如果缓冲区分配成功，则会将集合列表信息写入缓冲区。 否则，不执行写操作，并返回相应的 NTSTATUS 错误代码。

-   成功的写入操作由状态\_"确定" 值指示。 否则，将返回相应的 NTSTATUS 错误代码。

**CollectionsListDeserializeFromBuffer**

传感器 DDSI 的使用情况

-   读取[**传感器\_收集**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)源缓冲区中的列表信息\_列表信息。

备注

-   成功的读取操作由状态\_"确定" 值指示。 否则，将返回相应的 NTSTATUS 错误代码。

## <a name="requirements"></a>要求

|                          |                        |
|--------------------------|------------------------|
| 最低受支持的客户端 | Windows 8.1            |
| 最低受支持的服务器 | Windows Server 2012 R2 |
| 标头                   | Sensorsutils         |

 

## <a name="related-topics"></a>相关主题


[封送处理 helper 函数](marshalling-helper-functions.md)

 

 






