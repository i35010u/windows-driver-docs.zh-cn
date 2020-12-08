---
title: KSMFT_CATEGORY_MULTIPLEXER
description: KSMFT_CATEGORY_MULTIPLEXER
keywords:
- KSMFT_CATEGORY_MULTIPLEXER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSMFT_CATEGORY_MULTIPLEXER
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a5ac703d69b7d20424e86f723f6f3dfd5e974a85
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839505"
---
# <a name="ksmft_category_multiplexer"></a>KSMFT_CATEGORY_MULTIPLEXER


为 (KSMFT_CATEGORY_MULTIPLEXER [设备接口类](./overview-of-device-interface-classes.md)定义了将 (*多路复用*) 媒体流组合在一起的设备的 [内核流式处理](../stream/kernel-streaming.md)KS) 功能类别。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Attribute</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>KSMFT_CATEGORY_MULTIPLEXER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{059c561e-05ae-4b61-b69d-55b61ee54a7b}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

具有 MFT 编解码器的 AVStream 驱动程序支持注册此设备接口类的实例，以指示操作系统设备支持 KSMFT_CATEGORY_MULTIPLEXER 功能类别。

有关硬件编解码器支持的 AVStream 设备的设备接口类的详细信息，请参阅 [AVStream 中具有硬件编解码器支持的入门](../stream/getting-started-with-hardware-codec-support-in-avstream.md)。

有关如何在 INF 文件中注册此功能类别的详细信息，请参阅 *Hiddigi* 文件，该文件包含在 WDK 的 *src \\ 输入 \\ Hiddigi* 示例驱动程序中。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ks (包含 Ks .h) </td>
</tr>
</tbody>
</table>

 

