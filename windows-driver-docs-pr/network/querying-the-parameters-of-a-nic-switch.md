---
title: 查询 NIC 交换机的参数
description: 查询 NIC 交换机的参数
ms.assetid: 8C1F0F8A-D290-4552-A324-062DB92F6B5D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aeb951330ff4b8d3dab1802391cd7d1d4dee0da8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379201"
---
# <a name="querying-the-parameters-of-a-nic-switch"></a>查询 NIC 交换机的参数


基础驱动程序或用户应用程序可以获得可支持单根 I/O 虚拟化 (SR-IOV) 的网络适配器上已创建的 NIC 开关的参数。 驱动程序或应用程序发出的对象标识符 (OID) 方法请求[OID\_NIC\_交换机\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-parameters)来获取这些参数。

过量的驱动程序或用户应用程序会发出此 OID 方法请求之前，必须将格式化[ **NDIS\_NIC\_交换机\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构。 驱动程序或应用程序必须设置**SwitchId**成员添加到 NIC 开关的参数为要返回的标识符。

**请注意**  从 Windows Server 2012 开始，SR-IOV 接口只支持一个 NIC 切换上的网络适配器。 此交换机被称为*默认 NIC 开关*，并引用的 NDIS\_默认\_切换\_ID 标识符。

 

通过此 OID 方法请求成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_NIC\_交换机\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构。 此结构包含用于指定开关参数。

NDIS 句柄[OID\_NIC\_交换机\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-parameters)微型端口驱动程序的请求。 NDIS 从它所维护以下来源的数据的内部缓存中返回的信息：

-   在注册表中的标准化的 SR-IOV 关键字设置。 有关这些关键字的详细信息，请参阅[SR-IOV 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

-   OID 请求[OID\_NIC\_交换机\_创建\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)并[OID\_NIC\_交换机\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-parameters).

 

 





