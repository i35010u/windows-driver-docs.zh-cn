---
title: CcIsThereDirtyLoggedPages 例程
description: CcIsThereDirtyLoggedPages 例程确定是否某个卷不包含的文件系统缓存中的脏日志数据。
ms.assetid: B8FDD817-87E6-4D82-B668-7F1078041281
keywords:
- CcIsThereDirtyLoggedPages 例程可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- CcIsThereDirtyLoggedPages
api_location:
- NtosKrnl.exe
api_type:
- DllExport
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 745807c96a29eb281e946647eaf044054e839315
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534326"
---
# <a name="ccistheredirtyloggedpages-routine"></a>CcIsThereDirtyLoggedPages 例程


**CcIsThereDirtyLoggedPages**例程确定是否某个卷不包含的文件系统缓存中的脏日志数据。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
BOOLEAN CcIsThereDirtyLoggedPages(
  _In_     PDEVICE_OBJECT DeviceObject,
  _In_opt_ PULONG         NumberOfDirtyPages
);
```

<a name="parameters"></a>参数
----------

*DeviceObject* \[中\]  
指向与要检查的卷相关联的设备对象的指针。

*NumberOfDirtyPages* \[in, optional\]  
指向的可选指针**ULONG**该缓冲区用于接收与关联的卷上的脏日志页面数*DeviceObject*。

<a name="return-value"></a>返回值
------------

**CcIsThereDirtyLoggedPages**例程返回**TRUE**如果卷中包含一个或多个缓存的文件已在缓存中，修改但尚未刷新到磁盘的日志数据。 否则，此例程将返回**FALSE**。

<a name="remarks"></a>备注
-------

此例程将返回 **，则返回 TRUE**如果所有脏日志页存在。 它还将返回 **，则返回 TRUE**是否存在任何日志页当前排队到卷。

与不同[ **CcIsThereDirtyDataEx**](https://msdn.microsoft.com/library/windows/hardware/ff539152)，则**CcIsThereDirtyLoggedPages**例程使用文件系统设备对象以找到要检查更新的卷缓存信息登录页。

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
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows 8 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs.h （包括 Ntifs.h 或 FltKernel.h）</td>
</tr>
<tr class="even">
<td align="left"><p>Library</p></td>
<td align="left">NtosKrnl.lib</td>
</tr>
<tr class="odd">
<td align="left"><p>DLL</p></td>
<td align="left">NtosKrnl.exe</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**CcFlushCache**](https://msdn.microsoft.com/library/windows/hardware/ff539082)

[**CcPurgeCacheSection**](https://msdn.microsoft.com/library/windows/hardware/ff539188)

[**CcIsThereDirtyDataEx**](https://msdn.microsoft.com/library/windows/hardware/ff539152)

 

 






