---
title: 设备\_数据\_管理\_设置\_操作
description: 设备\_数据\_管理\_设置\_操作常量指定执行的设备的数据集属性上的驱动程序的管理操作的类型。
ms.assetid: cc64c7ad-7d1c-45c7-b236-a43e57086f8d
topic_type:
- apiref
api_name:
- DeviceDsmAction_None
- DeviceDsmAction_Trim
- DeviceDsmAction_Notification
- DeviceDsmAction_OffloadRead
- DeviceDsmAction_OffloadWrite
- DeviceDsmAction_Allocation
- DeviceDsmAction_Repair
- DeviceDsmAction_Scrub
- DeviceDsmAction_DrtQuery
- DeviceDsmAction_DrtClear
- DeviceDsmAction_DrtDisable
- DeviceDsmAction_NvCache_Change_Priority
- DeviceDsmAction_NvCache_Evict
api_location:
- ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: aee94d1032653ec6c8846556dcb0762d69c30db5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519284"
---
# <a name="devicedatamanagementsetaction"></a>设备\_数据\_管理\_设置\_操作


一个**设备\_数据\_管理\_设置\_操作**常量指定执行的设备的数据集属性上的驱动程序的管理操作的类型。

中指定的管理操作[**设备\_管理\_数据\_设置\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552527)的系统缓冲区中包含的结构[ **IOCTL\_存储\_管理\_数据\_设置\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff560573)请求。

<span id="DeviceDsmAction_None"></span><span id="devicedsmaction_none"></span><span id="DEVICEDSMACTION_NONE"></span>**DeviceDsmAction\_None**结构初始化为 0 仅目的。

<span id="DeviceDsmAction_Trim"></span><span id="devicedsmaction_trim"></span><span id="DEVICEDSMACTION_TRIM"></span>**DeviceDsmAction\_剪裁**1 驱动程序将执行剪裁操作。

<span id="DeviceDsmAction_Notification"></span><span id="devicedsmaction_notification"></span><span id="DEVICEDSMACTION_NOTIFICATION"></span>**DeviceDsmAction\_通知**(2 |DeviceDsmActionFlag\_非破坏性) 驱动程序将执行一个通知操作。

对于此操作， **ParameterBlockOffset**并**ParameterBlockLength**的成员[**设备\_管理\_数据\_设置\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff552527)结构指定通知操作的参数。 这些参数的格式为[**设备\_DSM\_通知\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff819207)结构。

&gt; \[!请注意\] &gt; Windows 7 和更高版本的 Windows 中受支持。

 

<span id="DeviceDsmAction_OffloadRead"></span><span id="devicedsmaction_offloadread"></span><span id="DEVICEDSMACTION_OFFLOADREAD"></span>**DeviceDsmAction\_OffloadRead** (3 |DeviceDsmActionFlag\_非破坏性) 驱动程序执行读取操作卸载。

对于此操作， **ParameterBlockOffset**并**ParameterBlockLength**的成员[**设备\_管理\_数据\_设置\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff552527)结构指定的卸载参数读取操作。 这些参数的格式为[**设备\_DSM\_卸载\_读取\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh439639)结构。

&gt; \[!请注意\] &gt; Windows 8 和更高版本的 Windows 中受支持。

 

<span id="DeviceDsmAction_OffloadWrite"></span><span id="devicedsmaction_offloadwrite"></span><span id="DEVICEDSMACTION_OFFLOADWRITE"></span>**DeviceDsmAction\_OffloadWrite** 4 驱动程序将执行卸载写入操作。

对于此操作， **ParameterBlockOffset**并**ParameterBlockLength**的成员[**设备\_管理\_数据\_设置\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff552527)结构指定的卸载参数写入操作。 这些参数的格式为[**设备\_DSM\_卸载\_编写\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh439644)结构。

&gt; \[!请注意\] &gt; Windows 8 和更高版本的 Windows 中受支持。

 

<span id="DeviceDsmAction_Allocation"></span><span id="devicedsmaction_allocation"></span><span id="DEVICEDSMACTION_ALLOCATION"></span>**DeviceDsmAction\_分配**(5 |DeviceDsmActionFlag\_非破坏性) 驱动程序将执行预配操作一个逻辑块。

逻辑块范围指定在单个[**设备\_数据\_设置\_范围**](https://msdn.microsoft.com/library/windows/hardware/ff552523)结构。

&gt; \[!请注意\] &gt; Windows 8 和更高版本的 Windows 中受支持。

 

<span id="DeviceDsmAction_Repair"></span><span id="devicedsmaction_repair"></span><span id="DEVICEDSMACTION_REPAIR"></span>**DeviceDsmAction\_修复**(6 |DeviceDsmActionFlag\_非破坏性) 驱动程序将执行存储空间修复操作。

逻辑块范围指定在单个[**设备\_数据\_设置\_范围**](https://msdn.microsoft.com/library/windows/hardware/ff552523)结构。 中指定的修复副本数**设备\_数据\_设置\_修复\_参数**结构位于指定的输入缓冲区中**ParameterBlockOffset**的成员[**设备\_管理\_数据\_设置\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552527)结构。

&gt; \[!请注意\] &gt; Windows 8 和更高版本的 Windows 中受支持。

 

<span id="DeviceDsmAction_Scrub"></span><span id="devicedsmaction_scrub"></span><span id="DEVICEDSMACTION_SCRUB"></span>**DeviceDsmAction\_清理**(7 |DeviceDsmActionFlag\_非破坏性) 驱动程序将执行存储空间清理操作。

逻辑块范围指定在单个[**设备\_数据\_设置\_范围**](https://msdn.microsoft.com/library/windows/hardware/ff552523)结构。

&gt; \[!请注意\] &gt; Windows 8 和更高版本的 Windows 中受支持。

 

<span id="DeviceDsmAction_DrtQuery"></span><span id="devicedsmaction_drtquery"></span><span id="DEVICEDSMACTION_DRTQUERY"></span>**DeviceDsmAction\_DrtQuery** (8 |DeviceDsmActionFlag\_非破坏性) 驱动程序将执行查询指定的逻辑块范围和检查如果包含在存储空间脏区域跟踪。 中返回该范围的同步状态**OperationStatus**的成员[**设备\_管理\_数据\_设置\_属性\_输出**](https://msdn.microsoft.com/library/windows/hardware/hh439656)结构。

指定逻辑块范围，则在输入时，在单个[**设备\_数据\_设置\_范围**](https://msdn.microsoft.com/library/windows/hardware/ff552523)结构。

&gt; \[!请注意\] &gt; Windows 8 和更高版本的 Windows 中受支持。

 

<span id="DeviceDsmAction_DrtClear"></span><span id="devicedsmaction_drtclear"></span><span id="DEVICEDSMACTION_DRTCLEAR"></span>**DeviceDsmAction\_DrtClear** (9 |DeviceDsmActionFlag\_非破坏性) 驱动程序将清除脏范围状态的指定逻辑块范围内。

逻辑块范围指定在单个[**设备\_数据\_设置\_范围**](https://msdn.microsoft.com/library/windows/hardware/ff552523)结构。

&gt; \[!请注意\] &gt; Windows 8 和更高版本的 Windows 中受支持。

 

<span id="DeviceDsmAction_DrtDisable"></span><span id="devicedsmaction_drtdisable"></span><span id="DEVICEDSMACTION_DRTDISABLE"></span>**DeviceDsmAction\_DrtDisable** (10 |DeviceDsmActionFlag\_非破坏性) 驱动程序将禁用脏区域跟踪指定的逻辑块范围。

逻辑块范围指定在单个[**设备\_数据\_设置\_范围**](https://msdn.microsoft.com/library/windows/hardware/ff552523)结构。

&gt; \[!请注意\] &gt; Windows 8 和更高版本的 Windows 中受支持。

 

<span id="DeviceDsmAction_NvCache_Change_Priority"></span><span id="devicedsmaction_nvcache_change_priority"></span><span id="DEVICEDSMACTION_NVCACHE_CHANGE_PRIORITY"></span>**DeviceDsmAction\_NvCache\_更改\_优先级**(14 |DeviceDsmActionFlag\_非破坏性) 驱动程序将更改指定范围的逻辑块的缓存优先级。

在中设置新的目标优先级**设备\_DSM\_NVCACHE\_更改\_优先级\_参数**结构位于**ParameterBlockOffset**中[**设备\_管理\_数据\_设置\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552527)。 要更改的优先级的逻辑块范围给出了一个或多个[**设备\_数据\_设置\_范围**](https://msdn.microsoft.com/library/windows/hardware/ff552523)结构。

**设备\_DSM\_NVCACHE\_更改\_优先级\_参数**中定义*ntddstor.h*并具有以下成员：

<span id="Size"></span><span id="size"></span><span id="SIZE"></span>大小  
此结构的大小。 设置为**sizeof**(设备\_DSM\_NVCACHE\_更改\_优先级\_参数)。

<span id="TargetPriority"></span><span id="targetpriority"></span><span id="TARGETPRIORITY"></span>TargetPriority  
给定逻辑块的新目标优先级的范围。

<span id="Resrved_3_"></span><span id="resrved_3_"></span><span id="RESRVED_3_"></span>Resrved\[3\]  
保留的字节数。

&gt; \[!请注意\] &gt; Windows 8.1 和更高版本的 Windows 中受支持。

 

<span id="DeviceDsmAction_NvCache_Evict"></span><span id="devicedsmaction_nvcache_evict"></span><span id="DEVICEDSMACTION_NVCACHE_EVICT"></span>**DeviceDsmAction\_NvCache\_逐出**(15 |DeviceDsmActionFlag\_非破坏性) 驱动程序将逐出缓存媒体中的数据。 逐出的所有数据，请将设备设置\_DSM\_标志\_整个\_数据\_设置\_中的范围标志**标志**的成员[ **设备\_管理\_数据\_设置\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff552527)并不包括任何[**设备\_数据\_设置\_范围**](https://msdn.microsoft.com/library/windows/hardware/ff552523)结构。

一个或多个中提供了特定逻辑块范围中收回[**设备\_数据\_设置\_范围**](https://msdn.microsoft.com/library/windows/hardware/ff552523)结构。

**DeviceDsmAction\_NvCache\_逐出**以同步方式执行操作。 任何其他操作是提供不服务，直到收回操作成功还是失败。 若要限制对应用程序使用的设备，其影响每个**DeviceDsmAction\_NvCache\_逐出**颁发的操作应包含相对较小的数据范围。 它们不应超过 10 MB，理想情况下为小于 2 MB。 这样可以尽量减少用户级别应用程序在访问设备上的数据时将遇到明显延迟的可能性。

&gt; \[!请注意\] &gt; Windows 8.1 和更高版本的 Windows 中受支持。

 

<a name="remarks"></a>备注
-------

如果按位**或者**的**设备\_数据\_管理\_设置\_操作**常量值和**DeviceDsmActionFlag\_非破坏性**执行标志，指定的操作会造成任何破坏。 如果设置此标志，该驱动程序可以安全地将转发[ **IOCTL\_存储\_管理\_数据\_设置\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff560573)请求即使堆栈中的下一个较低驱动程序到驱动程序不处理指定的操作。

&gt; \[!请注意\]&gt;转发之前[ **IOCTL\_存储\_管理\_数据\_设置\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff560573)请求，该驱动程序仍执行的数据集范围中指定的块的正常处理[**设备\_管理\_数据\_设置\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff552527)结构。 此块位于**DataSetRangesOffset**和包含格式化为一个或多个连续项[**设备\_数据\_设置\_范围**](https://msdn.microsoft.com/library/windows/hardware/ff552523)结构。 在中设置数据集范围的长度，以字节为单位， **DataSetRangesLength**的成员**设备\_管理\_数据\_设置\_特性**。

 

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
<td align="left"><p>从 Windows 7 开始可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntddstor.h （包括 Ntddstor.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**设备\_DSM\_通知\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff819207)

[**DEVICE\_MANAGE\_DATA\_SET\_ATTRIBUTES**](https://msdn.microsoft.com/library/windows/hardware/ff552527)

[**IOCTL\_STORAGE\_MANAGE\_DATA\_SET\_ATTRIBUTES**](https://msdn.microsoft.com/library/windows/hardware/ff560573)

 

 






