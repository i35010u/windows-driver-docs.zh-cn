---
title: FSCTL_SUSPEND_OVERLAY 控制代码
description: FSCTL\_挂起\_覆盖控制代码挂起附加到导致备份源无法访问，从而使其可以修改或删除的卷的备份源。
ms.assetid: 5BC73E77-86A0-4A7D-BCBA-F3E8DA980701
keywords:
- FSCTL_SUSPEND_OVERLAY 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_SUSPEND_OVERLAY
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff971708868ee5dfc2b0366d7df94310f3e86d0d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365905"
---
# <a name="fsctlsuspendoverlay-control-code"></a>FSCTL\_挂起\_OVERLAY 控件代码


**FSCTL\_挂起\_覆盖**控制代码挂起附加到导致备份源无法访问，从而使其可以修改或删除的卷的备份源。

若要执行此操作，调用[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)使用以下参数。

``` syntax
BOOL 
   WINAPI 
   DeviceIoControl( (HANDLE)       hDevice,         // handle to device
                    (DWORD)        FSCTL_SUSPEND_OVERLAY, // dwIoControlCode
                    (LPDWORD)      lpInBuffer,      // input buffer
                    (DWORD)        nInBufferSize,   // size of input buffer
                    (LPDWORD)      lpOutBuffer,     // output buffer
                    (DWORD)        nOutBufferSize,  // size of output buffer
                    (LPDWORD)      lpBytesReturned, // number of bytes returned
                    (LPOVERLAPPED) lpOverlapped );  // OVERLAPPED structure
```

**Parameters**

<a href="" id="instance--in-"></a>*实例\[中\]*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)仅。 调用方不透明实例指针。 此参数是必需的不能为 NULL。

<a href="" id="fileobject--in-"></a>*FileObject \[in\]*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)仅。 为其更新在覆盖区上的卷的文件指针对象。 此参数是必需的不能为 NULL。

<a href="" id="filehandle--in-"></a>*FileHandle \[in\]*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)仅。 为其更新在覆盖区上的卷的句柄。 此参数是必需的不能为 NULL。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode \[in\]*  
操作的控制代码。 使用**FSCTL\_挂起\_覆盖**对于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向输入缓冲区，必须包含[ **WOF\_外部\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_wof_external_info)结构。 在需要时，其他提供程序特定的数据是包含后立即**WOF\_外部\_信息**。 如果提供程序为 WIM 文件， [ **WIM\_提供程序\_挂起\_覆盖\_输入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_wim_provider_suspend_overlay_input)结构是在**WOF\_外部\_信息**。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength \[in\]*  
设置为**sizeof**([**WOF\_外部\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_wof_external_info)) 加上任何其他提供程序输入数据的大小。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer\[出\]*  
不使用。 设置为 NULL。

<a href="" id="outputbufferlength--in-"></a>*OutputBufferLength \[in\]*  
设置为 0。

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
<td align="left"><p>指向输入缓冲区的长度<em>InputBuffer</em>，并通过指定<em>InputBufferLength</em>，太小。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_INTERNAL_ERROR</strong></p></td>
<td align="left"><p>该请求的卷不可访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_DEVICE_REQUEST</strong></p></td>
<td align="left"><p>备份服务不存在或未启动。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果要删除的备份源 Windows 映像格式 (WIM) 文件，将包含输入的缓冲区[ **WOF\_外部\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_wof_external_info)结构跟[ **WIM\_提供程序\_挂起\_覆盖\_输入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_wim_provider_suspend_overlay_input)结构。 *InputBufferLength*在这种情况下将为**sizeof**(WOF\_外部\_INFO) + **sizeof**([**WIM\_提供程序\_删除\_覆盖\_输入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_wim_provider_remove_overlay_input))。 **DataSourceId**中的值**WIM\_提供程序\_挂起\_覆盖\_输入**之前在中添加的WIM文件必须是[ **FSCTL\_添加\_覆盖**](fsctl-add-overlay.md)请求。

其他支持提供程序将定义他们自己特定的输入的参数的结构。

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
<td align="left">Ntifs.h （包括 Ntifs.h 或 Fltkernel.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FSCTL\_REMOVE\_OVERLAY**](fsctl-remove-overlay.md)

[**FSCTL\_UPDATE\_OVERLAY**](fsctl-update-overlay.md)

[**FSCTL\_GET\_EXTERNAL\_BACKING**](fsctl-get-external-backing.md)

[**FSCTL\_SET\_EXTERNAL\_BACKING**](fsctl-set-external-backing.md)

 

 






