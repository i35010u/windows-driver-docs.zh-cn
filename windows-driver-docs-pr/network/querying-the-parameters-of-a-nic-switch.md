---
title: 查询 NIC 交换机的参数
description: 查询 NIC 交换机的参数
ms.assetid: 8C1F0F8A-D290-4552-A324-062DB92F6B5D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8ebc8aab9f8bc57baf53403fae1713aefc98b0f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844878"
---
# <a name="querying-the-parameters-of-a-nic-switch"></a>查询 NIC 交换机的参数


覆盖驱动程序或用户应用程序可以获取在支持单一根 i/o 虚拟化（SR-IOV）的网络适配器上创建的 NIC 交换机的参数。 驱动程序或应用程序发出 OID\_NIC 的对象标识符（OID）方法请求[\_交换机\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-parameters)以获取这些参数。

在过量驱动程序或用户应用程序发出此 OID 方法请求之前，它必须[ **\_交换机\_参数结构初始化 NDIS\_NIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters) 。 驱动程序或应用程序必须将**SwitchId**成员设置为要为其返回参数的 NIC 交换机的标识符。

**注意**  从 Windows Server 2012 开始，sr-iov 接口仅支持网络适配器上的一个 NIC 交换机。 此开关称为*默认 NIC 交换机*，由 NDIS\_默认\_交换机\_ID 标识符引用。

 

成功从此 OID 方法请求返回后， [**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**ndis\_\_NIC 的指针\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构. 此结构包含指定开关的参数。

NDIS 处理[\_NIC 的 OID\_交换机\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-parameters)请求以获得微型端口驱动程序。 NDIS 从以下源中返回的数据的内部缓存返回信息：

-   注册表中的标准化 SR-IOV 关键字设置。 有关这些关键字的详细信息，请参阅[sr-iov 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

-   Oid\_NIC 的 OID 请求[\_交换机\_创建\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)和[OID\_nic\_SWITCH\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-parameters)。

 

 





