---
title: OID_GEN_CO_HARDWARE_STATUS
description: 本主题介绍 OID_GEN_CO_HARDWARE_STATUS 对象标识符（OID）。
ms.assetid: b846622a-a082-41e8-b32b-74c111b31f69
keywords:
- OID_GEN_CO_HARDWARE_STATUS
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7241b2a9568c895298bf587ab1d2442714e1f36c
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917963"
---
# <a name="oid_gen_co_hardware_status"></a>OID_GEN_CO_HARDWARE_STATUS

OID_GEN_CO_HARDWARE_STATUS OID 指定基础 NIC 的当前硬件状态，作为以下 NDIS_HARDWARE_STATUS 类型值之一：

**NdisHardwareStatusReady**  
可以通过网络发送和接收数据。

**NdisHardwareStatusInitializing**  
正在初始化。

**NdisHardwareStatusReset**  
重置.

**NdisHardwareStatusClosing**  
Closing。

**NdisHardwareStatusNotReady**  
未就绪。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的**标头**： Ntddndis （包括 Ndis .h）

