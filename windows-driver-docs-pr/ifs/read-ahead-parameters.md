---
title: 预读参数
description: 预读粒度和管线预读参数。
ms.assetid: ''
keywords:
- 预读参数
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
ms.openlocfilehash: e909d6a84af48f41caa21016a3b651a05029e57e
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067370"
---
# <a name="read_ahead_parameters-structure"></a>READ_AHEAD_PARAMETERS 结构

**READ_AHEAD_PARAMETERS**结构包含公开读取的预读参数。

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

*NodeByteSize* \[中\]  
节点的大小（以字节为单位）。

*粒度* \[中\]  
读取 aheads 的粒度。 此值必须是2的甚至大于或等于 PAGE_SIZE

*PipelinedRequestSize* \[中\]  
要在执行管道 aheads 时使用的请求大小（以字节为单位）。 管道中的每个预读请求会划分为较小的 **PipelinedRequestSize** 大小的请求。 这通常用于通过并行化多个 requets （而不是一个大）来增加吞吐量。

> [!NOTE]
> 由于向后兼容性，如果此值为零，则每个预读请求都将分为两个。

*ReadAheadGrowthPercentage* \[中\]  
从目前为止，应用程序已准备就绪的数据百分比的增长。 


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
<td align="left"><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">通用</a></td>
</tr>
<tr class="even">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 windows 8 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs (包含 Ntifs) </td>
</tr>
<tr class="even">
<td align="left"><p>库</p></td>
<td align="left">Ntoskrnl.exe</td>
</tr>
<tr class="odd">
<td align="left"><p>DLL</p></td>
<td align="left">NtosKrnl.exe</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**CcSetReadAheadGranularityEx**](CcSetReadAheadGranularityEx.md)

[**CcReadAhead**](/previous-versions/ff539191(v=vs.85))

[**CcScheduleReadAhead**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ccschedulereadahead)