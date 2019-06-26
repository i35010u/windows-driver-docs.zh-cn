---
title: OID_WDI_SET_ADD_CIPHER_KEYS
description: OID_WDI_SET_ADD_CIPHER_KEYS 添加或覆盖的端口的表中的密码密钥。 这是仅限组的属性。
ms.assetid: d10fc976-9e51-4bbb-8f29-caf8c600618a
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_ADD_CIPHER_KEYS 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 9e86053bca1e6e46e6f982a24ffcabfa8105decf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387255"
---
# <a name="oidwdisetaddcipherkeys"></a>OID\_WDI\_SET\_ADD\_CIPHER\_KEYS


OID\_WDI\_设置\_添加\_密码\_密钥添加或覆盖的端口的表中的密码密钥。 这是仅限组的属性。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| Port  | 是                      | 1                               |

 

标记为不应在漫游时清除静态密码密钥。 仅在被清除[OID\_WDI\_任务\_DOT11\_重置](oid-wdi-task-dot11-reset.md)或者如果它们已被覆盖具有新 OID\_WDI\_设置\_添加\_密码\_密钥。

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                          | 允许多个 TLV 实例 | 可选 | 描述                                                              |
|------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------------------|
| [**WDI\_TLV\_SET\_CIPHER\_KEY\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-set-cipher-key-info) | X                              |          | 要添加或覆盖该端口的表中的密码密钥。 |

 

## <a name="set-property-results"></a>设置属性结果


没有其他数据。 标头中的数据就足够了。

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
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID\_WDI\_SET\_DELETE\_CIPHER\_KEYS](oid-wdi-set-delete-cipher-keys.md)

 

 




