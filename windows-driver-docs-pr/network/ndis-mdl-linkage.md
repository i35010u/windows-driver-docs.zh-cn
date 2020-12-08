---
title: NDIS_MDL_LINKAGE 宏
description: NDIS_MDL_LINKAGE 宏检索指向与指定 MDL 关联的下一个 MDL 的指针。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_MDL_LINKAGE 宏网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a7dfc58929e02755a441cf53ec5cd9020b0def31
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801601"
---
# <a name="ndis_mdl_linkage-macro"></a>NDIS \_ MDL \_ 链接宏


**NDIS \_ MDL \_ 链接** 宏检索指向与指定 mdl 关联的下一个 mdl 的指针。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PVOID NDIS_MDL_LINKAGE(
   PMDL _Mdl
);
```

<a name="parameters"></a>参数
----------

*\_Mdl*   
指向 MDL 的指针。

<a name="return-value"></a>返回值
------------

**NDIS \_如果 \_** 没有下一个 MDL，mdl 链接将返回指向 MDL 的指针或 **NULL** 。

<a name="remarks"></a>备注
-------

**Ndis \_ MDL \_ 链接** 宏提供基于 MDL 的 [**NDIS \_ 缓冲区 \_ 链接**](/previous-versions/windows/hardware/network/ff556919(v=vs.85))函数版本。

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


[**NDIS \_ 缓冲区 \_ 链接**](/previous-versions/windows/hardware/network/ff556919(v=vs.85))

 

