---
title: NdisQueryMdlOffset macro
description: NdisQueryMdlOffset 宏检索在一个物理页内的偏移量的开始给定的 MDL 缓冲区和缓冲区的长度。
ms.assetid: d6f23e9c-5015-4087-b7a2-badee00bdafa
ms.date: 07/18/2017
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 NdisQueryMdlOffset 宏
ms.localizationpriority: medium
ms.openlocfilehash: ac4ab915d2d096f3262904bb98d8256542aedfe6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392392"
---
# <a name="ndisquerymdloffset-macro"></a>NdisQueryMdlOffset macro


**NdisQueryMdlOffset**宏检索在一个物理页内的偏移量的开始给定的 MDL 缓冲区和缓冲区的长度。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID NdisQueryMdlOffset(
    _Mdl,
    _Offset,
    _Length
);
```

<a name="parameters"></a>Parameters
----------

*\_Mdl*   
指向 MDL 的指针。

*\_Offset*   
指向调用方提供的变量在此宏用于返回中包含 MDL 指定缓冲区的物理页的从零开始的字节偏移量的指针。

*\_Length*   
在此宏用于返回 MDL 由指定的虚拟地址范围的长度，以字节为单位，调用方提供的变量指向的指针。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

**NdisQueryMdlOffset**宏提供的基于 MDL 版本[ **NdisQueryBufferOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff554411)函数。

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
<td><p>&lt;= DISPATCH_LEVEL</p></td>
</tr>
<tr class="odd">
<td><p>DDI 符合性规则</p></td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff547985" data-raw-source="[&lt;strong&gt;Irql_NetBuffer_Function&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547985)"><strong>Irql_NetBuffer_Function</strong></a></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NdisQueryBufferOffset**](https://msdn.microsoft.com/library/windows/hardware/ff554411)

 

 




