---
title: OID_WDI_GET_NEXT_ACTION_FRAME_DIALOG_TOKEN
description: OID_WDI_GET_NEXT_ACTION_FRAME_DIALOG_TOKEN 请求要在下一个操作框架中使用的 DialogToken。
ms.assetid: EB5F6077-1566-41AE-B414-9ECF24BAE982
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_GET_NEXT_ACTION_FRAME_DIALOG_TOKEN 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d7ce0040abef7e828f6cbae3cb8f0cca87f9ab0b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213293"
---
# <a name="oid_wdi_get_next_action_frame_dialog_token"></a>OID \_ WDI \_ 获取 \_ 下一个 \_ 操作 \_ 框架 \_ 对话框 \_ 令牌


OID \_ WDI \_ 获取 \_ 下一个 \_ 操作 \_ 框架 \_ 对话框 \_ 令牌请求要在下一个操作帧中使用 DialogToken。

| 作用域 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 否                       | 1                               |

 

## <a name="get-property-parameters"></a>获取属性参数


无其他参数。 标头中的数据足够了。
## <a name="get-property-results"></a>获取属性结果


| TLV                                                                     | 允许多个 TLV 实例 | 可选 | 说明     |
|-------------------------------------------------------------------------|--------------------------------|----------|-----------------|
| [**WDI \_ TLV \_ 下一个 \_ 对话框 \_ 令牌**](./wdi-tlv-next-dialog-token.md) |                                |          | 对话框标记。 |

 

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

 

