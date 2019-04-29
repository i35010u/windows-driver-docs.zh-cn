---
title: OID_GEN_CO_HARDWARE_STATUS
description: 本主题介绍 OID_GEN_CO_HARDWARE_STATUS 对象标识符 (OID)。
ms.assetid: b846622a-a082-41e8-b32b-74c111b31f69
keywords:
- OID_GEN_CO_HARDWARE_STATUS
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e66f46a34e7f8afc5ac138ac7dfa0a3fcd5f0b6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379219"
---
# <a name="oidgencohardwarestatus"></a>OID_GEN_CO_HARDWARE_STATUS

OID_GEN_CO_HARDWARE_STATUS OID 指定的基础 NIC 的新的硬件状态作为以下 NDIS_HARDWARE_STATUS 类型值之一：

**NdisHardwareStatusReady**  
可用并能够发送和接收网络上的数据。

**NdisHardwareStatusInitializing**  
正在初始化。

**NdisHardwareStatusReset**  
正在重置。

**NdisHardwareStatusClosing**  
关闭。

**NdisHardwareStatusNotReady**  
未就绪。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

