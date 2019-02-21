---
title: OID_WDI_SET_P2P_WPS_ENABLED
description: OID_WDI_SET_P2P_WPS_ENABLED 请求适配器启用或禁用的 Wi-fi 受保护的安装程序 (WPS) 上的 nic。
ms.assetid: 96F21807-464F-4B50-AF7E-779F6BF6FE37
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_P2P_WPS_ENABLED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8c2a7dd1decd9ba925f1bc0fb9ed427e354d0865
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555285"
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

 

 




