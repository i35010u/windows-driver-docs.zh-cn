---
title: WDI_TLV_BSS_ENTRY_SIGNAL_INFO
description: WDI_TLV_BSS_ENTRY_SIGNAL_INFO 是包含 BSS 入口的信号信息 TLV。
ms.assetid: 4410F447-5226-4DF4-923D-11D10D0159CC
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BSS_ENTRY_SIGNAL_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 589ce10edc66861e06ec1721367e5876dce2dc32
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379183"
---
# <a name="wditlvbssentrysignalinfo"></a>WDI\_TLV\_BSS\_条目\_信号\_信息


WDI\_TLV\_BSS\_条目\_信号\_信息是包含 BSS 入口的信号信息 TLV。

## <a name="tlv-type"></a>TLV 类型


0xB

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                                                                                        |
|--------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| INT32  | 接收到的信号强度指示 (RSSI) 符信号或探测响应从对等方的值。 分贝引用到 1.0 毫瓦 (dBm) 为单位指定此值 |
| UINT32 | 指定一个介于 0 到 100 之间的链接质量。 100 的值指定最高的链接质量。                                                                            |

 

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

 

 




