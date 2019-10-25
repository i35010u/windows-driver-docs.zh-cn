---
title: FSCTL_GET_RETRIEVAL_POINTER_BASE 控制代码
description: FSCTL\_获取\_检索\_\_基准返回到相对于卷开头的文件系统的第一个逻辑群集号（LCN）的扇区偏移量。
ms.assetid: 2c342e58-ef9a-487a-beb9-4353dcbc8115
keywords:
- FSCTL_GET_RETRIEVAL_POINTER_BASE 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_GET_RETRIEVAL_POINTER_BASE
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 884431651cc443633e5cfd39cd8eb5c9573669ff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841305"
---
# <a name="fsctl_get_retrieval_pointer_base-control-code"></a>FSCTL\_获取\_检索\_\_基控制代码的指针


**FSCTL\_获取\_检索\_\_基准**返回到相对于卷开头的文件系统的第一个逻辑群集号（LCN）的扇区偏移量。

若要执行此操作，请调用具有以下参数的[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)函数或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)函数。

**Parameters**

<a href="" id="fileobject--in-"></a>*FileObject \[\]*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 FSCTL\_获取的卷的文件对象指针 **\_检索\_指针\_基**是检索基。 此参数是必需的，不能为**NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
仅[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。 卷的文件句柄， **FSCTL\_获取\_检索\_\_基的指针**。 此参数是必需的，不能为**NULL**。

必须使用 SE\_管理\_卷\_名称访问权限打开此句柄。 有关详细信息，请参阅[文件安全性和访问权限](https://docs.microsoft.com/windows/desktop/FileIO/file-security-and-access-rights)。

<a href="" id="fscontrolcode--in-"></a> *\]中的 FsControlCode \[*  
操作的控制代码。 使用**FSCTL\_获取此操作的\_检索\_指针\_基**。

<a href="" id="inputbuffer"></a>*InputBuffer*  
不与此操作一起使用。 设置为**NULL**。

<a href="" id="inputbufferlength--in-"></a> *\]中的 InputBufferLength \[*  
不与此操作一起使用。 设置为零。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[out\]*  
指向大\_整数的指针，该整数接收相对于卷开头的文件系统的第一个 LCN 的扇区偏移量。

<a href="" id="outputbufferlength--in-"></a> *\]中的 OutputBufferLength \[*  
输出缓冲区的大小（以字节为单位）。 此值必须是8。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZWFSCONTROLFILE**](https://msdn.microsoft.com/library/windows/hardware/ff566462)将返回状态\_SUCCESS 或适当的 NTSTATUS 值，如以下之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_SUCCESS</strong></p></td>
<td align="left"><p>操作成功。 OutputBuffer 包含相对于卷开头的文件系统的第一个 LCN 的扇区偏移量。</p></td>
</tr>
<tr class="even">
<td align="left"><p> <strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>用户不具有 SE_MANAGE_VOLUME 访问权限。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p>OutputBuffer 不够大，无法满足结果。 未将任何信息写入缓冲区。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>参数无效;例如，使用的句柄不是有效的卷句柄。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

添加 FSCTL 检索到的值\_获取\_检索\_指针\_从基到 FSCTL 检索到的值\_获取\_检索\_指针控制代码导致卷相对文件区偏移量。

FSCTL\_获取\_检索\_\_基控制代码可在 FastFAT 和 exFAT 设备上使用。 此功能支持为闪存驱动器等设备使用 BitLocker。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>Windows Server 2008 R2，Windows 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






