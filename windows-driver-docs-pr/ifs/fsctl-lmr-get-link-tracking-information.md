---
title: FSCTL_LMR_GET_LINK_TRACKING_INFORMATION 控制代码
description: FSCTL\_LMR\_获取\_链接\_跟踪\_信息控制代码检索文件的链接跟踪信息。
ms.assetid: 8ddb8aca-4998-47ed-b8c9-39219e342c2c
keywords:
- FSCTL_LMR_GET_LINK_TRACKING_INFORMATION 控制代码可安装的文件系统驱动程序
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
ms.openlocfilehash: c9f5451dd1a4cfffc11370eda7365599b3e24fee
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841289"
---
# <a name="fsctl_lmr_get_link_tracking_information-control-code"></a>FSCTL\_LMR\_获取\_链接\_跟踪\_信息控制代码


**FSCTL\_LMR\_获取\_链接\_跟踪\_信息**控制代码检索文件的链接跟踪信息。

若要执行此操作，请调用具有以下参数的[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 远程卷的文件对象指针。 此参数是必需的，不能为**NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
仅[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。 远程卷的句柄。 此参数是必需的，不能为**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用**FSCTL\_LMR\_获取\_链接\_跟踪**此操作的\_信息。

<a href="" id="inputbuffer"></a>*InputBuffer*  
无。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
不使用。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
**\_跟踪\_信息**结构的链接，其中包含文件的链接跟踪信息。

``` syntax
typedef struct _LINK_TRACKING_INFORMATION {
  LINK_TRACKING_INFORMATION_TYPE  Type;
  UCHAR  VolumeId[16];
} LINK_TRACKING_INFORMATION, *PLINK_TRACKING_INFORMATION;
```

<a href="" id="type"></a>**类别**  
**\_跟踪\_信息的链接，\_类型**信息枚举值，该值指定文件所在的文件系统的类型。 如果此成员的值为**DfsLinkTrackingInformation**，则该文件位于分布式文件系统上。 如果此成员的值为**NtfsLinkTrackingInformation**，则该文件位于 NTFS 文件系统上。

<a href="" id="volumeid"></a>**VolumeId**  
包含卷标识符的无符号字符数组。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
*OutputBuffer*参数指向的缓冲区的大小（以字节为单位）。

<a name="status-block"></a>状态块
------------

如果操作成功，则[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)返回状态\_成功。 否则，相应的函数将返回相应的 NTSTATUS 错误代码。

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
<td align="left">Ntifs （包括 Ntifs）</td>
</tr>
</tbody>
</table>

 

 





