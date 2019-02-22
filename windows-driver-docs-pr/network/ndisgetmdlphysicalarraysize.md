---
title: NdisGetMdlPhysicalArraySize 宏
description: NdisGetMdlPhysicalArraySize 宏检索与 MDL 相关联的断开连接的物理内存块的数目。
ms.assetid: 25e3f9a3-3057-4081-af74-427102197906
ms.date: 07/18/2017
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 NdisGetMdlPhysicalArraySize 宏
ms.localizationpriority: medium
ms.openlocfilehash: bc8cd67880d36826e04479559492b713ab7fa6bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542454"
---
# <a name="ndisgetmdlphysicalarraysize-macro"></a>NdisGetMdlPhysicalArraySize 宏


**NdisGetMdlPhysicalArraySize**宏检索与 MDL 相关联的断开连接的物理内存块的数目。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID NdisGetMdlPhysicalArraySize(
    _Mdl,
    _ArraySize
);
```

<a name="parameters"></a>参数
----------

*\_Mdl*   
指向 MDL 的指针。

*\_ArraySize*   
在此宏用于返回与指定 MDL 相关联的断开连接的物理内存块的数目的调用方提供的变量指向的指针。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

**NdisGetMdlPhysicalArraySize**宏提供的基于 MDL 版本[ **NdisGetBufferPhysicalArraySize** ](https://msdn.microsoft.com/library/windows/hardware/ff552033)函数。

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
<td><p>&lt;= DISPATCH_LEVEL</p></td>
</tr>
<tr class="odd">
<td><p>DDI 符合性规则</p></td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff547985" data-raw-source="[&lt;strong&gt;Irql_NetBuffer_Function&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547985)"><strong>Irql_NetBuffer_Function</strong></a></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NdisGetBufferPhysicalArraySize**](https://msdn.microsoft.com/library/windows/hardware/ff552033)

 

 




