---
title: 枚举的网络适配器上的 NIC 开关
description: 枚举的网络适配器上的 NIC 开关
ms.assetid: 0799A879-2BC0-43C5-A6B6-6D46C74A26FB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5066ebde7ac30d395c459da0faa64e7993d01c2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523445"
---
# <a name="enumerating-nic-switches-on-a-network-adapter"></a>枚举的网络适配器上的 NIC 开关


基础驱动程序或用户应用程序可以获取已在支持单个根 I/O 虚拟化 (SR-IOV) 的网络适配器创建的所有 NIC 交换机的列表。 驱动程序或应用程序发出的对象标识符 (OID) 查询请求[OID\_NIC\_交换机\_枚举\_开关](https://msdn.microsoft.com/library/windows/hardware/hh451819)来获取此列表。

通过此 OID 请求成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含指向包含如下内容的缓冲区：

-   [ **NDIS\_NIC\_交换机\_信息\_数组**](https://msdn.microsoft.com/library/windows/hardware/hh451577)结构，用于定义数组中元素数。

-   一个数组[ **NDIS\_NIC\_交换机\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451582)结构。 每个这些结构包含有关网络适配器上创建一个 NIC 交换机的信息。

    **请注意**  如果网络适配器不具有任何 NIC 开关，该驱动程序集**NumElements**的成员[ **NDIS\_NIC\_交换机\_INFO\_数组**](https://msdn.microsoft.com/library/windows/hardware/hh451577)为零，并无结构[ **NDIS\_NIC\_交换机\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451582)返回的结构。

     

**请注意**  从 Windows Server 2012 开始，SR-IOV 接口只支持一个 NIC 切换上的网络适配器。 此交换机被称为*默认 NIC 开关*，并引用的 NDIS\_默认\_切换\_ID 标识符。

 

NDIS 句柄[OID\_NIC\_交换机\_枚举\_开关](https://msdn.microsoft.com/library/windows/hardware/hh451819)微型端口驱动程序的请求。 NDIS 从它所维护以下来源的数据的内部缓存中返回的信息：

-   在注册表中的标准化的 SR-IOV 关键字设置。 有关这些关键字的详细信息，请参阅[SR-IOV 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

-   OID 请求[OID\_NIC\_交换机\_创建\_开关](https://msdn.microsoft.com/library/windows/hardware/hh451815)并[OID\_NIC\_交换机\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451823).

**请注意**  NDIS 还提供了枚举中的交换机**NicSwitchArray**中的成员[ **NDIS\_绑定\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff564832)并[ **NDIS\_筛选器\_附加\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff565481)结构。 因此，如果选择的协议和筛选器驱动程序没有颁发[OID\_NIC\_交换机\_枚举\_开关](https://msdn.microsoft.com/library/windows/hardware/hh451819)请求获取此信息。

 

 

 





