---
title: NDIS_MDL_LINKAGE 宏
description: NDIS_MDL_LINKAGE 宏检索指向与指定 MDL 相关联的下一步 MDL。
ms.assetid: 3d5a91cb-cb26-49fb-b510-75fc95f7f46b
ms.date: 07/18/2017
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 NDIS_MDL_LINKAGE 宏
ms.localizationpriority: medium
ms.openlocfilehash: 58f91c90d0927c9780d4dde8c742b7d936987bd0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385747"
---
# <a name="ndismdllinkage-macro"></a>NDIS\_MDL\_链接宏


**NDIS\_MDL\_链接**宏检索指向与指定 MDL 相关联的下一步 MDL。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PVOID NDIS_MDL_LINKAGE(
   PMDL _Mdl
);
```

<a name="parameters"></a>Parameters
----------

*\_Mdl*   
指向 MDL 的指针。

<a name="return-value"></a>返回值
------------

**NDIS\_MDL\_链接**返回一个指向 MDL 或**NULL**如果没有下一步 MDL。

<a name="remarks"></a>备注
-------

**NDIS\_MDL\_链接**宏提供的基于 MDL 版本[ **NDIS\_缓冲区\_链接**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff556919(v=vs.85))函数。

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


[**NDIS\_缓冲区\_链接**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff556919(v=vs.85))

 

 




