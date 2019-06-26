---
title: FSCTL_LMR_GET_LINK_TRACKING_INFORMATION 控制代码
description: FSCTL\_LMR\_获取\_链接\_跟踪\_信息控制代码会检索跟踪的文件信息的链接。
ms.assetid: 8ddb8aca-4998-47ed-b8c9-39219e342c2c
keywords:
- FSCTL_LMR_GET_LINK_TRACKING_INFORMATION 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_LMR_GET_LINK_TRACKING_INFORMATION
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 882bf7ac134d64d967caade3d99ca591c227aed2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380136"
---
# <a name="fsctllmrgetlinktrackinginformation-control-code"></a>FSCTL\_LMR\_获取\_链接\_跟踪\_信息控制代码


**FSCTL\_LMR\_获取\_链接\_跟踪\_信息**控制代码检索跟踪的文件信息的链接。

若要执行此操作，调用[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)使用以下参数。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)仅。 远程卷文件对象指针。 此参数是必需的不能**NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)仅。 远程卷句柄。 此参数是必需的不能**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
该操作控制代码。 使用**FSCTL\_LMR\_获取\_链接\_跟踪\_信息**对于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
无。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
不使用。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
一个**链接\_跟踪\_信息**结构，其中包含跟踪文件的信息的链接。

``` syntax
typedef struct _LINK_TRACKING_INFORMATION {
  LINK_TRACKING_INFORMATION_TYPE  Type;
  UCHAR  VolumeId[16];
} LINK_TRACKING_INFORMATION, *PLINK_TRACKING_INFORMATION;
```

<a href="" id="type"></a>**Type**  
一个**链接\_跟踪\_信息\_类型**信息枚举值，指定的文件所驻留的文件系统类型。 如果此成员保留值**DfsLinkTrackingInformation**，该文件驻留在分布式的文件系统上。 如果此成员保留值**NtfsLinkTrackingInformation**，该文件驻留在 NTFS 文件系统上。

<a href="" id="volumeid"></a>**VolumeId**  
保存卷标识符的无符号的字符数组。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
大小 （字节） 通过指向的缓冲区*OutputBuffer*参数。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)将返回状态\_成功如果操作成功。 否则，相应的函数返回相应的 NTSTATUS 错误代码。

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
<td align="left">Ntifs.h （包括 Ntifs.h）</td>
</tr>
</tbody>
</table>

 

 





