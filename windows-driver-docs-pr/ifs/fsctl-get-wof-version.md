---
title: FSCTL_GET_WOF_VERSION 控制代码
description: FSCTL\_GET\_WOF\_版本 i/o 控制代码（IOCTL）用于查询用于支持特定提供程序的驱动程序版本。
ms.assetid: 0E3C3C7E-2A89-4CA8-8741-7C057E063155
keywords:
- FSCTL_GET_WOF_VERSION 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_GET_WOF_VERSION
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a479f3a6bd0d0283e82847725b77d9fc7a1f31cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841301"
---
# <a name="fsctl_get_wof_version-control-code"></a>FSCTL\_获取 WOF\_版本控制代码\_


**FSCTL\_GET\_WOF\_版本**i/o 控制代码（IOCTL）用于查询用于支持特定提供程序的驱动程序版本。

若要执行此操作，请调用具有以下参数的[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。

``` syntax
BOOL 
   WINAPI 
   DeviceIoControl( (HANDLE)       hDevice,         // handle to device
                    (DWORD)        FSCTL_GET_WOF_VERSION, // dwIoControlCode
                    (LPDWORD)      lpInBuffer,      // input buffer
                    (DWORD)        nInBufferSize,   // size of input buffer
                    (LPDWORD)      lpOutBuffer,     // output buffer
                    (DWORD)        nOutBufferSize,  // size of output buffer
                    (LPDWORD)      lpBytesReturned, // number of bytes returned
                    (LPOVERLAPPED) lpOverlapped );  // OVERLAPPED structure
```

**Parameters**

<a href="" id="hdevice--in-"></a> *\]中的 hDevice \[*  
设备的句柄。 若要获取设备句柄，请调用[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)函数或类似的 API。

<a href="" id="dwiocontrolcode--in-"></a> *\]中的 dwIoControlCode \[*  
操作的控制代码。 使用**FSCTL\_获取此操作\_WOF\_版本**。

<a href="" id="lpinbuffer"></a>*lpInBuffer*  
操作的输入缓冲区。 这是指向[**WOF\_外部\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)结构的指针。

<a href="" id="ninbuffersize--in-"></a> *\]中的 nInBufferSize \[*  
输入缓冲区的大小（以字节为单位）。 这应为**sizeof**（[**WOF\_外部\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)）。

<a href="" id="lpoutbuffer--out-"></a>*lpOutBuffer \[out\]*  
操作的输出缓冲区。 这是指向[**WOF\_版本\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_version_info)结构的指针。

<a href="" id="noutbuffersize--in-"></a> *\]中的 nOutBufferSize \[*  
输出缓冲区的大小（以字节为单位）。 应为**sizeof**（[**WOF\_版本\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_version_info)）。

<a href="" id="lpbytesreturned--out-"></a>*lpBytesReturned \[out\]*  
**LPDWORD**

指向一个变量的指针，该变量接收存储在输出缓冲区中的数据的大小（以字节为单位）。

如果输出缓冲区太小，则调用失败， [**GetLastError**](https://docs.microsoft.com/windows/desktop/api/errhandlingapi/nf-errhandlingapi-getlasterror)返回**错误\_\_缓冲区不足**， *lpBytesReturned*为零。

如果*lpOverlapped*为**null**，则*lpBytesReturned*不能为**null**。 即使当操作不返回任何输出数据并且*lpOutBuffer*为**NULL**时， [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)使用*lpBytesReturned*。 此类操作完成后， *lpBytesReturned*的值没有意义。

如果*lpOverlapped*不为**null**，则*lpBytesReturned*可以为**null**。 如果此参数不为**NULL** ，并且操作返回数据，则在重叠操作完成之前， *lpBytesReturned*是无意义的。 若要检索返回的字节数，请调用[**getoverlappedresult 期间**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-getoverlappedresult)。 如果*hDevice*参数与 i/o 完成端口关联，则可以通过调用[**GetQueuedCompletionStatus**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-getqueuedcompletionstatus)检索返回的字节数。

<a href="" id="lpoverlapped--in-"></a> *\]中的 lpOverlapped \[*  
**LPOVERLAPPED**

指向[**重叠**](https://docs.microsoft.com/windows/desktop/api/minwinbase/ns-minwinbase-_overlapped)的结构的指针。

如果在未指定**文件\_标志**的情况下打开*hDevice*\_重叠，则将忽略*lpOverlapped* 。

如果*hDevice*是使用**文件\_标志打开的\_重叠**标志，则以重叠（异步）操作的方式执行该操作。 在这种情况下， *lpOverlapped*必须指向包含事件对象句柄的有效[**重叠**](https://docs.microsoft.com/windows/desktop/api/minwinbase/ns-minwinbase-_overlapped)结构。 否则，函数将会失败。

对于重叠操作， [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)将立即返回，并且在操作完成后会发出事件对象。 否则，在操作完成或发生错误之前，函数不会返回。

<a name="status-block"></a>状态块
------------

如果操作成功完成，则[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)将返回一个非零值。

如果操作失败或挂起，则[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)将返回零。 若要获取扩展的错误信息，请调用[**GetLastError**](https://docs.microsoft.com/windows/desktop/api/errhandlingapi/nf-errhandlingapi-getlasterror)。

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
<td align="left"><p>可从 Windows 10 开始使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs （包括 Ntifs 或 Fltkernel）</td>
</tr>
</tbody>
</table>

 

 





