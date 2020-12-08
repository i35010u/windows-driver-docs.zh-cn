---
title: OID_WDI_SET_FAST_BSS_TRANSITION_PARAMETERS
description: 为了响应 NDIS_STATUS_WDI_INDICATION_FT_ASSOC_PARAMS_NEEDED，将发送 OID_WDI_SET_FAST_BSS_TRANSITION_PARAMETERS。 它具有) 关联请求发送 (所需的参数。 命令作为直接 OID 发送到驱动程序。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_FAST_BSS_TRANSITION_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: c6d8a89ed6b7d2f292d0c812c4914d97cb4bb885
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829379"
---
# <a name="oid_wdi_set_fast_bss_transition_parameters"></a>OID \_ WDI \_ 设置 \_ 快速 \_ BSS \_ 转换 \_ 参数


OID \_ WDI \_ 设置 \_ 快速 \_ BSS \_ 转换 \_ 参数是为了响应 [NDIS \_ 状态 \_ WDI \_ 指示 \_ \_ \_ \_ 需要 FT ASSOC](ndis-status-wdi-indication-ft-assoc-params-needed.md)参数而发送的。 它具有) 关联请求发送 (所需的参数。 命令作为直接 OID 发送到驱动程序。

| 范围 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 否                       | 1                               |

 

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                  | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                                                                                                                                                    |
|------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ 状态**](./wdi-tlv-status.md)      |                                |          | 如果此状态为 "成功"，则会显示 (RSNIE，MDE，FTE) 的其余字段。 这表明身份验证响应不存在问题或错误 (例如，MIC 检查失败) 并且 IHV 可以继续重新关联请求。 |
| [**WDI \_ TLV \_ FT \_ RSNIE**](./wdi-tlv-ft-rsnie.md) |                                | X        | RSN IE 字节 blob。                                                                                                                                                                                                                                          |
| [**WDI \_ TLV \_ FT \_ MDE**](./wdi-tlv-ft-mde.md)     |                                | X        | MDE 字节 blob。                                                                                                                                                                                                                                             |
| [**WDI \_ TLV \_ FT \_ FTE**](./wdi-tlv-ft-fte.md)     |                                | X        | FTE 字节 blob。                                                                                                                                                                                                                                             |

 

## <a name="set-property-results"></a>设置属性结果


无其他数据。 标头中的数据足够了。

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

 

