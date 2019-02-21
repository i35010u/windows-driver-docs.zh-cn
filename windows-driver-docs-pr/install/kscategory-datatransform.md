---
title: KSCATEGORY_DATATRANSFORM
description: KSCATEGORY_DATATRANSFORM
ms.assetid: 2e5ff89a-6ec4-4bdf-b935-675c2a337efb
keywords:
- KSCATEGORY_DATATRANSFORM 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_DATATRANSFORM
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1102c962f517c6f47ebbd2290c708eef7e4b6a67
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543876"
---
# <a name="kscategorydatatransform"></a>KSCATEGORY_DATATRANSFORM


KSCATEGORY_DATATRANSFORM[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff568277)(KS) 转换的音频数据流量的功能类别。

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
<td align="left"><p>KSCATEGORY_DATATRANSFORM</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{2EB07EA0-7E70-11D0-A5D6-28DB04C10000}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序注册 KSCATEGORY_DATATRANSFORM 向操作系统指示设备支持 KSCATEGORY_DATATRANSFORM 功能分类的实例。

有关如何在一个 INF 文件中注册此功能的类别的示例，请参阅*Ddksynth.inf*软件合成器示例中包含的 INF 文件*src\\音频\\ddksynth* WDK 的目录。

有关此功能的类别的详细信息，请参阅[音频适配器安装设备接口](https://msdn.microsoft.com/library/windows/hardware/ff536813)， [ **KSPROPERTY_TOPOLOGY_CATEGORIES**](https://msdn.microsoft.com/library/windows/hardware/ff565799)，以及[GFX 要求筛选器工厂](https://msdn.microsoft.com/library/windows/hardware/ff537839)。

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

 

 





