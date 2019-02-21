---
title: KSCATEGORY_VBICODEC
description: KSCATEGORY_VBICODEC
ms.assetid: c69857e5-19ca-44aa-ae42-bc015be2b0f8
keywords:
- KSCATEGORY_VBICODEC 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_VBICODEC
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: de1cf995ad3c8b3ea99057ef398afaa6beab18b7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554606"
---
# <a name="kscategoryvbicodec"></a>KSCATEGORY_VBICODEC


KSCATEGORY_VBICODEC[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff568277)(KS) 功能的视频的遮蔽间隔 (VBI) 编解码器设备类别。

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
<td align="left"><p>KSCATEGORY_VBICODEC</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{07DAD660-22F1-11D1-A9F4-00C04FBBDE8F}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序注册 KSCATEGORY_VBICODEC 向操作系统指示设备支持 KSCATEGORY_VBICODEC 功能分类的实例。

有关视频设备的常规信息，请参阅[视频捕获设备](https://msdn.microsoft.com/library/windows/hardware/ff568699)。

有关视频消隐功能的详细信息，请参阅[流式处理视频捕获设备中的数据](https://msdn.microsoft.com/library/windows/hardware/ff568268)并[VBI 类别](https://msdn.microsoft.com/library/windows/hardware/ff568691)。

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
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSCATEGORY_VIDEO**](kscategory-video.md)

 

 






