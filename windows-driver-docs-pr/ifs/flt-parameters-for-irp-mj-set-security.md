---
title: FLT_PARAMETERS IRP_MJ_SET_SECURITY 联合
description: 联合组件时使用 FLT MajorFunction 字段\_IO\_参数\_操作的块结构是 IRP\_MJ\_设置\_安全。
ms.assetid: 9006ef50-bd2e-4c75-8c6b-8bb777122a75
keywords:
- FLT_PARAMETERS IRP_MJ_SET_SECURITY 联合可安装文件系统驱动程序
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
ms.openlocfilehash: 0e3a3d4c3f8b35612494d8f8cf1f40ac0c27c18d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522523"
---
# <a name="fltparameters-for-irpmjsetsecurity-union"></a>FLT\_IRP 的参数\_MJ\_设置\_安全联合


联合组件时使用**MajorFunction**字段[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)结构操作已[ **IRP\_MJ\_设置\_安全**](irp-mj-set-security.md)。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    SECURITY_INFORMATION SecurityInformation;
    PSECURITY_DESCRIPTOR SecurityDescriptor;
  } SetSecurity;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**SetSecurity**  
结构，它包含以下成员。

**SecurityInformation**  
指向[**安全\_信息**](security-information.md)值，该值指定哪些安全信息是在安全描述符中设置。 此值可以是以下值之一。

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
<td align="left"><p>DACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>设置对象的自由访问控制列表 (DACL)。 需要 WRITE_DAC 访问权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GROUP_SECURITY_INFORMATION</p></td>
<td align="left"><p>设置对象的主要组标识符。 需要 WRITE_OWNER 访问权限。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>OWNER_SECURITY_INFORMATION</p></td>
<td align="left"><p>设置对象的所有者标识符。 需要 WRITE_OWNER 访问权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>设置对象的系统 ACL (SACL)。 需要 ACCESS_SYSTEM_SECURITY 访问权限。</p></td>
</tr>
</tbody>
</table>

 

**SecurityDescriptor**  
指向[**安全\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff556610)结构，其中包含要分配给该对象的安全信息的值。

<a name="remarks"></a>备注
-------

[ **FLT\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff544673)结构[ **IRP\_MJ\_设置\_安全**](irp-mj-set-security.md)操作包含表示的回调数据集安全性信息操作的参数 ([**FLT\_回调\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff544620))结构。 包含在 FLT\_IO\_参数\_块结构。

IRP\_MJ\_设置\_安全是一个基于 IRP 的操作。

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


[**FLT\_CALLBACK\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**IRP\_MJ\_SET\_SECURITY**](irp-mj-set-security.md)

[**安全\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff556610)

[**安全\_信息**](security-information.md)

 

 






