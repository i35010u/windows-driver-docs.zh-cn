---
title: NDIS_MDL_TO_SPAN_PAGES 宏
description: NDIS_MDL_TO_SPAN_PAGES 宏检索的内存用于返回给定的 MDL 的物理页的数目。
ms.assetid: 8c9df989-4a5f-4ec1-9544-29b59517a502
ms.date: 07/18/2017
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 NDIS_MDL_TO_SPAN_PAGES 宏
ms.localizationpriority: medium
ms.openlocfilehash: 4c69272cb175c5dd228f6dd73c4b48944c8a0067
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385744"
---
# <a name="ndismdltospanpages-macro"></a>NDIS\_MDL\_TO\_跨度\_页宏


**NDIS\_MDL\_TO\_跨度\_页面**宏检索的内存用于返回给定的 MDL 的物理页的数目。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
int NDIS_MDL_TO_SPAN_PAGES(
   PMDL _Mdl
);
```

<a name="parameters"></a>Parameters
----------

*\_Mdl*   
指向 MDL 的指针。

<a name="return-value"></a>返回值
------------

**NDIS\_MDL\_TO\_跨度\_页**返回要为 MDL 执行备份的虚拟范围的页面数。

<a name="remarks"></a>备注
-------

**NDIS\_MDL\_TO\_跨度\_页**宏提供的基于 MDL 版本[ **NDIS\_缓冲区\_TO\_跨度\_页面**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff556922(v=vs.85))函数。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>目标平台</p></td>
<td>桌面设备</td>
</tr>
<tr class="even">
<td><p>Version</p></td>
<td><p>支持 NDIS 6.0 及更高版本。</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
<tr class="even">
<td><p>IRQL</p></td>
<td><p>任何级别</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_缓冲区\_TO\_跨度\_页**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff556922(v=vs.85))

 

 




