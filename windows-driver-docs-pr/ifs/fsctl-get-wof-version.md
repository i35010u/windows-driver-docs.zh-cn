---
title: FSCTL_GET_WOF_VERSION 控制代码
description: FSCTL\_获取\_WOF\_版本 I/O 控制代码 (IOCTL) 用于查询的使用以支持特定的提供程序的驱动程序版本。
ms.assetid: 0E3C3C7E-2A89-4CA8-8741-7C057E063155
keywords:
- FSCTL_GET_WOF_VERSION 控制代码可安装文件系统驱动程序
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
ms.openlocfilehash: 73dc3150b48ed350168e619a99e52ffa8f28f08f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324608"
---
# <a name="fsctlgetwofversion-control-code"></a>FSCTL\_获取\_WOF\_版本控制代码


**FSCTL\_获取\_WOF\_版本**I/O 控制代码 (IOCTL) 用于查询的使用以支持特定的提供程序的驱动程序版本。

若要执行此操作，调用[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)使用以下参数。

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

<a href="" id="hdevice--in-"></a>*hDevice \[in\]*  
设备句柄。 若要获取设备句柄，请调用[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)函数或类似的 API。

<a href="" id="dwiocontrolcode--in-"></a>*dwIoControlCode \[in\]*  
操作的控制代码。 使用**FSCTL\_获取\_WOF\_版本**对于此操作。

<a href="" id="lpinbuffer"></a>*lpInBuffer*  
该操作的的输入的缓冲区。 这是一个指向[ **WOF\_外部\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn632452)结构。

<a href="" id="ninbuffersize--in-"></a>*nInBufferSize \[in\]*  
以字节为单位，输入缓冲区的大小。 这应该是**sizeof**([**WOF\_外部\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn632452))。

<a href="" id="lpoutbuffer--out-"></a>*lpOutBuffer \[out\]*  
该操作的的输出缓冲区。 这是一个指向[ **WOF\_版本\_信息**](https://msdn.microsoft.com/library/windows/hardware/mt426742)结构。

<a href="" id="noutbuffersize--in-"></a>*nOutBufferSize \[in\]*  
以字节为单位，输出缓冲区的大小。 这应该是**sizeof**([**WOF\_版本\_信息**](https://msdn.microsoft.com/library/windows/hardware/mt426742))。

<a href="" id="lpbytesreturned--out-"></a>*lpBytesReturned\[出\]*  
**LPDWORD**

指向一个变量来接收数据存储在输出缓冲区，以字节为单位的大小的指针。

如果输出缓冲区太小，则调用失败， [ **GetLastError** ](https://msdn.microsoft.com/library/windows/desktop/ms679360)返回**错误\_不足\_缓冲区**，和*lpBytesReturned*为零。

如果*lpOverlapped*是**NULL**， *lpBytesReturned*不能为**NULL**。 甚至当操作不返回任何输出数据和*lpOutBuffer*是**NULL**， [ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)利用*lpBytesReturned*。 此类操作的值后*lpBytesReturned*毫无意义。

如果*lpOverlapped*不是**NULL**， *lpBytesReturned*可以**NULL**。 如果此参数不是**NULL**且该操作返回的数据， *lpBytesReturned*重叠的操作未完成之前没有意义。 若要检索返回的字节数，请调用[ **GetOverlappedResult**](https://msdn.microsoft.com/library/windows/desktop/ms683209)。 如果*hDevice*参数是与 I/O 完成端口相关联，可以检索通过调用返回的字节数[ **GetQueuedCompletionStatus**](https://msdn.microsoft.com/library/windows/desktop/aa364986)。

<a href="" id="lpoverlapped--in-"></a>*lpOverlapped \[in\]*  
**LPOVERLAPPED**

一个指向[ **OVERLAPPED** ](https://msdn.microsoft.com/library/windows/desktop/ms684342)结构。

如果*hDevice*而无需指定打开**文件\_标志\_OVERLAPPED**， *lpOverlapped*将被忽略。

如果*hDevice*以打开**文件\_标志\_OVERLAPPED**重叠 （异步） 操作的形式执行的标志，该操作。 在这种情况下， *lpOverlapped*必须指向有效[ **OVERLAPPED** ](https://msdn.microsoft.com/library/windows/desktop/ms684342)结构，其中包含一个事件对象的句柄。 否则，该函数将失败不可预知的方式。

对于重叠操作， [ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)会立即返回，并在操作完成后，发出信号的事件对象。 否则，该函数不返回直到操作完成或发生错误。

<a name="status-block"></a>状态块
------------

如果操作成功，完成[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)返回非零值。

如果操作失败或已挂起[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)返回零。 若要获得扩展错误信息，请调用[ **GetLastError**](https://msdn.microsoft.com/library/windows/desktop/ms679360)。

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
<td align="left"><p>从 Windows 10 开始可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h （包括 Ntifs.h 或 Fltkernel.h）</td>
</tr>
</tbody>
</table>

 

 





