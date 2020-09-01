---
title: OID_WDI_IHV_REQUEST
description: OID_WDI_IHV_REQUEST 用于转发 IHV 扩展性模块已发送到小型端口的信息。
ms.assetid: d5639def-ddde-4972-b331-46c0f768d155
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_IHV_REQUEST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 06571ab709af749f121bdfcade188bfb2b399ebb
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215835"
---
# <a name="oid_wdi_ihv_request"></a>OID \_ WDI \_ IHV \_ 请求


OID \_ WDI \_ ihv \_ 请求用于转发 IHV 扩展性模块已发送到小型端口的信息。

| 作用域 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 否                       | 1                               |

 

此命令不会与任何任务一起序列化。 它使用其他属性和任务的 M1-M3 进行序列化。

## <a name="command-parameter"></a>命令参数


| TLV                                                  | 允许多个 TLV 实例 | 可选 | 说明                                        |
|------------------------------------------------------|--------------------------------|----------|----------------------------------------------------|
| [**WDI \_ TLV \_ IHV \_ 数据**](./wdi-tlv-ihv-data.md) |                                | X        | 来自 IHV 扩展性模块的信息。 |

 

## <a name="response-result"></a>响应结果


| TLV                                                  | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                 |
|------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ IHV \_ 数据**](./wdi-tlv-ihv-data.md) |                                | X        | 要发送到 IHV 扩展性模块的响应。 数据值将按原样转发到 IHV 扩展模块。 |

 

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
<td><p>标头</p></td>
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

 

