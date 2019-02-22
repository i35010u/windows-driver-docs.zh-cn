---
title: NDIS_MDL_LINKAGE 宏
description: NDIS_MDL_LINKAGE 宏检索指向与指定 MDL 相关联的下一步 MDL。
ms.assetid: 3d5a91cb-cb26-49fb-b510-75fc95f7f46b
ms.date: 07/18/2017
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 NDIS_MDL_LINKAGE 宏
ms.localizationpriority: medium
ms.openlocfilehash: b47a283b39ff3a2cfd17b8acd76e87634cbfeb47
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542842"
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

<a name="parameters"></a>参数
----------

*\_Mdl*   
指向 MDL 的指针。

<a name="return-value"></a>返回值
------------

**NDIS\_MDL\_链接**返回一个指向 MDL 或**NULL**如果没有下一步 MDL。

<a name="remarks"></a>备注
-------

**NDIS\_MDL\_链接**宏提供的基于 MDL 版本[ **NDIS\_缓冲区\_链接**](https://msdn.microsoft.com/library/windows/hardware/ff556919)函数。

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
<td><p>版本</p></td>
<td><p>支持 NDIS 6.0 及更高版本。</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
<tr class="even">
<td><p>IRQL</p></td>
<td><p>任何级别</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_缓冲区\_链接**](https://msdn.microsoft.com/library/windows/hardware/ff556919)

 

 




