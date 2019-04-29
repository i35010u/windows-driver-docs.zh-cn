---
title: KSCATEGORY_MIXER
description: KSCATEGORY_MIXER
ms.assetid: b17696ed-d8d6-4d02-a23b-64ebc8505afd
keywords:
- KSCATEGORY_MIXER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_MIXER
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 04b65ef0d7e0ef8b8e80c7fb8c0ae0643f13ca92
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390742"
---
# <a name="kscategorymixer"></a>KSCATEGORY_MIXER


KSCATEGORY_MIXER[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff568277)混合使用数据流的 (KS) 功能类别。

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
<td align="left"><p>KSCATEGORY_MIXER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{AD809C00-7B88-11D0-A5D6-28DB04C10000}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序注册 KSCATEGORY_MIXER 向操作系统指示设备支持 KSCATEGORY_MIXER 功能分类的实例。

有关此功能的类别和其他功能的类别的详细信息，请参阅[音频适配器安装设备接口](https://msdn.microsoft.com/library/windows/hardware/ff536813)并[ **KSPROPERTY_TOPOLOGY_CATEGORIES**](https://msdn.microsoft.com/library/windows/hardware/ff565799).

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

## <a name="see-also"></a>请参阅


[**KSPROPERTY_TOPOLOGY_CATEGORIES**](https://msdn.microsoft.com/library/windows/hardware/ff565799)

 

 






