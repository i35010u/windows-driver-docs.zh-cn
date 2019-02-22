---
title: WDI_TLV_BSS_ENTRY_CHANNEL_INFO
description: WDI_TLV_BSS_ENTRY_CHANNEL_INFO 是 TLV 包含 BSS 条目通道信息。
ms.assetid: 01DA2EDA-2BE2-4E4F-AE5D-8E07EEF691FE
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BSS_ENTRY_CHANNEL_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1ef1ce103cbc16074fe9aada4beda535cf04b15d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543439"
---
# <a name="wditlvbssentrychannelinfo"></a>WDI\_TLV\_BSS\_条目\_通道\_信息


WDI\_TLV\_BSS\_条目\_通道\_信息是 TLV 包含 BSS 条目通道信息。

## <a name="tlv-type"></a>TLV 类型


0x3A

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                          | 描述                                                  |
|-------------------------------|--------------------------------------------------------------|
| WDI\_通道\_数 (UINT32) | 发现对等逻辑频道号。 |
| UINT32                        | BSS 条目外 ID。                               |

 

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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




