---
title: IRP_MJ_NETWORK_QUERY_OPEN 联合的 FLT_PARAMETERS
description: 当操作的 FLT \_ IO \_ 参数块结构的 MajorFunction 字段 \_ 为 IRP \_ MJ \_ 网络 \_ 查询 \_ 打开时，将使用以下联合组件。
keywords:
- IRP_MJ_NETWORK_QUERY_OPEN 联合可安装文件系统驱动程序的 FLT_PARAMETERS
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
ms.openlocfilehash: cc77bc0ef23d0c8e246be70da68e0a80f022765f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839265"
---
# <a name="flt_parameters-for-irp_mj_network_query_open-union"></a>\_IRP \_ MJ \_ 网络 \_ 查询 \_ 开放式联合的 FLT 参数


当操作的 [**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的 **MajorFunction** 字段为 IRP \_ MJ \_ 网络 \_ 查询 \_ 打开时，将使用以下联合组件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    PIRP                           Irp;
    PFILE_NETWORK_OPEN_INFORMATION NetworkInformation;
  } NetworkQueryOpen;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**NetworkQueryOpen**  
包含以下成员的结构。

**Irp**  
指向表示此打开操作的 create IRP 的指针。 此 IRP 将由文件系统用于常见的打开/创建代码，但实际上并未完成。

**NetworkInformation**  
指向 [**文件网络的 \_ 指针 \_ 打开 \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_network_open_information)结构缓冲区以接收有关文件的请求信息。

<a name="remarks"></a>备注
-------

IRP MJ 网络查询打开操作的 [**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters) 结构 \_ \_ \_ \_ 包含回调数据所表示的 NetworkQueryOpen 操作的参数 ([**FLT \_ 回调 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 结构。 **FLT \_ 参数** 结构包含在 [**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构中。

> [!NOTE]
> 与 IRP \_ MJ 网络查询打开关联的文件对象 \_ \_ \_ 是一种基于堆栈的对象。
为 NetworkQueryOpen 回调注册的筛选器不得引用此对象。 也就是说，不要在此基于堆栈的文件对象上调用 ObReferenceObject 或 ObDereferenceObject。 此外，请不要保存指向对象的指针。

 

IRP \_ MJ \_ 网络 \_ 查询 \_ 打开是一种快速的 i/o 操作。 它等效于 FastIoQueryOpen (FastIoQueryNetworkOpenInfo) 操作。 必须为此操作注册筛选器。

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

## <a name="see-also"></a>请参阅


[**文件 \_ 网络 \_ 打开 \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_network_open_information)

[**FLT \_ 回调 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT \_ 是 \_ FASTIO \_ 操作**](/windows-hardware/drivers/ddi/index)

[**FLT \_ 为 \_ FS \_ 筛选器 \_ 操作**](/previous-versions/ff544648(v=vs.85))

[**FLT \_ 是 \_ IRP \_ 操作**](/previous-versions/ff544654(v=vs.85))

[**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FltQueryInformationFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueryinformationfile)

[**IRP \_ MJ \_ 查询 \_ 信息**](irp-mj-query-information.md)

[**ZwQueryInformationFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)

 

