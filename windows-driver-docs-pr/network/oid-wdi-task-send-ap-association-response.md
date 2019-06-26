---
title: OID_WDI_TASK_SEND_AP_ASSOCIATION_RESPONSE
description: OID_WDI_TASK_SEND_AP_ASSOCIATION_RESPONSE 请求 IHV 组件发送到对等设备最近发送的关联请求的关联响应。
ms.assetid: 8d19b009-db81-4b5e-ac63-5e6c5ad9727d
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_SEND_AP_ASSOCIATION_RESPONSE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 4c6f44fa3797de1b41ea76f413328f3dd03ef0a6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386212"
---
# <a name="oidwditasksendapassociationresponse"></a>OID\_WDI\_TASK\_SEND\_AP\_ASSOCIATION\_RESPONSE


OID\_WDI\_任务\_发送\_AP\_关联\_响应请求 IHV 组件发送到对等设备最近发送一个关联的关联响应请求。

| Object | 中止支持                                           | 默认优先级 （主机驱动程序策略） | 正常执行时间 （秒） |
|--------|---------------------------------------------------------|---------------------------------------|---------------------------------|
| Port   | 是。 端口必须保持干净状态后中止。 | 3                                     | 1                               |

 

如果发送由于任何原因失败，一个空[NDIS\_状态\_WDI\_指示\_发送\_AP\_关联\_响应\_完整](ndis-status-wdi-indication-send-ap-association-response-complete.md)会填充标头中包含的正确状态。

## <a name="task-parameters"></a>任务参数


| TLV                                                                                                      | 允许多个 TLV 实例 | 可选 | 描述                                                                                                      |
|----------------------------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_关联\_响应\_参数**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-association-response-parameters)      |                                |          | 关联响应参数。                                                                                 |
| [**WDI\_TLV\_VENDOR\_SPECIFIC\_IE**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-vendor-specific-ie)                                |                                | X        | 端口必须将追加到关联响应 IE 向对等方适配器发送响应之前设置的更多 Ie。 |
| [**WDI\_TLV\_传入\_关联\_请求\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-incoming-association-request-info) |                                |          | 传入关联请求有关的信息。                                                              |
| [**WDI\_TLV\_WFD\_关联\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-wfd-association-status)                        |                                | X        | 要设置关联请求被拒绝时的状态值。                                                  |

 

## <a name="task-completion-indication"></a>指示任务完成


[NDIS\_状态\_WDI\_指示\_发送\_AP\_关联\_响应\_完成](ndis-status-wdi-indication-send-ap-association-response-complete.md)

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




