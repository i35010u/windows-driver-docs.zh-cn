---
title: FLT_PARAMETERS IRP_MJ_NETWORK_QUERY_OPEN 联合
description: 使用以下联合组件时 FLT MajorFunction 字段\_IO\_参数\_操作的块结构是 IRP\_MJ\_网络\_查询\_打开。
ms.assetid: bafe015c-a747-4d18-95d5-adad2ad1570b
keywords:
- FLT_PARAMETERS IRP_MJ_NETWORK_QUERY_OPEN 联合可安装文件系统驱动程序
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
ms.openlocfilehash: a7ed19b2c5a58fd1dba80d11b37c958640c01763
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353807"
---
# <a name="fltparameters-for-irpmjnetworkqueryopen-union"></a>FLT\_IRP 的参数\_MJ\_网络\_查询\_打开的并集


使用以下联合组件时**MajorFunction**字段[ **FLT\_IO\_参数\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构，该操作是 IRP\_MJ\_网络\_查询\_打开。

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
结构，它包含以下成员。

**Irp**  
创建表示此打开操作的 IRP 的指针。 此 IRP 是由文件系统的公共打开/创建代码，但不是实际完成。

**NetworkInformation**  
指向[**文件\_网络\_打开\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_network_open_information)-用于接收请求的文件信息的结构化的缓冲区。

<a name="remarks"></a>备注
-------

[ **FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)结构 IRP\_MJ\_网络\_查询\_打开操作包含的参数表示的回调数据的 NetworkQueryOpen 操作 ([**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 结构。 **FLT\_参数**结构包含在[ **FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构。

&gt; \[!请注意\]IRP 与关联的文件对象\_MJ\_网络\_查询\_打开是基于堆栈的对象。
&gt;为 NetworkQueryOpen 回调注册的筛选器不能引用此对象。 也就是说，不要调用 ObReferenceObject 或 ObDereferenceObject 对此基于堆栈的文件对象。 此外，不保存指针的对象。

 

IRP\_MJ\_网络\_查询\_打开是一个快速的 I/O 操作。 它是 FastIoQueryOpen (不 FastIoQueryNetworkOpenInfo) 操作的等效项。 筛选器必须注册此操作。

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


[**FILE\_NETWORK\_OPEN\_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_network_open_information)

[**FLT\_CALLBACK\_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_IS\_FASTIO\_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_IS\_IRP\_操作**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**FltQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltqueryinformationfile)

[**IRP\_MJ\_查询\_信息**](irp-mj-query-information.md)

[**ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntqueryinformationfile)

 

 






