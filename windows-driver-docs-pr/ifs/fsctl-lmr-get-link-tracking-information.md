---
title: FSCTL_LMR_GET_LINK_TRACKING_INFORMATION 控制代码
description: FSCTL \_ LMR \_ 获取 \_ 链接 \_ 跟踪 \_ 信息控制代码检索文件的链接跟踪信息。
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
ms.openlocfilehash: 61d58bdd4eff69e45713a77ba0b1314acde0ec38
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808345"
---
# <a name="fsctl_lmr_get_link_tracking_information-control-code"></a>FSCTL \_ LMR \_ 获取 \_ 链接 \_ 跟踪 \_ 信息控制代码


**FSCTL \_ LMR \_ 获取 \_ 链接 \_ 跟踪 \_ 信息** 控制代码检索文件的链接跟踪信息。

若要执行此操作，请调用具有以下参数的 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
仅 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 远程卷的文件对象指针。 此参数是必需的，不能为 **NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
仅 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。 远程卷的句柄。 此参数是必需的，不能为 **NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用 **FSCTL \_ LMR 获取此操作的 \_ \_ 链接 \_ 跟踪 \_ 信息** 。

<a href="" id="inputbuffer"></a>*InputBuffer*  
无。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
未使用。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
**链接 \_ 跟踪 \_ 信息** 结构，其中包含文件的链接跟踪信息。

``` syntax
typedef struct _LINK_TRACKING_INFORMATION {
  LINK_TRACKING_INFORMATION_TYPE  Type;
  UCHAR  VolumeId[16];
} LINK_TRACKING_INFORMATION, *PLINK_TRACKING_INFORMATION;
```

<a href="" id="type"></a>**类别**  
**链接 \_ 跟踪 \_ 信息 \_ 类型** 信息枚举值，用于指定文件所在的文件系统的类型。 如果此成员的值为 **DfsLinkTrackingInformation**，则该文件位于分布式文件系统上。 如果此成员的值为 **NtfsLinkTrackingInformation**，则该文件位于 NTFS 文件系统上。

<a href="" id="volumeid"></a>**VolumeId**  
包含卷标识符的无符号字符数组。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
*OutputBuffer* 参数指向的缓冲区的大小（以字节为单位）。

<a name="status-block"></a>状态块
------------

如果操作成功，则 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))返回状态 \_ SUCCESS。 否则，相应的函数将返回相应的 NTSTATUS 错误代码。

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
<td align="left">Ntifs (包含 Ntifs) </td>
</tr>
</tbody>
</table>

 

