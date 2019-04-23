---
title: OID_WDI_SET_DEFAULT_KEY_ID
description: OID_WDI_SET_DEFAULT_KEY_ID 默认密钥 ID 的端口上的数据包传输设置。
ms.assetid: 5112a661-3560-4070-b74a-0027e3adfac1
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_DEFAULT_KEY_ID 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: bbbfb73d6cf5558266ea4c9edc853545d80ca058
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903551"
---
# <a name="oidwdisetdefaultkeyid"></a>OID\_WDI\_SET\_DEFAULT\_KEY\_ID


OID\_WDI\_设置\_默认\_密钥\_ID 集的默认密钥 ID 的端口上的数据包传输。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                             | 允许多个 TLV 实例 | 可选 | 描述                                             |
|-------------------------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------------|
| [**WDI\_TLV\_DEFAULT\_TX\_KEY\_ID\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/dn926281) |                                |          | 默认值为在端口上的数据包传输密钥 ID。 |

 

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

 

 




