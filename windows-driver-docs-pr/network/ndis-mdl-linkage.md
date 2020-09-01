---
title: NDIS_MDL_LINKAGE 宏
description: NDIS_MDL_LINKAGE 宏检索指向与指定 MDL 关联的下一个 MDL 的指针。
ms.assetid: 3d5a91cb-cb26-49fb-b510-75fc95f7f46b
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_MDL_LINKAGE 宏网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1fb1cbeb667d4fb9f730fcec4c32cf6b14e46baa
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213915"
---
# <a name="ndis_mdl_linkage-macro"></a>NDIS \_ MDL \_ 链接宏


**NDIS \_ MDL \_ 链接**宏检索指向与指定 mdl 关联的下一个 mdl 的指针。

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

**NDIS \_如果 \_ ** 没有下一个 MDL，mdl 链接将返回指向 MDL 的指针或 **NULL** 。

<a name="remarks"></a>备注
-------

**Ndis \_ MDL \_ 链接**宏提供基于 MDL 的[**NDIS \_ 缓冲区 \_ 链接**](/previous-versions/windows/hardware/network/ff556919(v=vs.85))函数版本。

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
<td>“桌面”</td>
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

## <a name="see-also"></a>另请参阅


[**NDIS \_ 缓冲区 \_ 链接**](/previous-versions/windows/hardware/network/ff556919(v=vs.85))

 

