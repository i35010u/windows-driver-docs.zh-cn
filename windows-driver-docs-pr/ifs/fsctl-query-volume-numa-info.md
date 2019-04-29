---
title: FSCTL_QUERY_VOLUME_NUMA_INFO 控制代码
description: FSCTL\_查询\_卷\_NUMA\_信息控制代码查找当前的非统一内存体系结构 (NUMA) 节点索引的卷。
ms.assetid: ADDA4A8C-0BF3-45F1-AFE5-956CE5D1FC01
keywords:
- FSCTL_QUERY_VOLUME_NUMA_INFO 控制代码可安装文件系统驱动程序
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
ms.openlocfilehash: e7ea4fbfe4ce37d4d16c82416d99e80677f83b2a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391773"
---
# <a name="fsctlqueryvolumenumainfo-control-code"></a>FSCTL\_查询\_卷\_NUMA\_信息控制代码


**FSCTL\_查询\_卷\_NUMA\_信息**控件的代码查找当前的非统一内存体系结构 (NUMA) 节点索引的卷。

若要执行此操作，调用[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)使用以下参数的函数。

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

<a name="parameters"></a>Parameters
----------

*hDevice* \[in\]  
设备句柄。 若要获取设备句柄，请调用[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)函数。

这也可以是文件或目录以及在设备中的句柄。 此 FSCTL 将返回包含文件或目录的卷的 NUMA 节点。

*dwIoControlCode* \[in\]  
操作的控制代码。 使用**FSCTL\_查询\_卷\_NUMA\_信息**对于此操作。

*lpInBuffer*   
不用于此操作;设置为**NULL**

*nInBufferSize* \[in\]  
不用于此操作;设置为零。

*lpOutBuffer* \[out\]  
指向接收缓冲区的指针[ **FSCTL\_查询\_卷\_NUMA\_信息\_输出**](https://msdn.microsoft.com/library/windows/hardware/mt827087)结构，它指定在无将统一内存体系结构 (NUMA) 卷的当前节点。

*nOutBufferSize* \[in\]  
输出缓冲区，以字节为单位的大小。

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

[**FSCTL\_查询\_卷\_NUMA\_信息\_输出**](https://msdn.microsoft.com/library/windows/hardware/mt827087)

 

 






