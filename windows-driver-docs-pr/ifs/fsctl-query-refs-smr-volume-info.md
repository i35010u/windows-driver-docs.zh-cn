---
title: FSCTL_QUERY_REFS_SMR_VOLUME_INFO 控制代码
description: FSCTL\_查询\_REFS\_SMR\_卷\_信息控制代码将查询 Shingled 磁录制 (SMR) 卷上空间和垃圾收集活动，其当前状态。
ms.assetid: 1318CF90-2449-407E-8C9E-825E571F4CDD
keywords:
- FSCTL_QUERY_REFS_SMR_VOLUME_INFO 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_QUERY_REFS_SMR_VOLUME_INFO
api_location:
- WinIoctl.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38bee14a7e8a9c932f2a2d0ba0a4e9d212da94a2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380988"
---
# <a name="fsctlqueryrefssmrvolumeinfo-control-code"></a>FSCTL\_查询\_REFS\_SMR\_卷\_信息控制代码


**FSCTL\_查询\_REFS\_SMR\_卷\_信息**控制代码将查询 Shingled 磁录制 (SMR) 卷上的空间，其当前状态和垃圾回收活动。

若要执行此操作，调用[ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)使用以下参数的函数。

```ManagedCPlusPlus
BOOL 
DeviceIoControl( (HANDLE)       hDevice,         // handle to device
                    (DWORD)        FSCTL_QUERY_REFS_SMR_VOLUME_INFO, // dwIoControlCode
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
设备句柄。 若要获取设备句柄，请调用[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)函数。

*dwIoControlCode* \[in\]  
操作的控制代码。 使用**FSCTL\_查询\_REFS\_SMR\_卷\_信息**对于此操作。

*lpInBuffer*   
不用于此操作;设置为**NULL**。

*nInBufferSize* \[in\]  
不用于此操作;设置为零。

*lpOutBuffer* \[out\]  
指向接收缓冲区的指针[ **REFS\_SMR\_卷\_信息\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_refs_smr_volume_info_output)在空间指定的卷的当前状态的结构和垃圾回收活动。

*nOutBufferSize* \[in\]  
输出缓冲区，以字节为单位的大小。

*lpBytesReturned* \[out\]  
指向一个变量来接收数据存储在输出缓冲区，以字节为单位的大小的指针。

如果输出缓冲区太小，则调用失败， [ **GetLastError** ](https://docs.microsoft.com/windows/desktop/api/errhandlingapi/nf-errhandlingapi-getlasterror)返回**错误\_不足\_缓冲区**，和*lpBytesReturned*为零。

如果*lpOverlapped*是**NULL**， *lpBytesReturned*不能为**NULL**。 甚至当操作不返回任何输出数据和*lpOutBuffer*是**NULL**， [ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)利用*lpBytesReturned*。 此类操作的值后*lpBytesReturned*毫无意义。

如果*lpOverlapped*不是**NULL**， *lpBytesReturned*可以**NULL**。 如果此参数不是**NULL**且该操作返回的数据， *lpBytesReturned*重叠的操作未完成之前没有意义。 若要检索返回的字节数，请调用[ **GetOverlappedResult**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-getoverlappedresult)。 如果*hDevice*参数是与 I/O 完成端口相关联，可以检索通过调用返回的字节数[ **GetQueuedCompletionStatus**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-getqueuedcompletionstatus)。

*lpOverlapped* \[in\]  
一个指向[ **OVERLAPPED** ](https://docs.microsoft.com/windows/desktop/api/minwinbase/ns-minwinbase-_overlapped)结构。

如果*hDevice*而无需指定打开**文件\_标志\_OVERLAPPED**， *lpOverlapped*将被忽略。

如果*hDevice*以打开**文件\_标志\_OVERLAPPED**重叠 （异步） 操作的形式执行的标志，该操作。 在这种情况下， *lpOverlapped*必须指向有效[ **OVERLAPPED** ](https://docs.microsoft.com/windows/desktop/api/minwinbase/ns-minwinbase-_overlapped)结构，其中包含一个事件对象的句柄。 否则，该函数将失败不可预知的方式。

对于重叠操作， [ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)会立即返回，并在操作完成后，发出信号的事件对象。 否则，该函数不返回直到操作完成或发生错误。

<a name="return-value"></a>返回值
------------

如果操作成功，完成[ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)返回非零值。

如果操作失败或已挂起[ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)返回零。 若要获得扩展错误信息，请调用[ **GetLastError**](https://docs.microsoft.com/windows/desktop/api/errhandlingapi/nf-errhandlingapi-getlasterror)。

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
<td align="left"><p>从 Windows 10，版本 1709年开始可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">WinIoctl.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)

[**REFS\_SMR\_卷\_信息\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_refs_smr_volume_info_output)

[**REFS\_SMR\_卷\_GC\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ne-ntifs-_refs_smr_volume_gc_state)

 

 






