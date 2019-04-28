---
title: FSCTL_DUPLICATE_EXTENTS_TO_FILE_EX 控制代码
description: FSCTL\_重复\_区\_TO\_文件\_EX 控件代码指示要复制的文件字节范围代表应用程序的文件系统。 目标文件可能是相同或不同源文件中。
ms.assetid: B13C6415-5593-43CF-90AC-7D2DC844EC41
keywords:
- FSCTL_DUPLICATE_EXTENTS_TO_FILE_EX 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_DUPLICATE_EXTENTS_TO_FILE_EX
api_location:
- WinIoctl.h
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c78c9f36a52c3c930761324c8667464c13d7fb53
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327889"
---
# <a name="fsctlduplicateextentstofileex-control-code"></a>FSCTL\_重复\_区\_TO\_文件\_EX 控制代码


[ **FSCTL\_重复\_扩展盘区\_TO\_文件\_EX** ](fsctl-duplicate-extents-to-file-ex.md)控制代码指示文件系统复制的文件范围代表应用程序的字节数。 目标文件可能是相同或不同源文件中。

若要执行此操作，调用[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)使用以下参数的函数。

```ManagedCPlusPlus
BOOL 
   WINAPI 
   DeviceIoControl( (HANDLE)       hDevice,         // handle to device
                    (DWORD)        FSCTL_DUPLICATE_EXTENTS_TO_FILE_EX, // dwIoControlCode
                    (LPDWORD)      lpInBuffer,      // input buffer
                    (DWORD)        nInBufferSize,   // size of input buffer
                    (LPDWORD)      lpOutBuffer,     // output buffer
                    (DWORD)        nOutBufferSize,  // size of output buffer
                    (LPDWORD)      lpBytesReturned, // number of bytes returned
                    (LPOVERLAPPED) lpOverlapped );  // OVERLAPPED structure
```

<a name="parameters"></a>Parameters
----------

*hDevice* \[in\]  
设备句柄。 若要获取设备句柄，请调用[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)函数。

*dwIoControlCode* \[in\]  
操作的控制代码。 使用[ **FSCTL\_重复\_扩展盘区\_TO\_文件\_EX** ](fsctl-duplicate-extents-to-file-ex.md)对于此操作。

*lpInBuffer*   
一个指向**重复\_区\_数据\_EX**结构，它指定的源文件、 源字节范围和目标文件复制到的范围偏移量。

*nInBufferSize* \[in\]  
输入缓冲区，以字节为单位的大小。

*lpOutBuffer* \[out\]  
不使用与此操作。 设置为 NULL。

*nOutBufferSize* \[in\]  
不使用与此操作。 设置为零 (0)。

*lpBytesReturned* \[out\]  
指向一个变量来接收数据存储在输出缓冲区，以字节为单位的大小的指针。

如果输出缓冲区太小，则调用失败， [ **GetLastError** ](https://msdn.microsoft.com/library/windows/desktop/ms679360)返回**错误\_不足\_缓冲区**，和*lpBytesReturned*为零。

如果*lpOverlapped*是**NULL**， *lpBytesReturned*不能为**NULL**。 甚至当操作不返回任何输出数据和*lpOutBuffer*是**NULL**， [ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)利用*lpBytesReturned*。 此类操作的值后*lpBytesReturned*毫无意义。

如果*lpOverlapped*不是**NULL**， *lpBytesReturned*可以**NULL**。 如果此参数不是**NULL**且该操作返回的数据， *lpBytesReturned*重叠的操作未完成之前没有意义。 若要检索返回的字节数，请调用[ **GetOverlappedResult**](https://msdn.microsoft.com/library/windows/desktop/ms683209)。 如果*hDevice*参数是与 I/O 完成端口相关联，可以检索通过调用返回的字节数[ **GetQueuedCompletionStatus**](https://msdn.microsoft.com/library/windows/desktop/aa364986)。

*lpOverlapped* \[in\]  
一个指向[ **OVERLAPPED** ](https://msdn.microsoft.com/library/windows/desktop/ms684342)结构。

如果*hDevice*而无需指定打开**文件\_标志\_OVERLAPPED**， *lpOverlapped*将被忽略。

如果*hDevice*以打开**文件\_标志\_OVERLAPPED**重叠 （异步） 操作的形式执行的标志，该操作。 在这种情况下， *lpOverlapped*必须指向有效[ **OVERLAPPED** ](https://msdn.microsoft.com/library/windows/desktop/ms684342)结构，其中包含一个事件对象的句柄。 否则，该函数将失败不可预知的方式。

对于重叠操作， [ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)会立即返回，并在操作完成后，发出信号的事件对象。 否则，该函数不返回直到操作完成或发生错误。

<a name="return-value"></a>返回值
------------

如果操作成功，完成[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)返回非零值。

如果操作失败或已挂起[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)返回零。 若要获得扩展错误信息，请调用[ **GetLastError**](https://msdn.microsoft.com/library/windows/desktop/ms679360)。

<a name="remarks"></a>备注
-------

在此操作的 I/O 重叠的含义，请参阅备注部分[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)主题。

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
<td align="left">WinIoctl.h; Ntifs.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DeviceIoControl**](https://msdn.microsoft.com/library/windows/desktop/aa363216)

 






