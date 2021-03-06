---
title: 查询 NIC 交换机的参数
description: 查询 NIC 交换机的参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d973990b4a32fa4d8eed8b874da7e63af38a4434
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248611"
---
# <a name="querying-the-parameters-of-a-nic-switch"></a>查询 NIC 交换机的参数


覆盖驱动程序或用户应用程序可以获取 NIC 交换机的参数，这些参数在支持单个根 i/o 虚拟化 (SR-IOV) 的网络适配器上创建。 驱动程序或应用程序发出对象标识符 (OID) 方法请求 [oid \_ NIC \_ 交换机 \_ 参数](./oid-nic-switch-parameters.md) 以获取这些参数。

在过量驱动程序或用户应用程序发出此 OID 方法请求之前，它必须初始化 [**NDIS \_ NIC \_ 交换机 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters) 结构。 驱动程序或应用程序必须将 **SwitchId** 成员设置为要为其返回参数的 NIC 交换机的标识符。

**注意**  从 Windows Server 2012 开始，SR-IOV 接口仅支持网络适配器上的一个 NIC 交换机。 此开关称为 *默认 NIC 交换机*，由 NDIS \_ 默认 \_ 交换机 \_ ID 标识符引用。

 

成功从此 OID 方法请求返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ NIC \_ 交换机 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构的指针。 此结构包含指定开关的参数。

NDIS 处理微型端口驱动程序的 [OID \_ NIC \_ 交换机 \_ 参数](./oid-nic-switch-parameters.md) 请求。 NDIS 从以下源中返回的数据的内部缓存返回信息：

-   注册表中的标准化 SR-IOV 关键字设置。 有关这些关键字的详细信息，请参阅 [sr-iov 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

-   Oid [ \_ nic \_ 交换机 \_ 创建 \_ 交换机](./oid-nic-switch-create-switch.md) 和 [OID \_ nic \_ 交换机 \_ 参数](./oid-nic-switch-parameters.md)的 oid 请求。

 

