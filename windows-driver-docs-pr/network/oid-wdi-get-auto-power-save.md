---
title: OID_WDI_GET_AUTO_POWER_SAVE
description: OID_WDI_GET_AUTO_POWER_SAVE 获取端口的省电状态。
ms.assetid: b7a14348-66ad-4728-986d-05145eb49b27
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_GET_AUTO_POWER_SAVE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 66c64a6541d517c462e1f4a1306ee1203b87e2ca
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213295"
---
# <a name="oid_wdi_get_auto_power_save"></a>OID \_ WDI \_ 获取 \_ 自动 \_ 节能 \_


OID \_ WDI \_ GET \_ 自动省 \_ 电 \_ 获取端口的省电状态。

| 作用域 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 不适用           | 1                               |

 

省电与延迟之间的权衡。 当自动节能模式设置为使用 [OID \_ WDI \_ set \_ 连接 \_ 质量](oid-wdi-set-connection-quality.md) 命令启用时，固件将尝试与连接的访问点进行交互，使其尽可能多地进入省电模式。 该固件还负责检测连接的接入点是否确认为802.11 规范并遵循省电模式协议。 如果访问点不符合 (不能正确地) 节能模式，则即使将 "自动节能" 设置为 "已启用"，固件也不会进入节能模式。 当 "自动节能" 设置为 "已禁用" 时，固件侧重于发送和接收数据包的低延迟。 这种情况的示例包括：流式处理模式为打开状态，以及系统使用的是 AC 电源，因此首选低延迟是省电。

## <a name="get-property-parameters"></a>获取属性参数


无其他参数。 标头中的数据足够了。
## <a name="get-property-results"></a>获取属性结果


| TLV                                                                          | 允许多个 TLV 实例 | 可选 | 说明                  |
|------------------------------------------------------------------------------|--------------------------------|----------|------------------------------|
| [**WDI \_ TLV \_ 获取 \_ 自动 \_ 节能 \_**](./wdi-tlv-get-auto-power-save.md) |                                |          | 自动保存电源信息。 |

 

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

 

