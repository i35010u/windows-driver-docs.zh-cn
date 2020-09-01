---
title: IRP_MJ_PREPARE_MDL_WRITE 联合的 FLT_PARAMETERS
description: 当操作的 FLT \_ IO \_ 参数块结构的 MajorFunction 字段 \_ 为 IRP \_ MJ \_ PREPARE \_ MDL \_ 写入时，将使用以下联合组件。
ms.assetid: eebbb8d4-f46d-4aee-aeb3-7edcbd23207a
keywords:
- IRP_MJ_PREPARE_MDL_WRITE 联合可安装文件系统驱动程序的 FLT_PARAMETERS
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
ms.openlocfilehash: 9365afd24102ae121e571b735c40c3c3d7ca9fda
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065966"
---
# <a name="flt_parameters-for-irp_mj_prepare_mdl_write-union"></a>\_IRP \_ MJ \_ 准备 \_ MDL \_ 写入联合的 FLT 参数


当操作的[**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的**MajorFunction**字段为 IRP \_ MJ \_ PREPARE \_ MDL \_ 写入时，将使用以下联合组件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    LARGE_INTEGER           FileOffset;
    ULONG POINTER_ALIGNMENT Length;
    ULONG POINTER_ALIGNMENT Key;
    PMDL                    *MdlChain;
  } PrepareMdlWrite;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**PrepareMdlWrite**  
包含以下成员的结构。

**FileOffset**  
缓存文件中的起始字节。

**长度**  
要写入缓存文件的数据的长度（以字节为单位）。

**Key**  
与目标文件的字节范围锁关联的键值。 如果要写入的范围重叠，或者是文件内独占锁定范围的子范围，则此参数必须是该排他锁的键。 排他锁必须由调用线程的父进程持有;否则，将忽略此参数。

**MdlChain**  
指向一个变量的指针，该变量接收指向一个或多个内存描述符的链的指针 (MDL) 描述包含要写入的数据的页面。

<a name="remarks"></a>备注
-------

IRP MJ 准备 MDL 写入操作的 [**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters) 结构 \_ \_ \_ \_ 包含由回调数据表示的快速 I/o **PrepareMdlWrite** 操作的参数 ([**FLT \_ 回叫 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 结构。 它包含在 FLT \_ IO \_ 参数 \_ 块结构中。

如果快速 i/o IRP \_ MJ \_ 准备 \_ MDL \_ 写入请求失败，则 i/o 的颁发者会确定如何重新发出该请求。 微筛选器可能不会始终获取基于 IRP 的 IRP \_ MJ \_ MDL \_ 写入。 例如，可以将 IRP 请求重新颁发为 IRP \_ MJ \_ WRITE/IRP \_ MN \_ MDL。

IRP \_ MJ \_ 准备 \_ MDL \_ 写入是一种快速的 i/o 操作。

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

 

