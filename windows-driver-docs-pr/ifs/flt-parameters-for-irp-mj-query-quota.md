---
title: FLT_PARAMETERS IRP_MJ_QUERY_QUOTA 联合
description: 联合组件时使用 FLT MajorFunction 字段\_IO\_参数\_操作的块结构是 IRP\_MJ\_查询\_配额。
ms.assetid: b87b008d-f1ce-4dab-9afa-df67aa3dc596
keywords:
- FLT_PARAMETERS IRP_MJ_QUERY_QUOTA 联合可安装文件系统驱动程序
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
ms.openlocfilehash: 276622c2e08332d08edf16d759371a717fc528a9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577096"
---
# <a name="fltparameters-for-irpmjqueryquota-union"></a>FLT\_IRP 的参数\_MJ\_查询\_配额并集


联合组件时使用**MajorFunction**字段[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)结构操作已[ **IRP\_MJ\_查询\_配额**](irp-mj-query-quota.md)。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG                       Length;
    PSID                        StartSid;
    PFILE_GET_QUOTA_INFORMATION SidList;
    ULONG                       SidListLength;
    PVOID                       QuotaBuffer;
    PMLD                        MdlAddress;
  } QueryQuota;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**QueryQuota**  
结构，它包含以下成员。

**长度**  
缓冲区的长度，以字节为单位，该**QuotaBuffer**指向。

**StartSid**  
对安全的可选指针处开始扫描配额列表项的标识符 (SID)。 如果忽略此参数 SL\_索引\_FLT 中未设置指定标志\_IO\_参数\_操作的块结构或者如果**SidList**点为非空的列表。

**SidList**  
指向调用方提供的文件指针\_获取\_配额\_指定其配额信息是要查询的 Sid 的信息结构的输入的缓冲区。

**SidListLength**  
缓冲区的长度，以字节为单位，该**SidList**指向。

**QuotaBuffer**  
指向调用方提供[**文件\_配额\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540342)-其中的配额信息是要返回的结构化的输出缓冲区。

**MdlAddress**  
内存描述符列表 (MDL) 描述缓冲区的地址， **QuotaBuffer**指向。 此成员是可选的可以是**NULL**。

<a name="remarks"></a>备注
-------

[ **FLT\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff544673)结构[ **IRP\_MJ\_查询\_配额**](irp-mj-query-quota.md)操作包含表示的回调数据基于 IRP 的配额信息的查询操作的参数 ([**FLT\_回调\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff544620))结构。 包含在 FLT\_IO\_参数\_块结构。

IRP\_MJ\_查询\_配额是基于 IRP 的操作。

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

[**IRP\_MJ\_查询\_配额**](irp-mj-query-quota.md)

[**SID**](https://msdn.microsoft.com/library/windows/hardware/ff556740)

 

 






