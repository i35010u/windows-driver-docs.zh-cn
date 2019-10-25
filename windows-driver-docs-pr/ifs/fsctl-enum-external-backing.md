---
title: FSCTL_ENUM_EXTERNAL_BACKING 控制代码
description: FSCTL\_枚举\_外部\_后备控制代码开始或继续枚举具有后备源的卷上的文件。
ms.assetid: 86B07858-2F10-48EF-AEB5-7F4A23A55F7F
keywords:
- FSCTL_ENUM_EXTERNAL_BACKING 控制代码可安装的文件系统驱动程序
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
ms.openlocfilehash: da606fa058d4b545d0d037d9206cad2d278c9ee8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841317"
---
# <a name="fsctl_enum_external_backing-control-code"></a>FSCTL\_枚举\_外部\_后备控制代码


**FSCTL\_枚举\_外部\_后备**控制代码开始或继续枚举具有后备源的卷上的文件。 对于每个成功完成的请求，将返回支持的文件的标识符。 所有支持的文件都将被枚举，而不管哪个外部提供程序正在对其进行备份。 需要 **\_外部\_后备请求的后续 FSCTL\_枚举**来枚举卷上的所有支持的文件。

若要执行此操作，请调用具有以下参数的[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。

**Parameters**

<a href="" id="instance--in-"></a>*实例 \[\]*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 调用方的不透明实例指针。 此参数是必需的，不能为**NULL**。

<a href="" id="fileobject--in-"></a>*FileObject \[\]*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 文件指针对象，指定要卸除的卷。 此参数是必需的，不能为**NULL**。

<a href="" id="filehandle--in-"></a> *\]中的 FileHandle \[*  
仅[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。 要卸除的卷的文件句柄。 此参数是必需的，不能为**NULL**。

<a href="" id="fscontrolcode--in-"></a> *\]中的 FsControlCode \[*  
操作的控制代码。 使用**FSCTL\_枚举\_外部\_** 为此操作提供支持。

<a href="" id="inputbuffer"></a>*InputBuffer*  
无。 设置为**NULL**。

<a href="" id="inputbufferlength--in-"></a> *\]中的 InputBufferLength \[*  
设置为0。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[out\]*  
指向输出缓冲区的指针，该指针的大小必须足够大，以接收一个或多个**WOF\_外部\_文件\_ID**结构。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength \[out\]*  
*OutputBuffer*指向的输出缓冲区的大小。 *OutputBufferLength*必须 &gt;= **sizeof**（WOF\_外部\_文件\_ID）。

<a href="" id="lengthreturned--out-"></a>*LengthReturned \[out\]*  
指定成功完成后写入到*OutputBuffer*中的字节数。

<a name="status-block"></a>状态块
------------

如果操作成功，则[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)返回状态\_成功。 否则，相应的函数可能会返回以下 NTSTATUS 值之一。

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
<td align="left"><p>请求者没有管理权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p><em>OutputBuffer</em>指向的和由<em>OutputBufferLength</em>指定的输出缓冲区的长度太小。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_NO_MORE_FILES</strong></p></td>
<td align="left"><p>卷上的文件不再是后备源。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INTERNAL_ERROR</strong></p></td>
<td align="left"><p>请求的卷不可访问。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_INVALID_DEVICE_REQUEST</strong></p></td>
<td align="left"><p>后备服务不存在或未启动。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在*OutputBuffer*中返回的**WOF\_外部\_文件\_ID**结构包含用于已备份文件的唯一文件标识符。 结构在 ntifs 中定义如下。

```ManagedCPlusPlus
typedef struct _WOF_EXTERNAL_FILE_ID {
    FILE_ID_128 FileId;
} WOF_EXTERNAL_FILE_ID, *PWOF_EXTERNAL_FILE_ID;
```

**FSCTL\_枚举\_外部\_后备**请求会连续发出，以检索具有后备源的卷上的每个文件的标识符。 枚举所有文件后，将返回状态\_不\_更多\_文件状态代码。

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
<td align="left"><p>从 Windows 8.1 更新开始可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs （包括 Ntifs 或 Fltkernel）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

[**FSCTL\_获取\_外部\_后备**](fsctl-get-external-backing.md)

 

 






