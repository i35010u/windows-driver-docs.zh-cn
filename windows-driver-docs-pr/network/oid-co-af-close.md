---
title: OID_CO_AF_CLOSE
description: 本主题介绍 OID_CO_AF_CLOSE 对象标识符 (OID)。
ms.assetid: 451ab9d5-e118-41c9-8d16-02d75a25a1d4
keywords:
- OID_CO_AF_CLOSE
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: f721fe5a63f4859ded6bf76744a6f3c605569dfa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357668"
---
# <a name="oidcoafclose"></a>OID_CO_AF_CLOSE

必须先取消绑定本身从基础的微型端口驱动程序的调用管理器，即可发送 OID_CO_AF_CLOSE OID。 正在取消绑定本身从微型端口驱动程序之前调用管理器将此 OID 发送到已打开与呼叫管理器的地址族每个客户端。 在响应中，客户端应执行以下操作：

1. 如果客户端有任何活动的多点连接，调用[NdisClDropParty](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscldropparty)尽可能多地需要前一个参与方在每个 multipoint VC 上保持活动状态

2. 调用[NdisClCloseCall](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclclosecall)尽可能多地需要关闭所有调用仍处于打开与调用管理器

3. 调用[NdisClDeregisterSap](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclderegistersap)尽可能多地需要取消注册所有客户端已注册到调用管理器的 SAPs

4. 调用[NdisClCloseAddressFamily](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclcloseaddressfamily)关闭由 NdisAfHandle 引用包含 OID_CO_AF_CLOSE 在请求中的地址族

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

