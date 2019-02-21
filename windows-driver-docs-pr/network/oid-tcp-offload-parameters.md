---
title: OID_TCP_OFFLOAD_PARAMETERS
description: 本主题介绍 OID_TCP_OFFLOAD_PARAMETERS 对象标识符 (OID)。
ms.assetid: 5D9B5F62-E506-4983-B247-A93B81E70A43
keywords:
- OID_TCP_OFFLOAD_PARAMETERS，WDK Oid，WDK，WDK 网络 Oid 的网络对象标识符
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: be54f424f8b0d421e046f6bf7a495cd8fe01cd61
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544232"
---
# <a name="oidtcpoffloadparameters"></a>OID_TCP_OFFLOAD_PARAMETERS

不支持查询请求。

Set 请求，作为 OID_TCP_OFFLOAD_PARAMETERS OID 设置微型端口适配器的当前 TCP 卸载配置。 协议驱动程序或用户模式应用程序可以设置要更改当前的 TCP 卸载配置此 OID。 通过 Microsoft Windows Management Instrumentation (WMI) 界面，系统管理员可以使用此 OID。

## <a name="remarks"></a>备注

OID_TCP_OFFLOAD_PARAMETERS 是支持 TCP 卸载的微型端口驱动程序的必需和可选的其他微型端口驱动程序。 如果微型端口驱动程序不支持此 OID，则驱动程序应返回 NDIS_STATUS_NOT_SUPPORTED。

**InformationBuffer**的成员[NDIS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含[NDIS_OFFLOAD_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff566706)结构。 如果的内容**InformationBuffer**是否无效，微型端口驱动程序应返回 NDIS_STATUS_INVALID_DATA 以响应此 OID。

虽然 NDIS 处理此 OID，并将 OID 传递给微型端口驱动程序之前，NDIS 更新微型端口适配器的卸载标准化的关键字使用新的设置。

微型端口驱动程序必须使用的内容[NDIS_OFFLOAD_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff566706)结构，以更新当前报告的 TCP 卸载功能。 更新后，微型端口驱动程序必须报告的当前任务卸载能力[NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md)状态指示。 此状态指示可确保所有基础协议驱动程序使用新的功能信息更新。

此 OID 是一个更全面的 OID，指示启用或禁用某些卸载微型端口驱动程序。 可以配置大多数 TCP/IP 任务卸载，并将其激活此 OID。 对于某些卸载功能，例如 Rx 校验和或 Rx IPSec 此 OID 充当配置更改，并不意味着卸载将立即运行。 若要激活这些卸载，微型端口驱动程序必须等待，直到收到[OID_OFFLOAD_ENCAPSULATION](oid-offload-encapsulation.md)集请求。

在之前设置 OID_TCP_OFFLOAD_PARAMETERS，过量的应用程序或驱动程序可以使用[OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES](oid-tcp-offload-hardware-capabilities.md) OID 来确定微型端口适配器的硬件能够支持哪些功能。 使用 OID_TCP_OFFLOAD_PARAMETERS 以启用报告功能为未通过启用[OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md) OID。

### <a name="see-also"></a>另请参阅

[NDIS_OFFLOAD_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff566706)  
[NDIS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/ff566710)  
[NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md)  
[OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)  
[OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES](oid-tcp-offload-hardware-capabilities.md)

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 版本 | Windows Vista 及更高版本 |
| 标头 | Ntddndis.h （包括 Ndis.h） |

