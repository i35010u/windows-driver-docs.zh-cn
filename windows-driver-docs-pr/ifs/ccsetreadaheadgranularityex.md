---
title: CcSetReadAheadGranularityEx 例程
description: CcSetReadAheadGranularityEx 例程设置预读的粒度，并使管道的预读缓存文件。
ms.assetid: D70C3397-CF37-46E5-BA84-819BC984665A
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
ms.openlocfilehash: 4592e8296fa9e5382ec7752f8eee75099ff57f85
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364352"
---
# <a name="ccsetreadaheadgranularityex-routine"></a>CcSetReadAheadGranularityEx 例程


**CcSetReadAheadGranularityEx**例程设置预读的粒度，并使管道的预读缓存文件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID CcSetReadAheadGranularityEx(
  _In_ PFILE_OBJECT FileObject,
  _In_ PREAD_AHEAD_PARAMETERS    ReadAheadParameters
);
```

<a name="parameters"></a>Parameters
----------

*FileObject* \[in\]  
指向文件对象的已缓存的文件的预读的粒度是设置。

*ReadAheadParameters* \[in\]  
指定读取预参数。 请参阅[READ_AHEAD_PARAMETERS](read-ahead-parameters.md)有关详细信息。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

调用**CcSetReadAheadGranularityEx**将启用通过管线传输中的文件对象的预读请求*的文件对象*。 选择适当的值*PipelinedRequestSize*将除预读请求集成到较小的多个并行请求。 调用方**CcSetReadAheadGranularityEx**可以通过调整优化预读性能*PipelinedRequestSize*。

之后[ **CcInitializeCacheMap** ](https://msdn.microsoft.com/library/windows/hardware/ff539135)之前缓存文件，名为**CcSetReadAheadGranularityEx**称为缓存的文件，默认的预读粒度有关缓存的文件是否等于页\_大小。

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


[**CcInitializeCacheMap**](https://msdn.microsoft.com/library/windows/hardware/ff539135)

[**CcReadAhead**](https://docs.microsoft.com/previous-versions/ff539191(v=vs.85))

[**CcScheduleReadAhead**](https://msdn.microsoft.com/library/windows/hardware/ff539200)

[**CcSetAdditionalCacheAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff539203)

 

 






