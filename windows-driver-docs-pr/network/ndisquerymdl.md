---
title: NdisQueryMdl 宏
description: NdisQueryMdl 宏检索从 MDL 缓冲区长度和基本的虚拟地址 （可选）。
ms.assetid: 0eccd784-c815-4094-87e5-a3e283abed73
ms.date: 07/18/2017
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 NdisQueryMdl 宏
ms.localizationpriority: medium
ms.openlocfilehash: 5003880b56cfb2e96bf18d41b7b2e55c2209ae00
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392381"
---
# <a name="ndisquerymdl-macro"></a>NdisQueryMdl 宏


**NdisQueryMdl**宏从 MDL 检索缓冲区长度和基本的虚拟地址 （可选）。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID NdisQueryMdl(
    _Mdl,
    _VirtualAddress,
    _Length,
    _Priority
);
```

<a name="parameters"></a>Parameters
----------

*\_Mdl*   
指向 MDL 的指针。

*\_VirtualAddress*   
指向在其中此宏将返回由 MDL 描述的虚拟地址范围的基本虚拟地址的调用方提供的变量的指针。 可以是虚拟的基址**NULL**这两个原因如下：

-   系统资源很低或已耗尽和*\_优先级*参数设置为**LowPagePriority**或**NormalPagePriority**。

-   系统资源耗尽和*\_优先级*参数设置为**HighPagePriority**。

*\_Length*   
指向在其中此宏将返回由 MDL 描述的虚拟地址范围的长度，以字节为单位，调用方提供的变量的指针。

*\_优先级*   
页面优先级值。 此参数的可能值的列表，请参阅*优先级*的参数[ **MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559)宏。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

**NdisQueryMdl**宏提供的基于 MDL 版本[ **NdisQueryBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff554407)函数。

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


[**MmGetSystemAddressForMdlSafe**](https://msdn.microsoft.com/library/windows/hardware/ff554559)

[**NdisQueryBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff554407)

 

 




