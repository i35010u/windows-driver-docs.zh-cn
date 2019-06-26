---
title: FSCTL_ENUM_EXTERNAL_BACKING 控制代码
description: FSCTL\_ENUM\_外部\_支持控件代码开始或继续拥有备份源卷上文件的枚举。
ms.assetid: 86B07858-2F10-48EF-AEB5-7F4A23A55F7F
keywords:
- FSCTL_ENUM_EXTERNAL_BACKING 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_ENUM_EXTERNAL_BACKING
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b99344481f5b1a94b01bca30352c24632e2ba590
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365056"
---
# <a name="fsctlenumexternalbacking-control-code"></a>FSCTL\_ENUM\_外部\_支持控件代码


**FSCTL\_枚举\_外部\_备份**控制代码开始或继续拥有备份源卷上文件的枚举。 对于请求的每个成功完成后，将返回已备份文件的标识符。 无论哪一个外部提供程序支持它枚举所有已备份的文件。 连续**FSCTL\_枚举\_外部\_备份**请求才能枚举卷上的所有备份的文件。

若要执行此操作，调用[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)使用以下参数。

**Parameters**

<a href="" id="instance--in-"></a>*实例\[中\]*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)仅。 调用方的不透明实例指针。 此参数是必需的不能**NULL**。

<a href="" id="fileobject--in-"></a>*FileObject \[in\]*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)仅。 文件指针对象指定要卸除卷。 此参数是必需的不能**NULL**。

<a href="" id="filehandle--in-"></a>*FileHandle \[in\]*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)仅。 要卸除的卷的文件句柄。 此参数是必需的不能**NULL**。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode \[in\]*  
操作的控制代码。 使用**FSCTL\_枚举\_外部\_备份**对于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
无。 设置为**NULL**。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength \[in\]*  
设置为 0。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer\[出\]*  
指向输出缓冲区，其必须具有足够大，接收一个或多个大小的指针**WOF\_外部\_文件\_ID**结构。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength\[出\]*  
指向输出缓冲区的大小*OutputBuffer*。 *OutputBufferLength*必须是&gt; =  **sizeof**(WOF\_外部\_文件\_ID)。

<a href="" id="lengthreturned--out-"></a>*LengthReturned\[出\]*  
指定写入的字节数*OutputBuffer*在成功完成。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)将返回状态\_成功如果操作成功。 否则，相应的函数可能返回以下 NTSTATUS 值之一。

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
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>请求者不具有管理权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p>指向输出缓冲区的长度<em>OutputBuffer</em>并指定由<em>OutputBufferLength</em>太小。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_NO_MORE_FILES</strong></p></td>
<td align="left"><p>更多文件的卷上有一个备份源。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INTERNAL_ERROR</strong></p></td>
<td align="left"><p>该请求的卷不可访问。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_INVALID_DEVICE_REQUEST</strong></p></td>
<td align="left"><p>备份服务不存在或未启动。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**WOF\_外部\_文件\_ID**结构中返回*OutputBuffer*包含已备份文件的唯一文件标识符。 结构定义中 ntifs.h 如下所示。

```ManagedCPlusPlus
typedef struct _WOF_EXTERNAL_FILE_ID {
    FILE_ID_128 FileId;
} WOF_EXTERNAL_FILE_ID, *PWOF_EXTERNAL_FILE_ID;
```

一个**FSCTL\_枚举\_外部\_备份**连续发出请求以检索具有备份源卷上的每个文件的标识符。 当枚举所有文件时，状态\_否\_详细\_返回文件状态代码。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>从 Windows 8.1 更新开始可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h （包括 Ntifs.h 或 Fltkernel.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

[**FSCTL\_GET\_EXTERNAL\_BACKING**](fsctl-get-external-backing.md)

 

 






