---
title: OID_WDI_SET_ASSOCIATION_PARAMETERS
description: OID_WDI_SET_ASSOCIATION_PARAMETERS 指定在与一组 BSSIDs 关联期间适配器可使用的参数。
ms.assetid: 86a6cc62-eaa4-435c-af6c-b76591d92c00
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_ASSOCIATION_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 9525e1f22dc47ad984fcea97b3ce51dcd68ff0e2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209651"
---
# <a name="oid_wdi_set_association_parameters"></a>OID \_ WDI \_ 设置 \_ 关联 \_ 参数


OID \_ WDI \_ set \_ association \_ 参数指定在与一组 BSSIDs 关联期间适配器可以使用的参数。

| 作用域 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 否                       | 1                               |

 

此命令替换先前配置的 BSSID 特定关联参数的列表。

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                     | 允许多个 TLV 实例 | 可选 | 说明                     |
|-------------------------------------------------------------------------|--------------------------------|----------|---------------------------------|
| [**WDI \_ TLV \_ 连接 \_ BSS \_ 条目**](./wdi-tlv-connect-bss-entry.md) | X                              |          | BSS 条目和参数。 |

 

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

 

