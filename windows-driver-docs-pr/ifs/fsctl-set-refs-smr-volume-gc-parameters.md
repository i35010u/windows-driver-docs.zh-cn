---
title: FSCTL_SET_REFS_SMR_VOLUME_GC_PARAMETERS 控制代码
description: FSCTL \_ SET \_ REFS \_ SMR \_ VOLUME \_ GC \_ PARAMETERS 控制代码控制对 Shingled 磁性记录 (SMR) 卷的垃圾回收。
keywords:
- FSCTL_SET_REFS_SMR_VOLUME_GC_PARAMETERS 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_SET_REFS_SMR_VOLUME_GC_PARAMETERS
api_location:
- WinIoctl.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: af82408fb24ec00bb9e29bf303bf6494ea2c4abb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838039"
---
# <a name="fsctl_set_refs_smr_volume_gc_parameters-control-code"></a>FSCTL \_ 设置 \_ REFS \_ SMR \_ VOLUME \_ GC \_ PARAMETERS 控制代码


**FSCTL \_ SET \_ REFS \_ SMR \_ VOLUME \_ GC \_ PARAMETERS** 控制代码控制对 Shingled 磁性记录 (SMR) 卷的垃圾回收。

```ManagedCPlusPlus
BOOL
   DeviceIoControl( (HANDLE)       hDevice,         // handle to volume
                    FSCTL_SET_REFS_SMR_VOLUME_GC_PARAMETERS, // dwIoControlCode
                    (LPDWORD)      lpInBuffer,      // input buffer
                    (DWORD)        nInBufferSize,   // size of input buffer
                     NULL,     // output buffer
                     0,  // size of output buffer
                    (LPDWORD)      lpBytesReturned, // number of bytes returned
                    (LPOVERLAPPED) lpOverlapped );  // OVERLAPPED structure
```

<a name="parameters"></a>参数
----------

*hDevice* \[中\]  
设备的句柄。 若要获取设备句柄，请调用 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea) 函数。

*dwIoControlCode* \[中\]  
操作的控制代码。 对于此操作，请使用 **FSCTL \_ SET \_ REFS \_ SMR \_ VOLUME \_ GC \_ PARAMETERS** 。

*lpInBuffer*   
一个指针，指向分配给调用方的 [**REFS 的 \_ \_ 卷 \_ GC \_ 参数**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_refs_smr_volume_gc_parameters) 结构。

*nInBufferSize* \[中\]  
输入缓冲区的大小（以字节为单位）。

*lpOutBuffer* \[弄\]  
不与此操作一起使用;设置为 **NULL**。

*nOutBufferSize* \[中\]  
不与此操作一起使用;设置为零。

*lpBytesReturned* \[弄\]  
不与此操作一起使用;设置为 **NULL**。

*lpOverlapped* \[中\]  
指向 [**重叠**](/windows/win32/api/minwinbase/ns-minwinbase-overlapped) 的结构的指针。

如果在未指定 **文件 \_ 标志 \_ 重叠** 的情况下打开 *hDevice* ，则将忽略 *lpOverlapped* 。

如果使用 **FILE \_ 标记 \_ 交叠** 标志打开 *hDevice* ，则操作将作为 (异步) 操作的重叠进行。 在这种情况下， *lpOverlapped* 必须指向包含事件对象句柄的有效 [**重叠**](/windows/win32/api/minwinbase/ns-minwinbase-overlapped) 结构。 否则，函数将会失败。

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

## <a name="see-also"></a>请参阅


[**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol)

 

