---
title: 读取预参数
description: 预读的粒度和通过管线传输预读的预读的参数。
ms.assetid: ''
keywords:
- 预读的参数
topic_type:
- apiref
api_name:
- read_ahead_parame3ters
api_location:
- NtosKrnl.exe
api_type:
- DllExport
ms.author: eliotgra
ms.date: 09/14/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4134e79b3f135d96c791fe898cacc8d90ba0ab8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370117"
---
# <a name="readaheadparameters-structure"></a>READ_AHEAD_PARAMETERS 结构

**READ_AHEAD_PARAMETERS**结构包含公开读取预参数。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _READ_AHEAD_PARAMETERS {

    CSHORT NodeByteSize;
    ULONG Granularity;
    ULONG PipelinedRequestSize;
    ULONG ReadAheadGrowthPercentage;

} READ_AHEAD_PARAMETERS, *PREAD_AHEAD_PARAMETERS;
```

<a name="members"></a>成员
----------

*NodeByteSize* \[in\]  
以字节为单位的节点的大小。

*粒度*\[中\]  
读取 aheads 的粒度。 此值必须为 2 和大于或等于 PAGE_SIZE 偶数次幂

*PipelinedRequestSize* \[in\]  
请求大小 （字节），以执行时要使用通过管道传输预读数。 每个读请求通过管道传递分解为较小**PipelinedRequestSize**调整大小的请求。 这通常用于通过并行执行而不是单个一个大型的多个请求增加的吞吐量。

> [!NOTE]
> 由于向后兼容性，而如果该值为零，预读的每个请求将分解为两个。

*ReadAheadGrowthPercentage* \[in\]  
提前一个百分比表示的数据的已准备就绪的应用程序到目前为止读取的增长。 


<a name="remarks"></a>备注
-------

无 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left"><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">世界</a></td>
</tr>
<tr class="even">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows 8 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h （包括 Ntifs.h）</td>
</tr>
<tr class="even">
<td align="left"><p>Library</p></td>
<td align="left">NtosKrnl.lib</td>
</tr>
<tr class="odd">
<td align="left"><p>DLL</p></td>
<td align="left">NtosKrnl.exe</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**CcSetReadAheadGranularityEx**](CcSetReadAheadGranularityEx.md)

[**CcReadAhead**](https://msdn.microsoft.com/library/windows/hardware/ff539191)

[**CcScheduleReadAhead**](https://msdn.microsoft.com/library/windows/hardware/ff539200)
