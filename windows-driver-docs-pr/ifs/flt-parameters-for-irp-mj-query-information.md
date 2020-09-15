---
title: IRP_MJ_QUERY_INFORMATION 联合的 FLT_PARAMETERS
description: 操作的 FLT \_ IO \_ 参数块结构的 MajorFunction 字段 \_ 为 IRP \_ MJ \_ 查询 \_ 信息时使用的联合组件。
ms.assetid: 7fcd6881-1b6e-46eb-8476-d766f6fea7ef
keywords:
- IRP_MJ_QUERY_INFORMATION 联合可安装文件系统驱动程序的 FLT_PARAMETERS
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
ms.openlocfilehash: 8a50cf092fc77ed3bca1dbe5e215474556bad0c3
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102986"
---
# <a name="flt_parameters-for-irp_mj_query_information-union"></a>\_IRP \_ MJ \_ 查询 \_ 信息联合的 FLT 参数


操作的[**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的**MajorFunction**字段为[**IRP \_ MJ \_ 查询 \_ 信息**](irp-mj-query-information.md)时使用的联合组件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG                                    Length;
    FILE_INFORMATION_CLASS POINTER_ALIGNMENT FileInformationClass;
    PVOID                                    InfoBuffer;
  } QueryFileInformation;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**QueryFileInformation**  
包含以下成员的结构。

**长度**  
**InfoBuffer**缓冲区的长度（以字节为单位）。

**FileInformationClass**  
要返回的文件信息的类型。 下列类型作之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>FileAllInformation</strong></p></td>
<td align="left"><p>返回文件的 FILE_ALL_INFORMATION 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileAttributeTagInformation</strong></p></td>
<td align="left"><p>返回文件的 <a href="/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_attribute_tag_information" data-raw-source="[&lt;strong&gt;FILE_ATTRIBUTE_TAG_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_attribute_tag_information)"><strong>FILE_ATTRIBUTE_TAG_INFORMATION</strong></a> 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileBasicInformation</strong></p></td>
<td align="left"><p>返回文件的 <a href="/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information" data-raw-source="[&lt;strong&gt;FILE_BASIC_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information)"><strong>FILE_BASIC_INFORMATION</strong></a> 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileCompressionInformation</strong></p></td>
<td align="left"><p>返回文件的 FILE_COMPRESSION_INFORMATION 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileEaInformation</strong></p></td>
<td align="left"><p>返回文件的 FILE_EA_INFORMATION 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileInternalInformation</strong></p></td>
<td align="left"><p>返回文件的 <a href="/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_internal_information" data-raw-source="[&lt;strong&gt;FILE_INTERNAL_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_internal_information)"><strong>FILE_INTERNAL_INFORMATION</strong></a> 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileMoveClusterInformation</strong></p></td>
<td align="left"><p>返回文件的 FILE_MOVE_CLUSTER_INFORMATION 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileNameInformation</strong></p></td>
<td align="left"><p>返回文件的 <a href="/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_name_information" data-raw-source="[&lt;strong&gt;FILE_NAME_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_name_information)"><strong>FILE_NAME_INFORMATION</strong></a> 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileNetworkOpenInformation</strong></p></td>
<td align="left"><p>返回文件的单个 <a href="/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_network_open_information" data-raw-source="[&lt;strong&gt;FILE_NETWORK_OPEN_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_network_open_information)"><strong>FILE_NETWORK_OPEN_INFORMATION</strong></a> 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FilePositionInformation</strong></p></td>
<td align="left"><p>返回文件的单个 <a href="/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information" data-raw-source="[&lt;strong&gt;FILE_POSITION_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information)"><strong>FILE_POSITION_INFORMATION</strong></a> 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileStandardInformation</strong></p></td>
<td align="left"><p>返回文件的单个 <a href="/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_standard_information" data-raw-source="[&lt;strong&gt;FILE_STANDARD_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_standard_information)"><strong>FILE_STANDARD_INFORMATION</strong></a> 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileStreamInformation</strong></p></td>
<td align="left"><p>返回文件的单个 <a href="/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stream_information" data-raw-source="[&lt;strong&gt;FILE_STREAM_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stream_information)"><strong>FILE_STREAM_INFORMATION</strong></a> 结构。</p></td>
</tr>
</tbody>
</table>

 

**InfoBuffer**  
一个指针，指向要返回文件信息的输出缓冲区。

<a name="remarks"></a>注解
-------

IRP MJ 查询信息操作的 [**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters) 结构 \_ \_ \_ 包含由回调数据表示的查询信息操作的参数) 结构中 ([**FLT \_ 回调 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data) 。 它包含在 FLT \_ IO \_ 参数 \_ 块结构中。

IRP \_ MJ \_ 查询 \_ 信息可以是基于 IRP 的操作，也可以是快速 i/o 操作。

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


[**文件 \_ 属性 \_ 标记 \_ 信息**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_attribute_tag_information)

[**文件 \_ 基本 \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information)

[**文件 \_ 内部 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_internal_information)

[**文件名 \_ \_ 信息**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_name_information)

[**文件 \_ 网络 \_ 打开 \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_network_open_information)

[**文件 \_ 位置 \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information)

**文件 \_位置 \_ 信息** 
 [**文件 \_ 标准 \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_standard_information)

[**文件 \_ 流 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stream_information)

[**FLT \_ 回调 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT \_ 是 \_ FASTIO \_ 操作**](/windows-hardware/drivers/ddi/index)

[**FLT \_ 为 \_ FS \_ 筛选器 \_ 操作**](/previous-versions/ff544648(v=vs.85))

[**FLT \_ 是 \_ IRP \_ 操作**](/previous-versions/ff544654(v=vs.85))

[**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**IRP \_ MJ \_ 查询 \_ 信息**](irp-mj-query-information.md)

