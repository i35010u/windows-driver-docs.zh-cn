---
title: 集合列表序列化帮助程序
description: V2 传感器驱动程序使用集合列表序列化帮助器函数来对传感器 \_ 集合列表结构执行与序列化相关的操作 \_ 。
ms.assetid: 586FEDD7-6BA1-4E76-8E8D-E486F4711FAE
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: cccc10db6319bedd8706c6031b56547f9bbd4952
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010581"
---
# <a name="collection-list-serialization-helpers"></a>集合列表序列化帮助程序


V2 传感器驱动程序使用集合列表序列化帮助器函数来对 [**传感器 \_ 集合 \_ 列表**](/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list) 结构执行与序列化相关的操作。

Helper 函数与传感器设备驱动程序软件接口一起使用 (DDSI) 。 由于这些帮助器函数是独立于体系结构的，因此可以安全地将它们用于跨进程边界进行数据传输。 例如，在调用 DeviceIoControl 时，可以安全地使用这些帮助器函数。

**SerializationBufferAllocate**

传感器 DDSI 的使用情况

-   分配一个序列化缓冲区，并返回一个指向缓冲区的指针。

注释

-   成功的缓冲区分配由状态 \_ OK 值指示。 否则，将返回相应的 NTSTATUS 错误代码。

**SerializationBufferFree**

传感器 DDSI 的使用情况

-   释放不再需要的序列化缓冲区。

注释

-   无。

**CollectionsListGetSerializedSize**

传感器 DDSI 的使用情况

-   检索序列化缓冲区的大小。

注释

-   缓冲区大小作为 ULONG 变量返回。

**CollectionsListSerializeToBuffer**

传感器 DDSI 的使用情况

-   将 [**传感器 \_ 集合 \_ 列表**](/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list) 信息写入序列化缓冲区。

注释

-   成功的写入操作由状态 \_ OK 值指示。 否则，将返回相应的 NTSTATUS 错误代码。

**CollectionsListAllocateBufferAndSerialize**

传感器 DDSI 的使用情况

-   分配一个序列化缓冲区，然后将 [**传感器 \_ 集合 \_ 列表**](/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list) 信息写入缓冲区。

注释

-   如果缓冲区分配成功，则会将集合列表信息写入缓冲区。 否则，不执行写操作，并返回相应的 NTSTATUS 错误代码。

-   成功的写入操作由状态 \_ OK 值指示。 否则，将返回相应的 NTSTATUS 错误代码。

**CollectionsListDeserializeFromBuffer**

传感器 DDSI 的使用情况

-   从源缓冲区读取 [**传感器 \_ 集合 \_ 列表**](/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list) 信息。

注释

-   成功的读取操作由状态 \_ OK 值指示。 否则，将返回相应的 NTSTATUS 错误代码。

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 8。1

**支持的最低服务器**： Windows Server 2012 R2

**标头**： Sensorsutils


 

## <a name="related-topics"></a>相关主题


[帮助程序函数的封送处理](marshalling-helper-functions.md)

 

