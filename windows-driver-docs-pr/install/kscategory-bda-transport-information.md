---
title: KSCATEGORY_BDA_TRANSPORT_INFORMATION
description: KSCATEGORY_BDA_TRANSPORT_INFORMATION
ms.assetid: 0af3159c-8c44-4c42-8141-944bb734623c
keywords:
- KSCATEGORY_BDA_TRANSPORT_INFORMATION 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_BDA_TRANSPORT_INFORMATION
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 876b2de144310d1a68a6b6c143d987e6a816ccf5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383378"
---
# <a name="kscategorybdatransportinformation"></a>KSCATEGORY_BDA_TRANSPORT_INFORMATION


KSCATEGORY_BDA_TRANSPORT_INFORMATION[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)为定义[内核流式处理](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)(KS) 传输的信息中的筛选器 (TIF) 的功能类别[广播驱动程序体系结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_stream/index)(BDA)。

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
<td align="left"><p>KSCATEGORY_BDA_TRANSPORT_INFORMATION</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{A2E3074F-6C3D-11d3-B653-00C04F79498E}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

BDA 设备的驱动程序注册 KSCATEGORY_BDA_TRANSPORT_INFORMATION 向操作系统指示设备支持 BDA 传输的信息筛选器的实例。

有关 BDA 传输的信息筛选器的 KS 功能类别的详细信息，请参阅[BDA 筛选器类别 Guid](https://docs.microsoft.com/windows-hardware/drivers/stream/bda-filter-category-guids)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows XP、 DirectX 9.0 a 安装，Windows 2000 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Bdamedia.h （包括 Bdamedia.h）</td>
</tr>
</tbody>
</table>

 

 





