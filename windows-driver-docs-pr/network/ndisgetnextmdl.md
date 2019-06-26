---
title: NdisGetNextMdl 宏
description: NdisGetNextMdl 宏检索当前 MDL 提供一个指向 MDL 链中的下一步 MDL。
ms.assetid: 5b59ca7c-0998-4d53-9553-4946ef85327c
ms.date: 07/18/2017
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 NdisGetNextMdl 宏
ms.localizationpriority: medium
ms.openlocfilehash: 1280211dfee544e8c35a2e2823875be824290355
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383678"
---
# <a name="ndisgetnextmdl-macro"></a>NdisGetNextMdl 宏


**NdisGetNextMdl**宏检索当前 MDL 提供一个指向 MDL 链中的下一步 MDL。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID NdisGetNextMdl(
    _CurrentMdl,
    _NextMdl
);
```

<a name="parameters"></a>Parameters
----------

*\_CurrentMdl*   
指定当前 MDL 指向的指针。

*\_NextMdl*   
指向在其中此宏返回一个指向 MDL 链中的下一步 MDL 如果任何调用方提供的变量的指针，后面在 MDL  *\_CurrentMdl* 。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

**NdisGetNextMdl**宏提供的基于 MDL 版本[ **NdisGetNextBuffer** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff552070(v=vs.85))函数。

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


[**NdisGetNextBuffer**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff552070(v=vs.85))

 

 




