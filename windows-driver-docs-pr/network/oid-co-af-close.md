---
title: OID_CO_AF_CLOSE
description: 本主题介绍) OID_CO_AF_CLOSE 对象标识符 (OID。
ms.assetid: 451ab9d5-e118-41c9-8d16-02d75a25a1d4
keywords:
- OID_CO_AF_CLOSE
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: be3e4fdbe1c2658f01b3e952163e178789060c09
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214650"
---
# <a name="oid_co_af_close"></a>OID_CO_AF_CLOSE

OID_CO_AF_CLOSE OID 由呼叫管理器发送，该管理器必须从基础微型端口驱动程序对其自身进行解除绑定。 从微型端口驱动程序取消绑定自身之前，呼叫管理器会将此 OID 发送到使用呼叫管理器打开地址族的每个客户端。 作为响应，客户端应执行以下操作：

1. 如果客户端有任何活动的 multipoint 连接，则根据需要调用 [NdisClDropParty](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscldropparty) 多次，直到每个 multipoint VC 上只有一个参与方处于活动状态

2. 按需多次调用 [NdisClCloseCall](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall) ，以关闭仍通过呼叫管理器打开的所有呼叫

3. 按需多次调用 [NdisClDeregisterSap](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclderegistersap) ，以取消注册客户端已向呼叫管理器注册的所有 sap

4. 调用 [NdisClCloseAddressFamily](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclcloseaddressfamily) ，关闭包含 OID_CO_AF_CLOSE 的请求中的 NdisAfHandle 引用的地址族。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 