---
title: OID_CO_AF_CLOSE
description: 本主题介绍 OID_CO_AF_CLOSE 对象标识符 (OID)。
ms.assetid: 451ab9d5-e118-41c9-8d16-02d75a25a1d4
keywords:
- OID_CO_AF_CLOSE
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84abaf17253ba96ef7f43a410674a371520b0cd4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542907"
---
# <a name="oidcoafclose"></a>OID_CO_AF_CLOSE

必须先取消绑定本身从基础的微型端口驱动程序的调用管理器，即可发送 OID_CO_AF_CLOSE OID。 正在取消绑定本身从微型端口驱动程序之前调用管理器将此 OID 发送到已打开与呼叫管理器的地址族每个客户端。 在响应中，客户端应执行以下操作：

1. 如果客户端有任何活动的多点连接，调用[NdisClDropParty](https://msdn.microsoft.com/library/windows/hardware/ff561629)尽可能多地需要前一个参与方在每个 multipoint VC 上保持活动状态

2. 调用[NdisClCloseCall](https://msdn.microsoft.com/library/windows/hardware/ff561627)尽可能多地需要关闭所有调用仍处于打开与调用管理器

3. 调用[NdisClDeregisterSap](https://msdn.microsoft.com/library/windows/hardware/ff561628)尽可能多地需要取消注册所有客户端已注册到调用管理器的 SAPs

4. 调用[NdisClCloseAddressFamily](https://msdn.microsoft.com/library/windows/hardware/ff561626)关闭由 NdisAfHandle 引用包含 OID_CO_AF_CLOSE 在请求中的地址族

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 版本 | Windows Vista 及更高版本 |
| 标头 | Ntddndis.h （包括 Ndis.h） |

