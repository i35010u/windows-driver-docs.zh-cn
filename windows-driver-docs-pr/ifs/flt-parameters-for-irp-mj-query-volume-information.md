---
title: FLT_PARAMETERS IRP_MJ_QUERY_VOLUME_INFORMATION 联合
description: 联合组件时使用 FLT MajorFunction 字段\_IO\_参数\_操作的块结构是 IRP\_MJ\_查询\_卷\_信息。
ms.assetid: fc790885-a378-40dc-829d-94e75a7c6f13
keywords:
- FLT_PARAMETERS IRP_MJ_QUERY_VOLUME_INFORMATION 联合可安装文件系统驱动程序
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
ms.openlocfilehash: 0b349d79a89b9e4ec9c11e61dd65a705277ca31d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563669"
---
# <a name="fltparameters-for-irpmjqueryvolumeinformation-union"></a>FLT\_IRP 的参数\_MJ\_查询\_卷\_信息并集


联合组件时使用**MajorFunction**字段[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)结构操作已[ **IRP\_MJ\_查询\_卷\_信息**](irp-mj-query-volume-information.md)。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG                                  Length;
    FS_INFORMATION_CLASS POINTER_ALIGNMENT FsInformationClass;
  } QueryVolumeInformation;
  PVOID  VolumeBuffer;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**QueryVolumeInformation**  
结构，它包含以下成员。

**长度**  
在缓冲区的长度，以字节为单位， **VolumeBuffer**。

**FsInformationClass**  
卷文件系统返回的信息的类型。 下列情况之一：

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
<td align="left"><a href="" id="filefsattributeinformation"></a>
<strong>FileFsAttributeInformation</strong></td>
<td align="left"><p>返回<a href="https://msdn.microsoft.com/library/windows/hardware/ff540287" data-raw-source="[&lt;strong&gt;FILE_FS_VOLUME_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540287)"> <strong>FILE_FS_VOLUME_INFORMATION</strong> </a> ，包含有关该卷，卷标签、 序列号和创建时间等信息。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="" id="filefscontrolinformation"></a>
<strong>FileFsControlInformation</strong></td>
<td align="left"><p>返回<a href="https://msdn.microsoft.com/library/windows/hardware/ff540258" data-raw-source="[&lt;strong&gt;FILE_FS_CONTROL_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540258)"> <strong>FILE_FS_CONTROL_INFORMATION</strong> </a>结构，其中包含有关卷的文件系统控制信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="" id="filefsdeviceinformation"></a>
<strong>FileFsDeviceInformation</strong></td>
<td align="left"><p>返回<a href="https://msdn.microsoft.com/library/windows/hardware/ff545788" data-raw-source="[&lt;strong&gt;FILE_FS_DEVICE_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545788)"> <strong>FILE_FS_DEVICE_INFORMATION</strong> </a>结构，其中包含该卷的设备信息。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="" id="filefsdriverpathinformation"></a>
<strong>FileFsDriverPathInformation</strong></td>
<td align="left"><p>返回<a href="https://msdn.microsoft.com/library/windows/hardware/ff540262" data-raw-source="[&lt;strong&gt;FILE_FS_DRIVER_PATH_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540262)"> <strong>FILE_FS_DRIVER_PATH_INFORMATION</strong> </a>结构，其中包含有关指定驱动程序是在该卷的 I/O 路径信息。 IRP_MJ_QUERY_VOLUME_INFORMATION 请求的发起方必须发送 IRP 到文件系统卷设备堆栈之前在到 FILE_FS_DRIVER_PATH_INFORMATION 结构存储驱动程序的名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="" id="filefsfullsizeinformation"></a>
<strong>FileFsFullSizeInformation</strong></td>
<td align="left"><p>返回<a href="https://msdn.microsoft.com/library/windows/hardware/ff540267" data-raw-source="[&lt;strong&gt;FILE_FS_FULL_SIZE_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540267)"> <strong>FILE_FS_FULL_SIZE_INFORMATION</strong> </a>结构，其中包含有关在卷上的总可用空间量的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="" id="filefsobjectidinformation"></a>
<strong>FileFsObjectIdInformation</strong></td>
<td align="left"><p>返回<a href="https://msdn.microsoft.com/library/windows/hardware/ff540274" data-raw-source="[&lt;strong&gt;FILE_FS_OBJECTID_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540274)"> <strong>FILE_FS_OBJECTID_INFORMATION</strong> </a>结构，其中包含该卷的特定于系统文件的对象 ID 信息。 请注意，这是不与相同 (全局唯一标识符 [GUID]-基于) 操作系统分配的唯一卷名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="" id="filefssizeinformation"></a>
<strong>FileFsSizeInformation</strong></td>
<td align="left"><p>返回<a href="https://msdn.microsoft.com/library/windows/hardware/ff540282" data-raw-source="[&lt;strong&gt;FILE_FS_SIZE_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540282)"> <strong>FILE_FS_SIZE_INFORMATION</strong> </a>结构，其中包含有关可供用户与发起 IRP_MJ_ 线程关联的卷上的空间量的信息QUERY_VOLUME_INFORMATION 请求。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="" id="filefsvolumeinformation"></a>
<strong>FileFsVolumeInformation</strong></td>
<td align="left"><p>返回<a href="https://msdn.microsoft.com/library/windows/hardware/ff540287" data-raw-source="[&lt;strong&gt;FILE_FS_VOLUME_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540287)"> <strong>FILE_FS_VOLUME_INFORMATION</strong> </a> ，包含有关该卷，卷标签、 序列号和创建时间等信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="" id="filefssectorsizeinformation"></a>
<strong>FileFsSectorSizeInformation</strong></td>
<td align="left"><p>返回<a href="https://msdn.microsoft.com/library/windows/hardware/ff540262" data-raw-source="[&lt;strong&gt;FILE_FS_SECTOR_SIZE_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540262)"> <strong>FILE_FS_SECTOR_SIZE_INFORMATION</strong> </a>结构，其中包含有关物理和逻辑扇区大小的卷的信息。</p></td>
</tr>
</tbody>
</table>

 

**VolumeBuffer**  
指向其中的卷信息是要返回的输出缓冲区的指针。

<a name="remarks"></a>备注
-------

[ **FLT\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff544673)结构 IRP\_MJ\_查询\_卷\_操作包含的参数的信息基于 IRP 的回调数据由表示查询卷信息操作 ([**FLT\_回调\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 结构。 包含在 FLT\_IO\_参数\_块结构。

IRP\_MJ\_查询\_卷\_信息是基于 IRP 的操作。

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


[**文件\_FS\_属性\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540251)

[**文件\_FS\_控制\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540258)

[**FILE\_FS\_DEVICE\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff545788)

[**文件\_FS\_驱动程序\_路径\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540262)

[**文件\_FS\_完整\_大小\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540267)

[**文件\_FS\_OBJECTID\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540274)

**文件\_FS\_扇区\_大小\_信息**
[**文件\_FS\_大小\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540282)

[**文件\_FS\_卷\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540287)

[**FLT\_CALLBACK\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**IRP\_MJ\_查询\_信息**](irp-mj-query-information.md)

[**ZwQueryVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567070)

 

 






