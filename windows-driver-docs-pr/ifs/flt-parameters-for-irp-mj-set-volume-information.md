---
title: FLT_PARAMETERS IRP_MJ_SET_VOLUME_INFORMATION 联合
description: 联合组件时使用 FLT MajorFunction 字段\_IO\_参数\_操作的块结构是 IRP\_MJ\_设置\_卷\_信息。
ms.assetid: 316ce14c-02ea-45ab-8a2f-1b096f631d23
keywords:
- FLT_PARAMETERS IRP_MJ_SET_VOLUME_INFORMATION 联合可安装文件系统驱动程序
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
ms.openlocfilehash: aaad1d33441b956694a21468d579a0609f9ff64a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380499"
---
# <a name="fltparameters-for-irpmjsetvolumeinformation-union"></a>FLT\_IRP 的参数\_MJ\_设置\_卷\_信息并集


联合组件时使用**MajorFunction**字段[ **FLT\_IO\_参数\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构操作已[ **IRP\_MJ\_设置\_卷\_信息**](irp-mj-set-volume-information.md)。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG                                  Length;
    FS_INFORMATION_CLASS POINTER_ALIGNMENT FsInformationClass;
    PVOID                                  VolumeBuffer;
  } SetVolumeInformation;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**SetVolumeInformation**  
结构，它包含以下成员。

**长度**  
在缓冲区的长度，以字节为单位， **VolumeBuffer**。

**FsInformationClass**  
要为卷设置的信息类型。 下列情况之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>FileFsControlInformation</strong></p></td>
<td align="left"><p>设置<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_control_information" data-raw-source="[&lt;strong&gt;FILE_FS_CONTROL_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_control_information)"> <strong>FILE_FS_CONTROL_INFORMATION</strong> </a>卷。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileFsLabelInformation</strong></p></td>
<td align="left"><p>设置<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_label_information" data-raw-source="[&lt;strong&gt;FILE_FS_LABEL_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_label_information)"> <strong>FILE_FS_LABEL_INFORMATION</strong> </a>卷。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFsObjectIdInformation</strong></p></td>
<td align="left"><p>设置<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_objectid_information" data-raw-source="[&lt;strong&gt;FILE_FS_OBJECTID_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_objectid_information)"> <strong>FILE_FS_OBJECTID_INFORMATION</strong> </a>卷。</p></td>
</tr>
</tbody>
</table>

 

**VolumeBuffer**  
指向包含要设置的卷信息的值的输入缓冲区的指针。

<a name="remarks"></a>备注
-------

[ **FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)结构[ **IRP\_MJ\_设置\_卷\_信息** ](irp-mj-set-volume-information.md)操作包含表示的回调数据设置卷信息操作的参数 ([**FLT\_回调\_数据** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 结构。 包含在 FLT\_IO\_参数\_块结构。

IRP\_MJ\_设置\_卷\_信息是基于 IRP 的操作。

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


[**文件\_FS\_控制\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_control_information)

[**文件\_FS\_标签\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_label_information)

[**文件\_FS\_OBJECTID\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_objectid_information)

[**FLT\_CALLBACK\_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_IS\_FASTIO\_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_IS\_IRP\_操作**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**IRP\_MJ\_设置\_卷\_信息**](irp-mj-set-volume-information.md)

[**ZwSetVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567112)

 

 






