---
title: FLT_PARAMETERS IRP_MJ_SET_QUOTA 联合
description: 联合组件时使用 FLT MajorFunction 字段\_IO\_参数\_操作的块结构是 IRP\_MJ\_设置\_配额。
ms.assetid: 4ca19af9-695c-421e-90d5-eb40978f8d19
keywords:
- FLT_PARAMETERS IRP_MJ_SET_QUOTA 联合可安装文件系统驱动程序
- FLT_PARAMETERS 联合可安装文件系统驱动程序
- PFLT_PARAMETERS 联合指针可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FLT_PARAMETERS
api_location:
- fltkernel.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 627f24d18da2b69f2aff5c3ccab5eae8d48c4789
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63393028"
---
# <a name="fltparameters-for-irpmjsetquota-union"></a>FLT\_IRP 的参数\_MJ\_设置\_配额并集


联合组件时使用**MajorFunction**字段[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)结构操作已[ **IRP\_MJ\_设置\_配额**](irp-mj-set-quota.md)。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG Length;
    PVOID QuotaBuffer;
    PMDL  MdlAddress;
  } SetQuota;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**SetQuota**  
结构，它包含以下成员。

**长度**  
缓冲区的长度，以字节为单位，该**QuotaBuffer**指向。

**QuotaBuffer**  
指向调用方提供，指针[**文件\_配额\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540342)-包含要设置的配额信息的结构化输入的缓冲区。

**MdlAddress**  
描述缓冲区的内存描述符列表 (MDL) 的地址， **QuotaBuffer**指向。 此成员是可选的可以是**NULL**。

<a name="remarks"></a>备注
-------

[ **FLT\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff544673)结构[ **IRP\_MJ\_设置\_配额**](irp-mj-set-quota.md)操作包含表示的回调数据集配额信息操作的参数 ([**FLT\_回调\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 结构. 包含在 FLT\_IO\_参数\_块结构。

IRP\_MJ\_设置\_配额是基于 IRP 的操作。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Fltkernel.h （包括 Fltkernel.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**文件\_配额\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540342)

[**FLT\_CALLBACK\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**IoCheckQuotaBufferValidity**](https://msdn.microsoft.com/library/windows/hardware/ff548279)

[**IRP\_MJ\_SET\_QUOTA**](irp-mj-set-quota.md)

 

 






