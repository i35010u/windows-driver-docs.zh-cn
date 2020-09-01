---
title: OID_WDI_SET_ADD_CIPHER_KEYS
description: OID_WDI_SET_ADD_CIPHER_KEYS 在端口的键表中添加或覆盖密码密钥。 这是一个仅设置属性。
ms.assetid: d10fc976-9e51-4bbb-8f29-caf8c600618a
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_ADD_CIPHER_KEYS 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: c5c5c4c43cad056b90f81f9322b4c762af6fa223
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215845"
---
# <a name="oid_wdi_set_add_cipher_keys"></a>OID \_ WDI \_ 设置 \_ 添加 \_ 密码 \_ 密钥


OID \_ WDI \_ 设置 \_ 添加 \_ 密码 \_ 密钥在端口的键表中添加或覆盖密码密钥。 这是一个仅设置属性。

| 作用域 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

不应在漫游时清除标记为静态的密码密钥。 只能在 [OID \_ WDI \_ TASK \_ DOT11 \_ RESET](oid-wdi-task-dot11-reset.md) 上清除这些设置，或者使用新 OID 覆盖它们 \_ WDI \_ 设置 \_ 添加 \_ 密码 \_ 密钥。

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                          | 允许多个 TLV 实例 | 可选 | 说明                                                              |
|------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------------------|
| [**WDI \_ TLV \_ 设置 \_ 密码 \_ 密钥 \_ 信息**](./wdi-tlv-set-cipher-key-info.md) | X                              |          | 要在端口的键表中添加或覆盖的密码密钥。 |

 

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


[OID \_ WDI \_ 设置 \_ 删除 \_ 密码 \_ 密钥](oid-wdi-set-delete-cipher-keys.md)

 

