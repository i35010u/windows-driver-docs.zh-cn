---
title: OID_WDI_SET_DELETE_CIPHER_KEYS
description: OID_WDI_SET_DELETE_CIPHER_KEYS 从设备的密码密钥表中删除密码密钥。
ms.assetid: 0a8d4625-382b-4976-aa3f-a8fea0976a00
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_DELETE_CIPHER_KEYS 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 30f9f4c8fb7e5d6aeeda0e348824605de7ecf80a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212115"
---
# <a name="oid_wdi_set_delete_cipher_keys"></a>OID \_ WDI \_ 设置 \_ 删除 \_ 密码 \_ 密钥


OID \_ WDI \_ 设置 \_ 删除 \_ 密码 \_ 密钥从设备的密码密钥表中删除密码密钥。

| 作用域 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                | 允许多个 TLV 实例 | 可选 | 说明                                                |
|------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------|
| [**WDI \_ TLV \_ 删除 \_ 密码 \_ 密钥 \_ 信息**](./wdi-tlv-delete-cipher-key-info.md) | X                              |          | 要从设备的键表中删除的密码密钥。 |

 

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

## <a name="see-also"></a>另请参阅


[OID \_ WDI \_ 设置 \_ 添加 \_ 密码 \_ 密钥](oid-wdi-set-add-cipher-keys.md)

 

