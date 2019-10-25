---
title: FLT_PARAMETERS for IRP_MJ_NETWORK_QUERY_OPEN union
description: 当 FLT\_IO\_参数\_块结构的操作为 IRP\_MJ\_打开的网络\_查询时，将使用以下联合组件。
ms.assetid: bafe015c-a747-4d18-95d5-adad2ad1570b
keywords:
- FLT_PARAMETERS for IRP_MJ_NETWORK_QUERY_OPEN union 可安装的文件系统驱动程序
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
ms.openlocfilehash: d7e9242c16bd2ad36fb110cb98f97914bde3f829
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841374"
---
# <a name="flt_parameters-for-irp_mj_network_query_open-union"></a>FLT\_IRP\_MJ\_网络\_查询\_打开联合


当[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)**结构的操作**为 IRP\_MJ\_打开的网络\_查询时，将使用以下联合组件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    PIRP                           Irp;
    PFILE_NETWORK_OPEN_INFORMATION NetworkInformation;
  } NetworkQueryOpen;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**NetworkQueryOpen**  
包含以下成员的结构。

**Irp**  
指向表示此打开操作的 create IRP 的指针。 此 IRP 将由文件系统用于常见的打开/创建代码，但实际上并未完成。

**System.net.networkinformation**  
指向[**文件\_的指针\_打开\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_network_open_information)结构缓冲区来接收有关文件的请求信息。

<a name="remarks"></a>备注
-------

IRP\_MJ\_网络\_查询\_打开操作的[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构包含回调数据表示的 NetworkQueryOpen 操作的参数（[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)）结构。 **FLT\_参数**结构包含在[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构中。

&gt; \[！请注意\] 与 IRP\_MJ 关联的文件对象\_网络\_查询\_打开是一种基于堆栈的对象。
&gt;为 NetworkQueryOpen 回调注册的筛选器不得引用此对象。 也就是说，不要在此基于堆栈的文件对象上调用 ObReferenceObject 或 ObDereferenceObject。 此外，请不要保存指向对象的指针。

 

IRP\_MJ\_网络\_查询\_打开是一种快速的 i/o 操作。 它等效于 FastIoQueryOpen （而非 FastIoQueryNetworkOpenInfo）操作。 必须为此操作注册筛选器。

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


[**文件\_网络\_打开\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_network_open_information)

[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_\_FASTIO\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT\_\_FS\_筛选器\_操作**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_\_IRP\_操作**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FltQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueryinformationfile)

[**IRP\_MJ\_查询\_信息**](irp-mj-query-information.md)

[**ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)

 

 






