---
title: FSCTL_QUERY_REFS_SMR_VOLUME_INFO 控制代码
description: FSCTL \_ 查询 \_ REFS \_ SMR \_ 卷 \_ INFO 控制代码查询 SHINGLED 磁性记录， (SMR) 卷的当前状态和垃圾回收活动。
ms.assetid: 1318CF90-2449-407E-8C9E-825E571F4CDD
keywords:
- FSCTL_QUERY_REFS_SMR_VOLUME_INFO 控制代码可安装的文件系统驱动程序
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
ms.openlocfilehash: 500d36d05d4d81fa4223c7b6549e6d9229d7f8ba
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91423795"
---
# <a name="fsctl_query_refs_smr_volume_info-control-code"></a>FSCTL \_ 查询 \_ REFS \_ SMR \_ 卷 \_ 信息控制代码


**FSCTL \_ 查询 \_ REFS \_ SMR \_ 卷 \_ INFO**控制代码查询 Shingled 磁性记录， (SMR) 卷的当前状态和垃圾回收活动。

若要执行此操作，请调用具有以下参数的 [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) 函数。

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

<a name="parameters"></a>parameters
----------

*hDevice* \[中\]  
设备的句柄。 若要获取设备句柄，请调用 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea) 函数。

*dwIoControlCode* \[中\]  
操作的控制代码。 对于此操作，请使用 **FSCTL \_ 查询 \_ REFS \_ SMR \_ VOLUME \_ INFO** 。

*lpInBuffer*   
不与此操作一起使用;设置为 **NULL**。

*nInBufferSize* \[中\]  
不与此操作一起使用;设置为零。

*lpOutBuffer* \[弄\]  
指向缓冲区的指针，该缓冲区接收 REFS，其中指定卷在空间和垃圾回收活动中的当前状态。 [** \_ \_ \_ \_ **](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_refs_smr_volume_info_output)

*nOutBufferSize* \[中\]  
输出缓冲区的大小（以字节为单位）。

*lpBytesReturned* \[弄\]  
指向一个变量的指针，该变量接收存储在输出缓冲区中的数据的大小（以字节为单位）。

如果输出缓冲区太小，则调用失败， [**GetLastError**](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror) 返回 **错误 \_ \_ 缓冲区**，并且 *lpBytesReturned* 为零。

如果 *lpOverlapped* 为 **null**，则 *lpBytesReturned* 不能为 **null**。 即使当操作不返回任何输出数据并且 *lpOutBuffer* 为 **NULL**时， [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) 使用 *lpBytesReturned*。 此类操作完成后， *lpBytesReturned* 的值没有意义。

如果 *lpOverlapped* 不为 **null**，则 *lpBytesReturned* 可以为 **null**。 如果此参数不为 **NULL** ，并且操作返回数据，则在重叠操作完成之前， *lpBytesReturned* 是无意义的。 若要检索返回的字节数，请调用 [**getoverlappedresult 期间**](/windows/win32/api/ioapiset/nf-ioapiset-getoverlappedresult)。 如果 *hDevice* 参数与 i/o 完成端口关联，则可以通过调用 [**GetQueuedCompletionStatus**](/windows/win32/api/ioapiset/nf-ioapiset-getqueuedcompletionstatus)检索返回的字节数。

*lpOverlapped* \[中\]  
指向 [**重叠**](/windows/win32/api/minwinbase/ns-minwinbase-overlapped) 的结构的指针。

如果在未指定**文件 \_ 标志 \_ 重叠**的情况下打开*hDevice* ，则将忽略*lpOverlapped* 。

如果使用**FILE \_ 标记 \_ 交叠**标志打开*hDevice* ，则操作将作为 (异步) 操作的重叠进行。 在这种情况下， *lpOverlapped* 必须指向包含事件对象句柄的有效 [**重叠**](/windows/win32/api/minwinbase/ns-minwinbase-overlapped) 结构。 否则，函数将会失败。

对于重叠操作， [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) 将立即返回，并且在操作完成后会发出事件对象。 否则，在操作完成或发生错误之前，函数不会返回。

<a name="return-value"></a>返回值
------------

如果操作成功完成，则 [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) 将返回一个非零值。

如果操作失败或挂起，则 [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) 将返回零。 若要获取扩展的错误信息，请调用 [**GetLastError**](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror)。

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
<td align="left"><p>从 Windows 10 版本1709开始可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">WinIoctl</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol)

[**REFS \_ SMR \_ 卷 \_ 信息 \_ 输出**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_refs_smr_volume_info_output)

[**REFS \_ SMR \_ 卷 \_ GC \_ 状态**](/windows-hardware/drivers/ddi/ntifs/ne-ntifs-_refs_smr_volume_gc_state)

 

