---
title: 集合列表序列化帮助程序
description: 集合列表序列化帮助器函数由 v2 传感器驱动程序，用于执行序列化相关操作在传感器\_集合\_列表结构。
ms.assetid: 586FEDD7-6BA1-4E76-8E8D-E486F4711FAE
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: de8f12ff665197604096f632f043bacbc02e88f8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325317"
---
# <a name="collection-list-serialization-helpers"></a>集合列表序列化帮助程序


集合列表序列化帮助器函数用于 v2 传感器驱动程序，对执行序列化相关的操作[**传感器\_集合\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)结构。

传感器设备驱动程序软件接口 (DDSI) 一起使用的帮助器函数。 因为这些帮助器函数独立于体系结构的所以它可以安全地跨进程边界的数据传输使用它们。 例如，它是安全地给 DeviceIoControl 的调用期间使用这些帮助器函数。

**SerializationBufferAllocate**

通过传感器 DDSI 的使用情况

-   分配一个序列化的缓冲区，并返回指向缓冲区的指针。

备注

-   状态指示成功的缓冲区分配\_确定的值。 否则，返回相应的 NTSTATUS 错误代码。

**SerializationBufferFree**

通过传感器 DDSI 的使用情况

-   释放不再需要的序列化缓冲区。

备注

-   无。

**CollectionsListGetSerializedSize**

通过传感器 DDSI 的使用情况

-   检索序列化缓冲区的大小。

备注

-   为 ULONG 变量返回缓冲区大小。

**CollectionsListSerializeToBuffer**

通过传感器 DDSI 的使用情况

-   将写入[**传感器\_集合\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)到序列化缓冲区的信息。

备注

-   成功写入操作由状态\_确定的值。 否则，返回相应的 NTSTATUS 错误代码。

**CollectionsListAllocateBufferAndSerialize**

通过传感器 DDSI 的使用情况

-   分配一个序列化的缓冲区，并将写入[**传感器\_集合\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)到缓冲区的信息。

备注

-   如果缓冲区分配成功，则集合列表信息写入缓冲区。 否则为不执行写入操作并返回相应的 NTSTATUS 错误代码。

-   成功写入操作由状态\_确定的值。 否则，返回相应的 NTSTATUS 错误代码。

**CollectionsListDeserializeFromBuffer**

通过传感器 DDSI 的使用情况

-   读取[**传感器\_集合\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)源缓冲区中的信息。

备注

-   成功的读取的操作由状态\_确定的值。 否则，返回相应的 NTSTATUS 错误代码。

## <a name="requirements"></a>要求

|                          |                        |
|--------------------------|------------------------|
| 最低受支持的客户端 | Windows 8.1            |
| 最低受支持的服务器 | Windows Server 2012 R2 |
| Header                   | Sensorsutils.h         |

 

## <a name="related-topics"></a>相关主题


[帮助器函数的封送处理](marshalling-helper-functions.md)

 

 






