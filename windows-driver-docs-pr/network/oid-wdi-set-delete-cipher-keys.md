---
title: OID_WDI_SET_DELETE_CIPHER_KEYS
description: OID_WDI_SET_DELETE_CIPHER_KEYS 从设备的密码密钥表中删除密码密钥。
ms.assetid: 0a8d4625-382b-4976-aa3f-a8fea0976a00
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_DELETE_CIPHER_KEYS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 98710aad93945da650010b4bb7452d3bb1aefe87
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521677"
---
# <a name="oidwdisetdeletecipherkeys"></a>OID\_WDI\_SET\_DELETE\_CIPHER\_KEYS


OID\_WDI\_设置\_删除\_密码\_密钥删除密码设备的密码密钥表中的密钥。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                | 允许多个 TLV 实例 | 可选 | 描述                                                |
|------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------|
| [**WDI\_TLV\_DELETE\_CIPHER\_KEY\_INFO**](https://msdn.microsoft.com/library/windows/hardware/dn926283) | X                              |          | 若要从设备的密钥表中删除密码密钥。 |

 

## <a name="set-property-results"></a>设置属性结果


没有其他数据。 标头中的数据就足够了。
要求
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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID\_WDI\_SET\_ADD\_CIPHER\_KEYS](oid-wdi-set-add-cipher-keys.md)

 

 




