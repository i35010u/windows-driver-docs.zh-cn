---
title: FSCTL_SET_REFS_SMR_VOLUME_GC_PARAMETERS 控制代码
description: FSCTL\_将\_REFS\_SMR\_卷\_GC\_参数控制代码控制 Shingled 磁性记录（SMR）卷上的垃圾回收。
ms.assetid: 782542C4-CFC5-4BF7-AF38-3247A3AC6AB9
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
ms.openlocfilehash: 7931a45815cf4ce94eae34e7ceb52252e793675d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841249"
---
# <a name="fsctl_set_refs_smr_volume_gc_parameters-control-code"></a>FSCTL\_设置\_REFS\_SMR\_卷\_GC\_参数控制代码


**FSCTL\_将\_REFS\_SMR\_卷\_GC\_参数**控制代码控制 Shingled 磁性记录（SMR）卷上的垃圾回收。

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

\] 中的*hDevice* \[  
设备的句柄。 若要获取设备句柄，请调用[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)函数。

\] 中的*dwIoControlCode* \[  
操作的控制代码。 使用**FSCTL\_设置\_REFS\_SMR\_卷\_GC\_** 用于此操作的参数。

*lpInBuffer*   
指向分配给调用方的引用的指针， [ **\_SMR\_VOLUME\_GC\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_refs_smr_volume_gc_parameters)结构。

\] 中的*nInBufferSize* \[  
输入缓冲区的大小（以字节为单位）。

*lpOutBuffer* \[out\]  
不与此操作一起使用;设置为**NULL**。

\] 中的*nOutBufferSize* \[  
不与此操作一起使用;设置为零。

*lpBytesReturned* \[out\]  
不与此操作一起使用;设置为**NULL**。

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


[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)

 

 






