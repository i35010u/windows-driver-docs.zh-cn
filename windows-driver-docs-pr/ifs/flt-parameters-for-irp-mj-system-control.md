---
title: IRP_MJ_SYSTEM_CONTROL 联合的 FLT_PARAMETERS
description: 操作的 FLT \_ IO \_ 参数块结构的 MajorFunction 字段 \_ 为 IRP \_ MJ \_ 系统 \_ 控制时使用的联合组件。
ms.assetid: 6f1c34b2-1c79-4372-8b94-afe4b50294d5
keywords:
- IRP_MJ_SYSTEM_CONTROL 联合可安装文件系统驱动程序的 FLT_PARAMETERS
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
ms.openlocfilehash: 49ca47d82f182738a663f53c25d3f40f0f0801f8
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063418"
---
# <a name="flt_parameters-for-irp_mj_system_control-union"></a>\_IRP \_ MJ \_ 系统 \_ 控制联合的 FLT 参数


操作的[**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的**MajorFunction**字段为 IRP \_ MJ \_ 系统控制时使用的联合组件 \_ 。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG_PTR ProviderId;
    PVOID     DataPath;
    ULONG     BufferSize;
    PVOID     Buffer;
  } WMI;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**WMI**  
包含以下成员的结构。

**ProviderId**  
此参数的意义取决于操作的次要函数代码。  (参见下面的 "备注" 部分。 ) 

**DataPath**  
此参数的意义取决于操作的次要函数代码。  (参见下面的 "备注" 部分。 ) 

**BufferSize**  
此参数的意义取决于操作的次要函数代码。  (参见下面的 "备注" 部分。 ) 

**Buffer**  
此参数的意义取决于操作的次要函数代码。  (参见下面的 "备注" 部分。 ) 

<a name="remarks"></a>备注
-------

IRP MJ 系统控制操作的 [**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters) 结构 \_ \_ \_ 包含由回调数据所表示的系统控件操作的参数， ([**FLT \_ 回调 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 结构。 它包含在 FLT \_ IO \_ 参数 \_ 块结构中。

IRP \_ MJ \_ 系统控制参数的意义 \_ 取决于次要函数代码。  (查看[**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的**MinorFunction**成员。 ) 有关详细信息，请参阅以下次要函数代码的参考条目：

[**IRP \_ MN \_ 更改 \_ 单一 \_ 实例**](../kernel/irp-mn-change-single-instance.md)

[**IRP \_ MN \_ 更改 \_ 单个 \_ 项目**](../kernel/irp-mn-change-single-item.md)

[**IRP \_ MN \_ 禁用 \_ 收集**](../kernel/irp-mn-disable-collection.md)

[**IRP \_ MN \_ 禁用 \_ 事件**](../kernel/irp-mn-disable-events.md)

[**IRP \_ MN \_ 启用 \_ 收集**](../kernel/irp-mn-enable-collection.md)

[**IRP \_ MN \_ 启用 \_ 事件**](../kernel/irp-mn-enable-events.md)

[**IRP \_ MN \_ EXECUTE \_ 方法**](../kernel/irp-mn-execute-method.md)

[**IRP \_ MN \_ 查询 \_ 所有 \_ 数据**](../kernel/irp-mn-query-all-data.md)

[**IRP \_ MN \_ 查询 \_ 单一 \_ 实例**](../kernel/irp-mn-query-single-instance.md)

[**IRP \_ MN \_ REGINFO**](../kernel/irp-mn-reginfo.md)

[**IRP \_ MN \_ REGINFO \_ EX**](../kernel/irp-mn-reginfo-ex.md)

IRP \_ MJ \_ 系统 \_ 控件是基于 IRP 的操作。

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

[**IRP \_ MN \_ 更改 \_ 单一 \_ 实例**](../kernel/irp-mn-change-single-instance.md)

[**IRP \_ MN \_ 更改 \_ 单个 \_ 项目**](../kernel/irp-mn-change-single-item.md)

[**IRP \_ MN \_ 禁用 \_ 收集**](../kernel/irp-mn-disable-collection.md)

[**IRP \_ MN \_ 禁用 \_ 事件**](../kernel/irp-mn-disable-events.md)

[**IRP \_ MN \_ 启用 \_ 收集**](../kernel/irp-mn-enable-collection.md)

[**IRP \_ MN \_ 启用 \_ 事件**](../kernel/irp-mn-enable-events.md)

[**IRP \_ MN \_ EXECUTE \_ 方法**](../kernel/irp-mn-execute-method.md)

[**IRP \_ MN \_ 查询 \_ 所有 \_ 数据**](../kernel/irp-mn-query-all-data.md)

[**IRP \_ MN \_ 查询 \_ 单一 \_ 实例**](../kernel/irp-mn-query-single-instance.md)

[**IRP \_ MN \_ REGINFO**](../kernel/irp-mn-reginfo.md)

[**IRP \_ MN \_ REGINFO \_ EX**](../kernel/irp-mn-reginfo-ex.md)

 

