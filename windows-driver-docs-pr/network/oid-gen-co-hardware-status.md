---
title: OID_GEN_CO_HARDWARE_STATUS
description: 本主题介绍) OID_GEN_CO_HARDWARE_STATUS 对象标识符 (OID。
keywords:
- OID_GEN_CO_HARDWARE_STATUS
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3917c7bc723ac06da5e1fb0d5e9e699373db7bac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834357"
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

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 

