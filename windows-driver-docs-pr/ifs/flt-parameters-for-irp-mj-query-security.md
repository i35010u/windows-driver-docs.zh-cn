---
title: FLT_PARAMETERS IRP_MJ_QUERY_SECURITY 联合
description: 联合组件时使用 FLT MajorFunction 字段\_IO\_参数\_操作的块结构是 IRP\_MJ\_查询\_安全。
ms.assetid: 7707fec2-9fe8-40f6-9f34-f43403551440
keywords:
- FLT_PARAMETERS IRP_MJ_QUERY_SECURITY 联合可安装文件系统驱动程序
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
ms.openlocfilehash: 73f22e34f84a446b3e922a3568e18de85cfcba25
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523105"
---
# <a name="fltparameters-for-irpmjquerysecurity-union"></a>FLT\_IRP 的参数\_MJ\_查询\_安全联合


联合组件时使用**MajorFunction**字段[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)结构操作已[ **IRP\_MJ\_查询\_安全**](irp-mj-query-security.md)。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    SECURITY_INFORMATION    SecurityInformation;
    ULONG POINTER_ALIGNMENT Length;
    PVOID                   SecurityBuffer;
    PDML                    MdlAddress;
  } QuerySecurity;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**QuerySecurity**  
结构，它包含以下成员。

**SecurityInformation**  
指向调用方提供[**安全\_信息**](security-information.md)值，该值指定要查询的安全信息。 下列情况之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SecurityInformation 值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>OWNER_SECURITY_INFORMATION</p></td>
<td align="left"><p>正在查询的对象的所有者标识符。 需要 READ_CONTROL 访问权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GROUP_SECURITY_INFORMATION</p></td>
<td align="left"><p>正在查询的对象的主要组标识符。 需要 READ_CONTROL 访问权限。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>正在查询的对象的自由访问控制列表 (DACL)。 需要 READ_CONTROL 访问权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>正在查询的对象的系统 ACL (SACL)。 需要 ACCESS_SYSTEM_SECURITY 访问权限。</p></td>
</tr>
</tbody>
</table>

 

**长度**  
缓冲区的长度，以字节为单位，该**SecurityBuffer**指向。

**SecurityBuffer**  
指向接收副本的指定对象的安全描述符的调用方提供输出缓冲区的指针。 调用进程必须有权查看对象的安全状态的指定的方面。 [**安全\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff556610)自相关格式返回结构。

**MdlAddress**  
描述缓冲区的内存描述符列表 (MDL) 的地址， **SecurityBuffer**指向。 此成员是可选的可以是**NULL**。

<a name="remarks"></a>备注
-------

[ **FLT\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff544673)结构[ **IRP\_MJ\_查询\_安全**](irp-mj-query-security.md)操作包含表示的回调数据基于 IRP 的安全信息的查询操作的参数 ([**FLT\_回调\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff544620))结构。 包含在[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)结构。

Windows XP 及更高版本，该对象的**TargetFileObject** FLT 成员\_IO\_参数\_块结构指向可以表示命名的数据流。 有关命名的数据流的详细信息，请参阅[**文件\_流\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540364)。

IRP\_MJ\_查询\_安全是一个基于 IRP 的操作。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Fltkernel.h （包括 Fltkernel.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**文件\_流\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540364)

[**FLT\_CALLBACK\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**IRP\_MJ\_QUERY\_SECURITY**](irp-mj-query-security.md)

[**安全\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff556610)

[**安全\_信息**](security-information.md)

 

 






