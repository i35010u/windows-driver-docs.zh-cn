---
title: OID_WDI_IHV_REQUEST
description: OID_WDI_IHV_REQUEST 用于转发 IHV 扩展性模块已发送到微型端口的信息。
ms.assetid: d5639def-ddde-4972-b331-46c0f768d155
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_IHV_REQUEST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6c1a559c619cfe80261ae9677829bbb8f6ab089b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387263"
---
# <a name="oidwdiihvrequest"></a>OID\_WDI\_IHV\_请求


OID\_WDI\_IHV\_请求用于转发 IHV 扩展性模块已发送到微型端口的信息。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| Port  | 否                       | 1                               |

 

此命令不会用任何任务序列化。 使用其他属性和与 M1-M3 的一项任务，则会序列化。

## <a name="command-parameter"></a>命令参数


| TLV                                                  | 允许多个 TLV 实例 | 可选 | 描述                                        |
|------------------------------------------------------|--------------------------------|----------|----------------------------------------------------|
| [**WDI\_TLV\_IHV\_DATA**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ihv-data) |                                | X        | IHV 扩展性模块中的信息。 |

 

## <a name="response-result"></a>响应结果


| TLV                                                  | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                 |
|------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_IHV\_DATA**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ihv-data) |                                | X        | 要发送到 IHV 扩展性模块的响应。 数据值将作为转发-为 IHV 扩展性模块。 |

 

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

 

 




