---
title: NdisQueryMdlOffset 宏
description: NdisQueryMdlOffset 宏检索物理页面中给定 MDL 缓冲区开始处的偏移量和缓冲区的长度。
ms.assetid: d6f23e9c-5015-4087-b7a2-badee00bdafa
ms.date: 07/18/2017
keywords:
- NdisQueryMdlOffset 从 Windows Vista 开始的宏网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ce4e5608eb8fb55dd5d5042b91cb29c23cae78f8
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104864"
---
# <a name="ndisquerymdloffset-macro"></a>NdisQueryMdlOffset 宏


**NdisQueryMdlOffset**宏检索物理页面中给定 MDL 缓冲区开始处的偏移量和缓冲区的长度。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID NdisQueryMdlOffset(
    _Mdl,
    _Offset,
    _Length
);
```

<a name="parameters"></a>参数
----------

*\_Mdl*   
指向 MDL 的指针。

*\_抵销*   
指向调用方提供的变量的指针，此宏在包含 MDL 指定的缓冲区的物理页面内返回从零开始的字节偏移量。

*\_长短*   
指向调用方提供的变量的指针，此宏返回 MDL 指定的虚拟地址范围的长度（以字节为单位）。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

**NdisQueryMdlOffset**宏提供[**NdisQueryBufferOffset**](/previous-versions/windows/hardware/network/ff554411(v=vs.85))函数的基于 MDL 的版本。

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
<td>桌面型</td>
</tr>
<tr class="even">
<td><p>版本</p></td>
<td><p>在 NDIS 6.0 和更高版本中受支持。</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td> (包含 Ndis .h) </td>
</tr>
<tr class="even">
<td><p>IRQL</p></td>
<td><p>&lt;= DISPATCH_LEVEL</p></td>
</tr>
<tr class="odd">
<td><p>DDI 符合性规则</p></td>
<td><a href="/windows-hardware/drivers/devtest/ndis-irql-netbuffer-function" data-raw-source="[&lt;strong&gt;Irql_NetBuffer_Function&lt;/strong&gt;](../devtest/ndis-irql-netbuffer-function.md)"><strong>Irql_NetBuffer_Function</strong></a></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NdisQueryBufferOffset**](/previous-versions/windows/hardware/network/ff554411(v=vs.85))

