---
title: FLT_PARAMETERS for IRP_MJ_SYSTEM_CONTROL union
description: 当 FLT\_IO\_参数\_块结构的操作为 IRP\_MJ\_SYSTEM\_控件时使用的联合组件。
ms.assetid: 6f1c34b2-1c79-4372-8b94-afe4b50294d5
keywords:
- FLT_PARAMETERS for IRP_MJ_SYSTEM_CONTROL union 可安装的文件系统驱动程序
- FLT_PARAMETERS 可安装的可安装文件系统驱动程序
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
ms.openlocfilehash: 33ffaaa9582216a58117b1f909e8147736113782
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841339"
---
# <a name="flt_parameters-for-irp_mj_system_control-union"></a>IRP\_MJ\_系统\_控制联合的 FLT\_参数


当[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的操作为 IRP\_MJ\_SYSTEM\_控件时**使用的联合**组件。

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
此参数的意义取决于操作的次要函数代码。 （请参阅下面的 "备注" 部分。）

**数据路径**  
此参数的意义取决于操作的次要函数代码。 （请参阅下面的 "备注" 部分。）

**BufferSize**  
此参数的意义取决于操作的次要函数代码。 （请参阅下面的 "备注" 部分。）

**宽限**  
此参数的意义取决于操作的次要函数代码。 （请参阅下面的 "备注" 部分。）

<a name="remarks"></a>备注
-------

IRP\_MJ\_系统\_控制操作的[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构包含回调数据表示的系统控件操作的参数（[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)）构造. 它包含在 FLT\_IO\_参数\_块结构。

IRP\_MJ\_系统\_控制参数的意义取决于次要函数代码。 （请参阅 FLT 的**MinorFunction**成员[ **\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构。）有关详细信息，请参阅以下次要函数代码的参考条目：

[**IRP\_MN\_更改\_单一\_实例**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-instance)

[**IRP\_MN\_更改\_单一\_项**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-item)

[**IRP\_MN\_禁用\_集合**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-collection)

[**IRP\_MN\_禁用\_事件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-events)

[**IRP\_MN\_启用\_收集**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-collection)

[**IRP\_MN\_启用\_事件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-events)

[**IRP\_MN\_EXECUTE\_方法**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method)

[**IRP\_MN\_查询\_所有\_数据**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data)

[**IRP\_MN\_QUERY\_单一\_实例**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)

[**IRP\_MN\_REGINFO**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)

[**IRP\_MN\_REGINFO\_EX**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)

IRP\_MJ\_系统\_控件是基于 IRP 的操作。

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
<td align="left">Fltkernel （包括 Fltkernel）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_\_FASTIO\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT\_\_FS\_筛选器\_操作**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_\_IRP\_操作**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**IRP\_MN\_更改\_单一\_实例**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-instance)

[**IRP\_MN\_更改\_单一\_项**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-item)

[**IRP\_MN\_禁用\_集合**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-collection)

[**IRP\_MN\_禁用\_事件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-events)

[**IRP\_MN\_启用\_收集**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-collection)

[**IRP\_MN\_启用\_事件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-events)

[**IRP\_MN\_EXECUTE\_方法**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method)

[**IRP\_MN\_查询\_所有\_数据**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data)

[**IRP\_MN\_QUERY\_单一\_实例**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)

[**IRP\_MN\_REGINFO**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)

[**IRP\_MN\_REGINFO\_EX**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)

 

 






