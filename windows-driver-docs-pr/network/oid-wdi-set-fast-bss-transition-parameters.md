---
title: OID_WDI_SET_FAST_BSS_TRANSITION_PARAMETERS
description: OID_WDI_SET_FAST_BSS_TRANSITION_PARAMETERS NDIS_STATUS_WDI_INDICATION_FT_ASSOC_PARAMS_NEEDED 响应发送。 已发送 (Re) 所必需的参数关联的请求。 作为直接 OID 情况下，将命令发送到该驱动程序。
ms.assetid: D769E49D-C565-41CD-9C91-195B1223AE66
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_FAST_BSS_TRANSITION_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: a0a4099a4aec594c70bebeaca39582a1cfb8e9a7
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903609"
---
# <a name="oidwdisetfastbsstransitionparameters"></a>OID\_WDI\_SET\_FAST\_BSS\_TRANSITION\_PARAMETERS


OID\_WDI\_设置\_快速\_BSS\_转换\_参数发送到响应中[NDIS\_状态\_WDI\_指示\_FT\_ASSOC\_PARAMS\_需执行](ndis-status-wdi-indication-ft-assoc-params-needed.md)。 已发送 (Re) 所必需的参数关联的请求。 作为直接 OID 情况下，将命令发送到该驱动程序。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| 端口  | 否                       | 1                               |

 

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                  | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                                                                                                                                    |
|------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_STATUS**](https://msdn.microsoft.com/library/windows/hardware/dn898068)      |                                |          | 此状态为成功，其余字段 RSNIE、 MDE （FTE） 存在。 这表示没有任何问题或错误的身份验证响应 （例如，MIC 检查失败），IHV 可以继续重新关联请求。 |
| [**WDI\_TLV\_FT\_RSNIE**](https://msdn.microsoft.com/library/windows/hardware/mt269125) |                                | X        | RSN IE 字节 blob。                                                                                                                                                                                                                                          |
| [**WDI\_TLV\_FT\_MDE**](https://msdn.microsoft.com/library/windows/hardware/mt269120)     |                                | X        | MDE 字节 blob。                                                                                                                                                                                                                                             |
| [**WDI\_TLV\_FT\_FTE**](https://msdn.microsoft.com/library/windows/hardware/mt269118)     |                                | X        | FTE 字节 blob。                                                                                                                                                                                                                                             |

 

## <a name="set-property-results"></a>设置属性结果


没有其他数据。 标头中的数据就足够了。

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

 

 




