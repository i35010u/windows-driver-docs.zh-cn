---
title: NdisGetNextMdl 宏
description: 给定指向当前 MDL 的指针，NdisGetNextMdl 宏将检索 MDL 链中的下一个 MDL。
ms.date: 07/18/2017
keywords:
- NdisGetNextMdl 从 Windows Vista 开始的宏网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 039731afdd60d3ffec6836f4646eefe82ab8b7df
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789687"
---
# <a name="ndisgetnextmdl-macro"></a>NdisGetNextMdl 宏


给定指向当前 MDL 的指针， **NdisGetNextMdl** 宏将检索 MDL 链中的下一个 mdl。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID NdisGetNextMdl(
    _CurrentMdl,
    _NextMdl
);
```

<a name="parameters"></a>参数
----------

*\_CurrentMdl*   
指向指定的当前 MDL 的指针。

*\_NextMdl*   
一个指向调用方提供的变量的指针，此宏在该指针返回一个指向 MDL 链中下一个 MDL 的指针（如果有），该指针位于 *\_ CURRENTMDL* 的 mdl 之后。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

**NdisGetNextMdl** 宏提供 [**NdisGetNextBuffer**](/previous-versions/windows/hardware/network/ff552070(v=vs.85))函数的基于 MDL 的版本。

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
<td>台式机</td>
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
<td><p>任何级别</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NdisGetNextBuffer**](/previous-versions/windows/hardware/network/ff552070(v=vs.85))

 

