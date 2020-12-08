---
title: CcSetReadAheadGranularityEx 例程
description: CcSetReadAheadGranularityEx 例程设置预读的粒度，并为缓存的文件启用管道预读。
keywords:
- CcSetReadAheadGranularityEx 例程可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- CcSetReadAheadGranularityEx
api_location:
- NtosKrnl.exe
api_type:
- DllExport
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f644d50525a626d9baf2ede4d8e061a47fdc1f65
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786851"
---
# <a name="ccsetreadaheadgranularityex-routine"></a>CcSetReadAheadGranularityEx 例程


**CcSetReadAheadGranularityEx** 例程设置预读的粒度，并为缓存的文件启用管道预读。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID CcSetReadAheadGranularityEx(
  _In_ PFILE_OBJECT FileObject,
  _In_ PREAD_AHEAD_PARAMETERS    ReadAheadParameters
);
```

<a name="parameters"></a>参数
----------

*FileObject* \[中\]  
一个指针，指向要设置其预读粒度的缓存文件的文件对象。

*ReadAheadParameters* \[中\]  
指定预读参数。 有关详细信息，请参阅 [READ_AHEAD_PARAMETERS](read-ahead-parameters.md) 。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

调用 **CcSetReadAheadGranularityEx** 将为 *FileObject* 中的文件对象启用管道预读请求。 为 *PipelinedRequestSize* 选择适当的值会将预读请求拆分为较小的多个并行请求。 **CcSetReadAheadGranularityEx** 的调用方可以通过调整 *PipelinedRequestSize* 来优化预读性能。

在调用 [**CcInitializeCacheMap**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ccinitializecachemap) 来缓存文件后，但在为缓存文件调用 **CcSetReadAheadGranularityEx** 之前，缓存文件的默认预读粒度等于页面 \_ 大小。

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

## <a name="see-also"></a>请参阅


[**CcInitializeCacheMap**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ccinitializecachemap)

[**CcReadAhead**](/previous-versions/ff539191(v=vs.85))

[**CcScheduleReadAhead**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ccschedulereadahead)

[**CcSetAdditionalCacheAttributes**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ccsetadditionalcacheattributes)

 

