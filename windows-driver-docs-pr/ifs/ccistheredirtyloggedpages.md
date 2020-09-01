---
title: CcIsThereDirtyLoggedPages 例程
description: CcIsThereDirtyLoggedPages 例程确定卷是否包含系统缓存中有脏日志数据的任何文件。
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
ms.openlocfilehash: e33ba50c3825797a6439d74400603a5de7312abd
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065366"
---
# <a name="ccistheredirtyloggedpages-routine"></a>CcIsThereDirtyLoggedPages 例程


**CcIsThereDirtyLoggedPages**例程确定卷是否包含系统缓存中有脏日志数据的任何文件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
BOOLEAN CcIsThereDirtyLoggedPages(
  _In_     PDEVICE_OBJECT DeviceObject,
  _In_opt_ PULONG         NumberOfDirtyPages
);
```

<a name="parameters"></a>parameters
----------

*DeviceObject* \[中\]  
指向与要检查的卷关联的设备对象的指针。

*NumberOfDirtyPages* \[in，可选\]  
指向 **ULONG** 缓冲区的可选指针，该缓冲区接收与 *DeviceObject*关联的卷上的脏日志页数。

<a name="return-value"></a>返回值
------------

如果卷包含一个或多个缓存的文件，而该文件的日志数据已在缓存中被修改，但尚未刷新到磁盘，则 **CcIsThereDirtyLoggedPages** 例程返回 **TRUE** 。 否则，此例程返回 **FALSE**。

<a name="remarks"></a>备注
-------

如果存在任何脏日志页面，此例程将返回 **TRUE** 。 如果当前有任何日志页在卷上排队，它也将返回 **TRUE** 。

与 [**CcIsThereDirtyDataEx**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ccistheredirtydataex)不同， **CcIsThereDirtyLoggedPages** 例程使用文件系统设备对象查找卷缓存信息以检查是否有脏日志页面。

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
<td align="left">Ntifs (包含 Ntifs 或 FltKernel) </td>
</tr>
<tr class="even">
<td align="left"><p>库</p></td>
<td align="left">Ntoskrnl.exe</td>
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


[**CcFlushCache**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ccflushcache)

[**CcPurgeCacheSection**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ccpurgecachesection)

[**CcIsThereDirtyDataEx**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ccistheredirtydataex)

 

