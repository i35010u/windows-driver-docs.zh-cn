---
title: WDI_TLV_BSS_ENTRY_DEVICE_CONTEXT
description: WDI_TLV_BSS_ENTRY_DEVICE_CONTEXT 是一个 TLV，其中包含 BSS 条目的设备上下文。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BSS_ENTRY_DEVICE_CONTEXT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 800ef70d8216eef03b70f02be3fee0b0238e227e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782126"
---
# <a name="wdi_tlv_bss_entry_device_context"></a>WDI \_ TLV \_ BSS \_ 条目 \_ 设备 \_ 上下文


WDI \_ tlv \_ bss \_ 进入 \_ 设备 \_ 上下文是包含 BSS 条目的设备上下文的 tlv。

## <a name="tlv-type"></a>TLV 类型


0xD

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型      | 描述                                                                                                                                                                                                                                                                                |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | 指定上下文数据的 UINT8 元素的数组。 此上下文由 IHV 组件提供，可用于存储 IHV 组件要维护的每个 BSS 进入状态。 为了避免生存期管理问题，IHV 组件不能使用此 TLV 中的指针。 |

 

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




