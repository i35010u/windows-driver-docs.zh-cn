---
title: WDI_TLV_BSS_ENTRY_DEVICE_CONTEXT
description: WDI_TLV_BSS_ENTRY_DEVICE_CONTEXT 是包含 BSS 条目的设备上下文 TLV。
ms.assetid: 5672294B-C6C0-43A3-9553-D6309F64F4A6
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BSS_ENTRY_DEVICE_CONTEXT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bb67a5d4108599a2389da46c3bf3ad339d9ae10a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343216"
---
# <a name="wditlvbssentrydevicecontext"></a>WDI\_TLV\_BSS\_条目\_设备\_上下文


WDI\_TLV\_BSS\_条目\_设备\_上下文是包含 BSS 条目的设备上下文 TLV。

## <a name="tlv-type"></a>TLV 类型


0xD

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                                                                                                                                                                                                                                                |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | 指定的上下文数据 UINT8 元素的数组。 此上下文由 IHV 组件提供，可用于存储 IHV 组件想要维护的每个 BSS 入口状态。 若要避免生存期管理问题，IHV 组件必须在此 TLV 中不使用指针。 |

 

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

 

 




