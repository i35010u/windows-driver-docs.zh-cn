---
title: FSCTL_QUERY_VOLUME_NUMA_INFO 控制代码
description: FSCTL\_查询\_卷\_NUMA\_INFO 控制代码查找卷的当前非一致性内存体系结构（NUMA）节点索引。
ms.assetid: ADDA4A8C-0BF3-45F1-AFE5-956CE5D1FC01
keywords:
- FSCTL_QUERY_VOLUME_NUMA_INFO 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_QUERY_VOLUME_NUMA_INFO
api_location:
- WinIoctl.h
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95b9792b10fbf7f376a19b9fc65d5aec6f9bbbb1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841268"
---
# <a name="fsctl_query_volume_numa_info-control-code"></a>FSCTL\_查询\_卷\_NUMA\_信息控制代码


**FSCTL\_查询\_卷\_NUMA\_INFO**控制代码查找卷的当前非一致性内存体系结构（NUMA）节点索引。

若要执行此操作，请调用具有以下参数的[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)函数。

```ManagedCPlusPlus
BOOL 
   WINAPI 
   DeviceIoControl( (HANDLE)       hDevice,         
                    (DWORD)        FSCTL_QUERY_VOLUME_NUMA_INFO, // dwIoControlCode
                    (LPDWORD)      lpInBuffer,      // input buffer
                    (DWORD)        nInBufferSize,   // size of input buffer
                    (LPDWORD)      lpOutBuffer,     // output buffer
                    (DWORD)        nOutBufferSize,  // size of output buffer
                    (LPDWORD)      lpBytesReturned, // number of bytes returned
                    (LPOVERLAPPED) lpOverlapped );  // OVERLAPPED structure
```

<a name="parameters"></a>参数
----------

\] 中的*hDevice* \[  
设备的句柄。 若要获取设备句柄，请调用[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)函数。

这也可能是设备中文件或目录的句柄。 此 FSCTL 将返回包含文件或目录的卷的 NUMA 节点。

\] 中的*dwIoControlCode* \[  
操作的控制代码。 对于此操作，请使用**FSCTL\_查询\_卷\_NUMA\_信息**。

*lpInBuffer*   
不与此操作一起使用;设置为**NULL**

\] 中的*nInBufferSize* \[  
不与此操作一起使用;设置为零。

*lpOutBuffer* \[out\]  
指向缓冲区的指针，该缓冲区接收[**FSCTL\_查询\_卷\_NUMA\_INFO\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_query_volume_numa_info_output)结构，后者指定了非统一内存体系结构（NUMA）卷的当前节点。

\] 中的*nOutBufferSize* \[  
输出缓冲区的大小（以字节为单位）。

*lpBytesReturned* \[out\]  
指向一个变量的指针，该变量接收存储在输出缓冲区中的数据的大小（以字节为单位）。

如果输出缓冲区太小，则调用失败， [**GetLastError**](https://docs.microsoft.com/windows/desktop/api/errhandlingapi/nf-errhandlingapi-getlasterror)返回**错误\_\_缓冲区不足**， *lpBytesReturned*为零。

如果*lpOverlapped*为**null**，则*lpBytesReturned*不能为**null**。 即使当操作不返回任何输出数据并且*lpOutBuffer*为**NULL**时， [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)使用*lpBytesReturned*。 此类操作完成后， *lpBytesReturned*的值没有意义。

如果*lpOverlapped*不为**null**，则*lpBytesReturned*可以为**null**。 如果此参数不为**NULL** ，并且操作返回数据，则在重叠操作完成之前， *lpBytesReturned*是无意义的。 若要检索返回的字节数，请调用[**getoverlappedresult 期间**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-getoverlappedresult)。 如果*hDevice*参数与 i/o 完成端口关联，则可以通过调用[**GetQueuedCompletionStatus**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-getqueuedcompletionstatus)检索返回的字节数。

\] 中的*lpOverlapped* \[  
指向[**重叠**](https://docs.microsoft.com/windows/desktop/api/minwinbase/ns-minwinbase-_overlapped)的结构的指针。

如果在未指定**文件\_标志**的情况下打开*hDevice*\_重叠，则将忽略*lpOverlapped* 。

如果*hDevice*是使用**文件\_标志打开的\_重叠**标志，则以重叠（异步）操作的方式执行该操作。 在这种情况下， *lpOverlapped*必须指向包含事件对象句柄的有效[**重叠**](https://docs.microsoft.com/windows/desktop/api/minwinbase/ns-minwinbase-_overlapped)结构。 否则，函数将会失败。

对于重叠操作， [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)将立即返回，并且在操作完成后会发出事件对象。 否则，在操作完成或发生错误之前，函数不会返回。

<a name="return-value"></a>返回值
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
<td align="left"><p>标头</p></td>
<td align="left">WinIoctl;Ntifs</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)

[**FSCTL\_查询\_卷\_NUMA\_信息\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_query_volume_numa_info_output)

 

 






