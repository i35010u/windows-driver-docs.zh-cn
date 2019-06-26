---
title: KSCATEGORY_MULTIPLEXER
description: KSCATEGORY_MULTIPLEXER
ms.assetid: 3023769a-9b98-4c12-90b1-f83294a45ab0
keywords:
- KSCATEGORY_MULTIPLEXER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_MULTIPLEXER
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 406c326784aa2a1c9f1060d4b3c7dc5ddd71fcab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374225"
---
# <a name="kscategorymultiplexer"></a>KSCATEGORY_MULTIPLEXER


KSCATEGORY_MULTIPLEXER[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)为定义[内核流式处理](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)(KS) 功能的多路复用器设备类别。

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
<td align="left"><p>KSCATEGORY_MULTIPLEXER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{7A5DE1D3-01A1-452c-B481-4FA2B96271E8}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序注册 KSCATEGORY_MULTIPLEXER 向操作系统指示设备支持 KSCATEGORY_MULTIPLEXER 功能分类的实例。

有关如何在一个 INF 文件中注册此功能的类别的示例，请参阅*Bdan.inf* INF 文件，包括中的软件调谐器示例*src/swtuner/algtuner* WDK 的目录。

多路复用器有关的信息，请参阅[拓扑筛选器](https://docs.microsoft.com/windows-hardware/drivers/audio/topology-filters)。

有关 KSCATEGORY_MULTIPLEXER 功能类别的详细信息，请参阅[编码器安装和注册](https://docs.microsoft.com/windows-hardware/drivers/stream/encoder-installation-and-registration)。

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
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

 

 





