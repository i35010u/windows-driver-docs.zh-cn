---
title: OID_WDI_SET_DEFAULT_KEY_ID
description: OID_WDI_SET_DEFAULT_KEY_ID 设置端口上数据包传输的默认密钥 ID。
ms.assetid: 5112a661-3560-4070-b74a-0027e3adfac1
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_DEFAULT_KEY_ID 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: e07b9ffa4e21ad64b20a16a7747c6213ce805cc3
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213255"
---
# <a name="oid_wdi_set_default_key_id"></a>OID \_ WDI \_ 设置 \_ 默认 \_ 密钥 \_ ID


OID \_ WDI \_ SET \_ default \_ key \_ id 设置端口上数据包传输的默认密钥 id。

| 作用域 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                             | 允许多个 TLV 实例 | 可选 | 说明                                             |
|-------------------------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------------|
| [**WDI \_ TLV \_ 默认 \_ TX \_ 密钥 \_ ID \_ 参数**](./wdi-tlv-default-tx-key-id-parameters.md) |                                |          | 端口上数据包传输的默认密钥 ID。 |

 

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

 

