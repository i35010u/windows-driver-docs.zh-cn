---
title: IRP_MJ_VOLUME_MOUNT 联合的 FLT_PARAMETERS
description: 当操作的 FLT \_ IO \_ 参数块结构的 MajorFunction 字段 \_ 为 IRP \_ MJ \_ 卷 \_ 装入时，将使用以下联合组件。
ms.assetid: 3fcc20da-b985-4d08-a0f7-9d95ddfb79d8
keywords:
- IRP_MJ_VOLUME_MOUNT 联合可安装文件系统驱动程序的 FLT_PARAMETERS
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
ms.openlocfilehash: d5b89ee1b65d5579c632f0539bcfbff14fbc0e4b
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063410"
---
# <a name="flt_parameters-for-irp_mj_volume_mount-union"></a>\_IRP \_ MJ \_ 卷 \_ 装载联合的 FLT 参数


当操作的[**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的**MajorFunction**字段为 IRP \_ MJ \_ 卷装入时，将使用以下联合组件 \_ 。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG DeviceType;
  } MountVolume;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**MountVolume**  
包含以下成员的结构。

**DeviceType**  
新装入的卷的文件系统卷设备对象的设备类型。 下列类型作之一：

文件 \_ 设备 \_ CD \_ ROM \_ 文件 \_ 系统

文件 \_ 设备 \_ 磁盘 \_ 文件 \_ 系统

文件 \_ 设备 \_ 网络 \_ 文件 \_ 系统

<a name="remarks"></a>备注
-------

IRP MJ 卷装入操作的 [**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters) 结构 \_ \_ \_ 包含由回调数据表示的卷装入操作的参数) 结构中 ([**FLT \_ 回调 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data) 。 它包含在 FLT \_ IO \_ 参数 \_ 块结构中。

IRP \_ MJ \_ 卷 \_ 装载是一种快速的 i/o 操作。

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

[**IRP \_ MJ \_ 文件 \_ 系统 \_ 控制**](irp-mj-file-system-control.md)

 

