---
title: FLT_PARAMETERS IRP_MJ_QUERY_INFORMATION 联合
description: 联合组件时使用 FLT MajorFunction 字段\_IO\_参数\_操作的块结构是 IRP\_MJ\_查询\_信息。
ms.assetid: 7fcd6881-1b6e-46eb-8476-d766f6fea7ef
keywords:
- FLT_PARAMETERS IRP_MJ_QUERY_INFORMATION 联合可安装文件系统驱动程序
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
ms.openlocfilehash: fd9bf754c0259f4eda99951fb25d497fad05863d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525436"
---
# <a name="fltparameters-for-irpmjqueryinformation-union"></a>FLT\_IRP 的参数\_MJ\_查询\_信息并集


联合组件时使用**MajorFunction**字段[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)结构操作已[ **IRP\_MJ\_查询\_信息**](irp-mj-query-information.md)。

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
结构，它包含以下成员。

**长度**  
在缓冲区的长度，以字节为单位， **InfoBuffer**。

**FileInformationClass**  
要返回的文件信息的类型。 下列情况之一：

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
<td align="left"><p>返回该文件的 FILE_ALL_INFORMATION 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileAttributeTagInformation</strong></p></td>
<td align="left"><p>返回<a href="https://msdn.microsoft.com/library/windows/hardware/ff545750" data-raw-source="[&lt;strong&gt;FILE_ATTRIBUTE_TAG_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545750)"> <strong>FILE_ATTRIBUTE_TAG_INFORMATION</strong> </a>文件的结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileBasicInformation</strong></p></td>
<td align="left"><p>返回<a href="https://msdn.microsoft.com/library/windows/hardware/ff545762" data-raw-source="[&lt;strong&gt;FILE_BASIC_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545762)"> <strong>FILE_BASIC_INFORMATION</strong> </a>文件的结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileCompressionInformation</strong></p></td>
<td align="left"><p>返回该文件的 FILE_COMPRESSION_INFORMATION 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileEaInformation</strong></p></td>
<td align="left"><p>返回该文件的 FILE_EA_INFORMATION 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileInternalInformation</strong></p></td>
<td align="left"><p>返回<a href="https://msdn.microsoft.com/library/windows/hardware/ff540318" data-raw-source="[&lt;strong&gt;FILE_INTERNAL_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540318)"> <strong>FILE_INTERNAL_INFORMATION</strong> </a>文件的结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileMoveClusterInformation</strong></p></td>
<td align="left"><p>返回该文件的 FILE_MOVE_CLUSTER_INFORMATION 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileNameInformation</strong></p></td>
<td align="left"><p>返回<a href="https://msdn.microsoft.com/library/windows/hardware/ff545817" data-raw-source="[&lt;strong&gt;FILE_NAME_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545817)"> <strong>FILE_NAME_INFORMATION</strong> </a>文件的结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileNetworkOpenInformation</strong></p></td>
<td align="left"><p>返回单个<a href="https://msdn.microsoft.com/library/windows/hardware/ff545822" data-raw-source="[&lt;strong&gt;FILE_NETWORK_OPEN_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545822)"> <strong>FILE_NETWORK_OPEN_INFORMATION</strong> </a>文件的结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FilePositionInformation</strong></p></td>
<td align="left"><p>返回单个<a href="https://msdn.microsoft.com/library/windows/hardware/ff545848" data-raw-source="[&lt;strong&gt;FILE_POSITION_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545848)"> <strong>FILE_POSITION_INFORMATION</strong> </a>文件的结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileStandardInformation</strong></p></td>
<td align="left"><p>返回单个<a href="https://msdn.microsoft.com/library/windows/hardware/ff545855" data-raw-source="[&lt;strong&gt;FILE_STANDARD_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545855)"> <strong>FILE_STANDARD_INFORMATION</strong> </a>文件的结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileStreamInformation</strong></p></td>
<td align="left"><p>返回单个<a href="https://msdn.microsoft.com/library/windows/hardware/ff540364" data-raw-source="[&lt;strong&gt;FILE_STREAM_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540364)"> <strong>FILE_STREAM_INFORMATION</strong> </a>文件的结构。</p></td>
</tr>
</tbody>
</table>

 

**InfoBuffer**  
其中的文件信息是要返回的输出缓冲区的指针。

<a name="remarks"></a>备注
-------

[ **FLT\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff544673)结构 IRP\_MJ\_查询\_操作包含的参数的查询信息的信息表示回调数据的操作 ([**FLT\_回调\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 结构。 包含在 FLT\_IO\_参数\_块结构。

IRP\_MJ\_查询\_信息可以是基于 IRP 的操作或快速 I/O 操作。

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


[**FILE\_ATTRIBUTE\_TAG\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff545750)

[**文件\_BASIC\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545762)

[**FILE\_INTERNAL\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff540318)

[**文件\_名称\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545817)

[**FILE\_NETWORK\_OPEN\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff545822)

[**文件\_位置\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545848)

**文件\_位置\_信息**
[**文件\_标准\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545855)

[**文件\_流\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540364)

[**FLT\_CALLBACK\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**IRP\_MJ\_查询\_信息**](irp-mj-query-information.md)

 

 






