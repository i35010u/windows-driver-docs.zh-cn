---
title: KSMFT_CATEGORY_MULTIPLEXER
description: KSMFT_CATEGORY_MULTIPLEXER
ms.assetid: 79849eeb-7e5d-45bb-a0e4-cd6f413aa3dc
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
ms.openlocfilehash: 731e17f7619a9028b2abafb28960585defe48b2c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391689"
---
# <a name="ksmftcategorymultiplexer"></a>KSMFT_CATEGORY_MULTIPLEXER


KSMFT_CATEGORY_MULTIPLEXER[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff560842)(KS) 功能将组合的设备类别 (*多路复用*)媒体流。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">特性</th>
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

AVStream 驱动程序 MFT 编解码器支持注册此设备接口类，以向操作系统指示设备支持 KSMFT_CATEGORY_MULTIPLEXER 功能分类的实例。

有关 AVStream 编解码器支持硬件设备的设备接口类的详细信息，请参阅[开始使用硬件 AVStream 中支持的编解码器](https://msdn.microsoft.com/library/windows/hardware/gg299325)。

有关如何在一个 INF 文件中注册此功能的类别的详细信息，请参阅*Hiddigi.inf*文件，它是随*src\\输入\\hiddigi*示例WDK 中的驱动程序。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

 

 





