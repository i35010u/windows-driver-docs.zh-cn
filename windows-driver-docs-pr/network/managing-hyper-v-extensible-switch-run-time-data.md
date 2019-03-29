---
title: 管理 Hyper-V 可扩展交换机运行时数据
description: 管理 Hyper-V 可扩展交换机运行时数据
ms.assetid: 08A353F5-D8CB-4645-9337-8169D302F6F2
ms.date: 12/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5004c44a7205702b5dbc4d57b16a7309ae0a6734
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565983"
---
# <a name="managing-hyper-v-extensible-switch-run-time-data"></a>管理 Hyper-V 可扩展交换机运行时数据

本主题介绍了保存和还原的 HYPER-V 可扩展交换机扩展的操作。 这些操作中，要保存并还原单个可扩展交换机网络 adapters(NICs) 的运行时数据的扩展。 这些操作执行时所具有的网络适配器连接到可扩展交换机端口的 HYPER-V 子分区启动或停止。

## <a name="saving-hyper-v-extensible-switch-run-time-data"></a>保存的 HYPER-V 可扩展交换机运行时数据

本部分中描述的 HYPER-V 可扩展交换机扩展可以将单个网络适配器 (Nic) 的运行时数据保存所依据的操作。 正在停止连接到可扩展交换机端口的网络适配器的 HYPER-V 子分区或正在保存其状态时执行此操作。

### <a name="handling-the-oidswitchnicsave-request"></a>处理 OID\_交换机\_NIC\_将请求保存

当连接到可扩展交换机端口的网络适配器的 HYPER-V 子分区已停止或保存其状态时，将通知 HYPER-V 可扩展交换机接口。 这将导致发出的对象标识符 (OID) 方法请求的可扩展交换机的协议边缘[OID\_切换\_NIC\_保存](https://msdn.microsoft.com/library/windows/hardware/hh598268)向下可扩展交换机驱动程序堆栈。 可扩展交换机扩展接收此 OID 请求时，它可以保存附加到子分区指定的网络适配器连接其运行时数据。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构[OID\_开关\_NIC\_保存](https://msdn.microsoft.com/library/windows/hardware/hh598268)请求包含一个指向[ **NDIS\_开关\_NIC\_保存\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598216)结构。 此结构是由可扩展交换机的协议边缘分配并初始化如下所示：

-   **标头**成员初始化为包含当前类型 revisionof [ **NDIS\_开关\_NIC\_保存\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598216)结构。 大小设置为已满缓冲区大小。

-   **PortId**成员包含可扩展交换机端口的唯一标识符，用于保存正在执行的操作。

当它收到[OID\_交换机\_NIC\_保存](https://msdn.microsoft.com/library/windows/hardware/hh598268)方法请求，该扩展执行以下操作：

1.  扩展读取**PortId**的成员[ **NDIS\_开关\_NIC\_保存\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598216)结构。

2.  如果该扩展运行时数据，将保存为指定的 NIC，它将保存其数据内的[ **NDIS\_交换机\_NIC\_保存\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598216)结构开头*SaveDataOffset*从结构开始的字节数。 扩展然后完成 OID 方法请求使用 NDIS\_状态\_成功。

3.  如果[ **NDIS\_交换机\_NIC\_保存\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598216)结构不提供足够的缓冲区来存放的运行时状态，该扩展扩展设置的方法结构*BytesNeeded*字段**NDIS\_SIZEOF\_NDIS\_开关\_NIC\_保存\_状态\_修订\_1**缓冲区保存在保存所需量以及数据，并完成与 OID **NDIS\_状态\_缓冲区\_太\_短**。 OID 将与所需的大小重新颁发。

4.  如果扩展不具有运行时数据，将保存为指定的 NIC，它必须调用[ **NdisFOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561830)。 这 OID 方法将请求转发到可扩展交换机驱动程序堆栈中的基础驱动程序。 有关此过程的详细信息，请参阅[NDIS 筛选器驱动程序中筛选 OID 请求](filtering-oid-requests-in-an-ndis-filter-driver.md)。

如果该扩展运行时端口要保存的数据，保存运行时端口中的数据时，它必须遵循这些准则[ **NDIS\_交换机\_NIC\_保存\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598216)结构：

1.  扩展集**ExtensionId**成员添加到唯一标识该驱动程序的 GUID 值。
2.  扩展集**ExtensionFriendlyName**成员添加到驱动程序的名称。

    **请注意**  NDIS\_交换机\_扩展\_FRIENDLYNAME 数据类型是由类型定义[**如果\_盘点\_字符串**](https://msdn.microsoft.com/library/windows/hardware/hh451419)结构。 此结构定义的字符串不需要以 null 结尾。 但是，必须设置字符串的长度**长度**此结构的成员。 如果字符串以 NULL 结尾**长度**成员必须包括终止 NULL 字符。     

3.  扩展设置的关联与保存的运行时数据功能类时， **FeatureClassId**与唯一标识类的 GUID。

    **请注意**  扩展功能类不是与保存的运行时数据相关联的如果设置**FeatureClassId**为零。     

4.  扩展可将复制到运行时数据**SaveData**成员和集**SaveDataSize**大小 （字节） 的运行时数据的成员。

**请注意**  扩展不得更改**标头**或**PortId**的成员[ **NDIS\_交换机\_NIC\_保存\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598216)结构。 

OID 的方法请求[OID\_切换\_NIC\_保存](https://msdn.microsoft.com/library/windows/hardware/hh598268)最终由可扩展交换机的基础的微型端口边缘处理。 微型端口驱动程序后此 OID 方法请求已被转发给通过可扩展交换机驱动程序堆栈的微型端口驱动程序，完成 OID 请求使用 NDIS\_状态\_成功。 这会通知可扩展交换机的协议边缘可扩展交换机驱动程序堆栈中的所有扩展已被都查询的运行时端口数据。 可扩展交换机的协议边缘然后颁发的 OID 集请求[OID\_切换\_NIC\_保存\_完成](https://msdn.microsoft.com/library/windows/hardware/hh598269)完成保存操作。

### <a name="handling-the-oidswitchnicsavecomplete-request"></a>处理 OID\_交换机\_NIC\_保存\_完整的请求

当 HYPER-V 子分区的网络适配器连接到可扩展交换机端口已暂停或保存其状态后时，将通知 HYPER-V 可扩展交换机接口。 这将导致发出的对象标识符 (OID) 方法请求的可扩展交换机的协议边缘[OID\_切换\_NIC\_保存](https://msdn.microsoft.com/library/windows/hardware/hh598268)向下可扩展交换机驱动程序堆栈。 有关此过程的详细信息，请参阅[处理 OID\_交换机\_NIC\_保存请求](handling-the-oid-switch-nic-save-request.md)。

每个 HYPER-V 可扩展交换机扩展已保存其运行时数据，可扩展交换机的协议边缘通知基础扩展的保存操作已完成。 通过发出的 OID 集请求的协议边缘实现这[OID\_切换\_NIC\_保存\_完成](https://msdn.microsoft.com/library/windows/hardware/hh598269)向下可扩展交换机驱动程序堆栈。

**请注意**  可扩展交换机网络适配器连接启动保存操作运行时，另一个保存操作的同一个网络适配器连接将不会执行直到[OID\_交换机\_NIC\_保存\_完成](https://msdn.microsoft.com/library/windows/hardware/hh598269)发出请求。 但是，将保存在此期间，连接可能会发生其他网络适配器的操作。 

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构[OID\_开关\_NIC\_保存\_完成](https://msdn.microsoft.com/library/windows/hardware/hh598269)请求包含一个指向[ **NDIS\_交换机\_NIC\_保存\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598216)结构。 可扩展交换机的协议边缘分配了此结构。

当它收到的 OID 集请求[OID\_交换机\_NIC\_保存\_完成](https://msdn.microsoft.com/library/windows/hardware/hh598269)，扩展必须遵守以下原则：

-   该扩展不能修改[ **NDIS\_交换机\_NIC\_保存\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598216)与 OID 请求关联的结构。

-   扩展必须调用[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)通过可扩展交换机扩展堆栈此 OID 请求转发。 该扩展会 OID 请求必须失败。

    **请注意**  扩展应该监视此 OID 请求的完成状态。 扩展插件这样做是为了检测是否在保存操作已成功完成。     

OID 的方法请求[OID\_切换\_NIC\_保存\_完成](https://msdn.microsoft.com/library/windows/hardware/hh598269)最终由可扩展交换机的基础的微型端口边缘处理。 此 OID 方法请求已收到的微型端口边缘后, 完成 OID 请求使用 NDIS\_状态\_成功。 这会通知可扩展交换机的协议边缘可扩展交换机驱动程序堆栈中的所有扩展已都完成保存操作。

## <a name="restoring-hyper-v-extensible-switch-run-time-data"></a>还原的 HYPER-V 可扩展交换机运行时数据

当从暂停恢复 HYPER-V 子分区的网络适配器连接到可扩展交换机端口时，将通知 HYPER-V 可扩展交换机接口。 这将导致发出的对象标识符 (OID) 组请求的可扩展交换机的协议边缘[OID\_切换\_NIC\_还原](https://msdn.microsoft.com/library/windows/hardware/hh598267)向下可扩展交换机驱动程序堆栈。 扩展接收此 OID 请求时，它可以还原子分区所使用的可扩展交换机端口及其运行时数据。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构[OID\_开关\_NIC\_还原](https://msdn.microsoft.com/library/windows/hardware/hh598268)请求包含一个指向[ **NDIS\_开关\_NIC\_保存\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598216)结构。 可扩展交换机的协议边缘分配了此结构。

当它收到的 OID 集请求[OID\_切换\_NIC\_还原](https://msdn.microsoft.com/library/windows/hardware/hh598267)，可扩展交换机扩展必须首先确定它是否拥有的运行时数据。 通过将的值进行比较来扩展实现这**ExtensionId**的成员[ **NDIS\_开关\_NIC\_保存\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598216)结构与该扩展使用自己的 GUID 值。

如果该扩展拥有可扩展的交换机 NIC 的运行时数据，它可按以下方式恢复此数据：

1.  扩展可将复制中的运行时数据**SaveData**成员添加到驱动程序分配存储。

    **请注意**  的值**PortId**的成员[ **NDIS\_交换机\_NIC\_保存\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598216)结构可能不同于**PortId**处运行时数据已保存的时间值。 如果运行时数据从一个主机到另一个保存在实时迁移期间，这可能发生。 但是，在实时迁移期间保留的可扩展交换机 NIC 配置。 这样，扩展插件可以使用新的运行时数据还原到可扩展交换机 NIC **PortId**值。     

2.  扩展完成 OID 集请求使用 NDIS\_状态\_成功。

如果扩展不拥有指定的运行时数据，以保存，则扩展将调用[ **NdisFOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561830)。 这 OID 集将请求转发到可扩展交换机驱动程序堆栈中的基础驱动程序。 在这种情况下，该扩展不能修改[ **NDIS\_交换机\_NIC\_保存\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598216)与 OID 请求关联的结构。 有关如何将请求转发 OID 的详细信息，请参阅[NDIS 筛选器驱动程序中筛选 OID 请求](filtering-oid-requests-in-an-ndis-filter-driver.md)。

如果 OID 设置的请求[OID\_切换\_NIC\_还原](https://msdn.microsoft.com/library/windows/hardware/hh598267)已完成，但 NDIS\_状态\_成功后，可扩展交换机的协议边缘发出另一个OID 设置请求。 它接收此新 OID 集请求时，该扩展可以执行下列任一操作：

-   如果它拥有新的 OID 请求中的运行时数据，该扩展将还原中的其他运行时数据[ **NDIS\_交换机\_NIC\_保存\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598216)结构。 扩展然后完成 OID 请求使用 NDIS\_状态\_成功。

-   如果它不拥有新的 OID 请求中的运行时数据，则扩展将调用[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)转发此 OID 设置请求为基础驱动程序。

<a href="" id="oid-switch-nic-restore-complete"></a>[OID\_交换机\_NIC\_还原\_完成](https://msdn.microsoft.com/library/windows/hardware/hh846215)  
可扩展交换机接口发出信号发出可扩展 switchnetwork 适配器运行时数据的还原操作完成时此 OID 的可扩展交换机的协议边缘。

此 OID 请求通知的扩展的还原操作已完成仅对指定的可扩展交换机 nic。

有关此 OID 请求的详细信息，请参阅[OID\_交换机\_NIC\_还原\_完成](https://msdn.microsoft.com/library/windows/hardware/hh846215)。

**请注意**  如果[OID\_切换\_NIC\_还原](https://msdn.microsoft.com/library/windows/hardware/hh598267)可扩展交换机的微型端口边缘收到集请求时，它完成使用 NDIS OID 请求\_状态\_成功。 这会通知可扩展交换机的协议边缘没有扩展名拥有的运行时数据。 如果发生这种情况，可扩展交换机接口记录记录一个事件**ExtensionId**并**PortId**最初保存运行时的扩展插件的成员值端口数据。