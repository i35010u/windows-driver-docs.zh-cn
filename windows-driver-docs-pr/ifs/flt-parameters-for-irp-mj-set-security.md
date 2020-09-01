---
title: IRP_MJ_SET_SECURITY 联合的 FLT_PARAMETERS
description: 操作的 FLT \_ IO \_ 参数块结构的 MajorFunction 字段 \_ 为 IRP \_ MJ \_ SET \_ SECURITY 时使用的联合组件。
ms.assetid: 9006ef50-bd2e-4c75-8c6b-8bb777122a75
keywords:
- IRP_MJ_SET_SECURITY 联合可安装文件系统驱动程序的 FLT_PARAMETERS
- FLT_PARAMETERS 联合可安装文件系统驱动程序
- PFLT_PARAMETERS 联合指针可安装的文件系统驱动程序
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
ms.openlocfilehash: 26d43c9539d6cfbda9ef7c7ef51976eae52d8d36
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066190"
---
# <a name="flt_parameters-for-irp_mj_set_security-union"></a>\_IRP MJ 的 FLT \_ 参数 \_ 设置 \_ 安全联合


操作的[**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的**MajorFunction**字段为[**IRP \_ MJ \_ SET \_ SECURITY**](irp-mj-set-security.md)时使用的联合组件。

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
包含以下成员的结构。

**SecurityInformation**  
指向 [**安全 \_ 信息**](security-information.md) 值的指针，它指定要在安全描述符中设置的安全信息。 此值可以是下列值之一。

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
<td align="left"><p>正在设置对象 (DACL) 的自由访问控制列表。 需要 WRITE_DAC 访问权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GROUP_SECURITY_INFORMATION</p></td>
<td align="left"><p>正在设置对象的主要组标识符。 需要 WRITE_OWNER 访问权限。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>OWNER_SECURITY_INFORMATION</p></td>
<td align="left"><p>正在设置对象的所有者标识符。 需要 WRITE_OWNER 访问权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>正在设置对象的系统 ACL (SACL) 。 需要 ACCESS_SYSTEM_SECURITY 访问权限。</p></td>
</tr>
</tbody>
</table>

 

**SecurityDescriptor**  
指向 [**安全 \_ 描述符**](/previous-versions/windows/hardware/drivers/ff556610(v=vs.85)) 结构的指针，该结构包含要分配给对象的安全信息的值。

<a name="remarks"></a>备注
-------

[**IRP \_ MJ \_ 集 \_ 安全**](irp-mj-set-security.md)操作的[**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构包含由回调数据表示的设置安全信息操作的参数) 结构中 ([**FLT \_ 回调 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)。 它包含在 FLT \_ IO \_ 参数 \_ 块结构中。

IRP \_ MJ \_ SET \_ SECURITY 是一项基于 IRP 的操作。

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
<td align="left">Fltkernel (包含 Fltkernel) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FLT \_ 回调 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT \_ 是 \_ FASTIO \_ 操作**](/windows-hardware/drivers/ddi/index)

[**FLT \_ 为 \_ FS \_ 筛选器 \_ 操作**](/previous-versions/ff544648(v=vs.85))

[**FLT \_ 是 \_ IRP \_ 操作**](/previous-versions/ff544654(v=vs.85))

[**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**IRP \_ MJ \_ 设置 \_ 安全性**](irp-mj-set-security.md)

[**安全 \_ 描述符**](/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))

[**安全 \_ 信息**](security-information.md)

 

