---
title: OID_WDI_SET_P2P_WPS_ENABLED
description: OID_WDI_SET_P2P_WPS_ENABLED 请求适配器启用或禁用 NIC 上 Wi-Fi 受保护的安装程序 (WPS) 。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_P2P_WPS_ENABLED 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6fadf72c8bfd07c97c937a7c9a665c54b72297c7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829333"
---
# <a name="oid_wdi_set_p2p_wps_enabled"></a>OID \_ WDI \_ SET \_ P2P \_ WPS \_ 已启用


OID \_ WDI \_ SET \_ P2P \_ WPS \_ 已启用请求，适配器将启用或禁用 NIC 上 Wi-Fi 受保护的安装程序 (WPS) 。

| 范围 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                 | 允许多个 TLV 实例 | 可选 | 说明                                 |
|---------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------|
| [**\_已启用 WDI TLV \_ P2P \_ WPS \_**](./wdi-tlv-p2p-wps-enabled.md) |                                |          | 指定是启用还是禁用 WPS。 |

 

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

 

