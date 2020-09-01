---
title: WDI_TLV_INDICATION_WAKE_REASON
description: WDI_TLV_INDICATION_WAKE_REASON 是包含 NDIS_STATUS_WDI_INDICATION_WAKE_REASON 唤醒原因的 TLV。
ms.assetid: 3D3F93EA-4733-44FC-9CB3-721F0552F3E2
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_INDICATION_WAKE_REASON 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 520b4199f4b65d1e66bbb1702329b379a0a1f445
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214288"
---
# <a name="wdi_tlv_indication_wake_reason"></a>WDI \_ TLV \_ 指示 \_ 唤醒 \_ 原因


WDI \_ tlv \_ 指示 \_ 唤醒 \_ 原因是一个 Tlv，其中包含 [NDIS \_ 状态 \_ WDI \_ 指示 \_ 唤醒 \_ 原因](./ndis-status-wdi-indication-wake-reason.md)的唤醒原因。

## <a name="tlv-type"></a>TLV 类型


0x9C

## <a name="length"></a>Length


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


| 类型   | 说明                |
|--------|----------------------------|
| UINT32 | 指定唤醒原因。 |

 

有效的唤醒原因值为：

| 唤醒原因                                       | 值  | 说明                                                                                                          |
|---------------------------------------------------|--------|----------------------------------------------------------------------------------------------------------------------|
| WDI \_ 唤醒 \_ 原因 \_ 代码 \_ 数据包                   | 0x0001 | 接收的数据包与唤醒模式匹配。                                                                          |
| WDI \_ 唤醒 \_ 原因 \_ 代码 \_ 媒体 \_ 断开连接        | 0x0002 | 媒体断开连接。                                                                                                 |
| WDI \_ 唤醒 \_ 原因 \_ 代码 \_ 媒体 \_ 连接           | 0x0003 | 媒体连接。                                                                                                    |
| WDI \_ 唤醒 \_ 原因 \_ 代码 \_ NLO \_ DISCOVERY           | 0x1000 | NLO 发现。                                                                                                       |
| WDI \_ 唤醒 \_ 原因 \_ 代码 \_ AP \_ 关联 \_ 丢失    | 0x1001 | 访问点关联丢失。                                                                                       |
| WDI \_ 唤醒 \_ 原因 \_ 代码 \_ GTK \_ 握手 \_ 错误    | 0x1002 | GTK 握手错误。                                                                                                 |
| WDI \_ 唤醒 \_ 原因 \_ 代码 \_ 4WAY \_ 握手 \_ 请求 | 0x1003 | 4向握手请求。                                                                                             |
| WDI \_ 唤醒 \_ 原因 \_ 代码 \_ EAPID \_ 请求           | 0x1004 | 留待将来使用。                                                                                             |
| WDI \_ 唤醒 \_ 原因 \_ 代码 \_ 传入 \_ M1           | 0x1005 | 改为使用 WDI \_ 唤醒 \_ 原因 \_ 代码 \_ 4WAY \_ 握手 \_ 请求。                                                       |
| WDI \_ 唤醒 \_ 原因 \_ 代码 \_ 固件 \_ 停止        | 0x1010 | 检测到固件挂起 (例如，通过监视程序计时器) 并且唤醒逻辑仍可用于唤醒主机。 |
| WDI \_ 唤醒 \_ 原因 \_ 代码 \_ GTK \_ 握手 \_ 请求  | 0x1020 | 组密钥 rekey 请求。                                                                                             |

 

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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

