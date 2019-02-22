---
title: OID_WDI_GET_BSS_ENTRY_LIST
description: OID_WDI_GET_BSS_ENTRY_LIST 用于通过端口要求的适配器，以指示的已缓存的 BSS 网络的列表。
ms.assetid: 0eaa2b3a-6a1f-49e1-9556-81691892e666
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_GET_BSS_ENTRY_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 93cfcc5f960be78a815dc16d0ec6d75a34efb974
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521883"
---
# <a name="oidwdigetbssentrylist"></a>OID\_WDI\_GET\_BSS\_ENTRY\_LIST


OID\_WDI\_获取\_BSS\_条目\_列表询问以指示列表已缓存的 BSS 网络适配器端口使用。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| 端口  | 不支持 set 语句        | 1                               |

 

这仅用于执行 BSS 列表缓存的适配器。 时充当客户端，该端口必须报告的访问点的 BSS 条目。 此外，如果端口执行后台范围扫描，则应报告其扫描操作中它所发现的 BSS 条目。

当适配器收到此请求时，它必须发送[NDIS\_状态\_WDI\_指示\_BSS\_条目\_列表](ndis-status-wdi-indication-bss-entry-list.md)到的迹象Microsoft 组件。 这些指示必须包含符合获取参数的 BSS 项。 适配器可以发送一个或多个 NDIS\_状态\_WDI\_指示\_BSS\_条目\_属性完成之前，必须完成列表提示，但它们。

Microsoft 组件使用的指定项的列表的操作系统报告的 BSS 列表。 它还用于填充漫游的参数和连接的任务。

## <a name="get-property-parameters"></a>获取属性参数


| TLV                                         | 允许多个 TLV 实例 | 可选 | 描述                                           |
|---------------------------------------------|--------------------------------|----------|-------------------------------------------------------|
| [**WDI\_TLV\_SSID**](https://msdn.microsoft.com/library/windows/hardware/dn898064) |                                |          | 宿主需要 BSS SSID 列表的更新。 |

 

## <a name="get-property-results"></a>获取属性的结果


没有其他数据。 标头中的数据就足够了。
## <a name="unsolicited-indication"></a>未经请求的指示


[NDIS\_状态\_WDI\_指示\_BSS\_条目\_列表](ndis-status-wdi-indication-bss-entry-list.md)要求
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

 

 




