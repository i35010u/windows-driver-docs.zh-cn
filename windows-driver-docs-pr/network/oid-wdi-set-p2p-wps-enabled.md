---
title: OID_WDI_SET_P2P_WPS_ENABLED
description: OID_WDI_SET_P2P_WPS_ENABLED 请求适配器启用或禁用的 Wi-fi 受保护的安装程序 (WPS) 上的 nic。
ms.assetid: 96F21807-464F-4B50-AF7E-779F6BF6FE37
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_P2P_WPS_ENABLED 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 4e679249bb4a78c3719b99186e37c9ad257f686a
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902415"
---
# <a name="oidwdisetp2pwpsenabled"></a>OID\_WDI\_SET\_P2P\_WPS\_ENABLED


OID\_WDI\_设置\_P2P\_WPS\_已启用请求适配器启用或禁用的 Wi-fi 受保护的安装程序 (WPS) 上的 nic。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                 | 允许多个 TLV 实例 | 可选 | 描述                                 |
|---------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------|
| [**WDI\_TLV\_P2P\_WPS\_ENABLED**](https://msdn.microsoft.com/library/windows/hardware/dn898018) |                                |          | 指定是否启用或禁用 WPS。 |

 

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

 

 




