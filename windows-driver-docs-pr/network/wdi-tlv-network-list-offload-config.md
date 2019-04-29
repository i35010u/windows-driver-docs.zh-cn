---
title: WDI_TLV_NETWORK_LIST_OFFLOAD_CONFIG
description: WDI_TLV_NETWORK_LIST_OFFLOAD_CONFIG 是包含网络列表卸载 (NLO) 配置 TLV。
ms.assetid: 8805B31C-7601-4045-AD52-21B91E2D3722
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_NETWORK_LIST_OFFLOAD_CONFIG 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 661e49bac0106242b6c533fac5d3209c50567071
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392273"
---
# <a name="wditlvnetworklistoffloadconfig"></a>WDI\_TLV\_NETWORK\_LIST\_OFFLOAD\_CONFIG


WDI\_TLV\_网络\_列表\_卸载\_CONFIG 是包含网络列表卸载 (NLO) 配置 TLV。

## <a name="tlv-type"></a>TLV 类型


0xDA

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                           |
|--------|-----------------------------------------------------------------------------------------------------------------------|
| UINT32 | 保留的字段。                                                                                                       |
| UINT32 | 将启动扫描计划之前的延迟 （以秒为单位）。                                                               |
| UINT32 | 时间段 （以秒为单位） 以在第一阶段中进行扫描。                                                                   |
| UINT32 | 快速扫描阶段中的迭代次数。                                                                      |
| UINT32 | 时间段 （以秒为单位） 以在进行慢扫描阶段中进行扫描。 此阶段一直持续无限期到设置新的 NLO 命令。 |

 

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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




