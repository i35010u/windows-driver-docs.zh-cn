---
title: KSMFT_CATEGORY_DEMULTIPLEXER
description: KSMFT_CATEGORY_DEMULTIPLEXER
ms.assetid: 8cb22e49-67e5-474f-8e71-d540c789c798
keywords:
- KSMFT_CATEGORY_DEMULTIPLEXER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSMFT_CATEGORY_DEMULTIPLEXER
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5f215568d6ef7a78ae5dda7e2653da30d6a40f5e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540450"
---
# <a name="ksmftcategorydemultiplexer"></a>KSMFT_CATEGORY_DEMULTIPLEXER


KSMFT_CATEGORY_DEMULTIPLEXER[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff560842)(KS) 分隔的设备的功能类别 (*demultiplexes*) 媒体流。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>KSMFT_CATEGORY_DEMULTIPLEXER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{a8700a7a-939b-44c5-99d7-76226b23b3f1}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

AVStream 驱动程序 MFT 编解码器支持注册此设备接口类，以向操作系统指示设备支持 KSMFT_CATEGORY_DEMULTIPLEXER 功能分类的实例。

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
<td align="left"><p>标头</p></td>
<td align="left">Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

 

 





