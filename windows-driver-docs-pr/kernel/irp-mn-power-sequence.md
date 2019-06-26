---
title: IRP_MN_POWER_SEQUENCE
description: 此 IRP 返回设备的 power 序列值。
ms.date: 08/12/2017
ms.assetid: f00c0021-a909-4d76-9114-6710e1aa4307
keywords:
- IRP_MN_POWER_SEQUENCE Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: cc80b848a2e4b93ae8d6c33651d8caffa23a1f7b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383310"
---
# <a name="irpmnpowersequence"></a>IRP\_MN\_POWER\_SEQUENCE


此 IRP 返回设备的 power 序列值。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_电源**](irp-mj-power.md)时发送
---------

驱动程序将此 IRP 发送作为一种优化以确定是否在其设备实际输入特定电源状态。 对此 IRP 的支持是可选的。

若要发送此 IRP，驱动程序必须调用[ **IoAllocateIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)分配指定的主要 IRP 代码 IRP [ **IRP\_MJ\_POWER**](irp-mj-power.md)和次要 IRP 代码**IRP\_MN\_POWER\_序列**。 然后，该驱动程序必须调用[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) (Windows Vista) 或[ **PoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver) （Windows Server 2003、 Windows XP 和 Windows 2000) 以将 IRP 传递给下一个较低的驱动程序。 电源管理器无法发送此 IRP。

必须在 IRQL 运行此 IRP 的发件人&lt;= 调度\_级别。

## <a name="input-parameters"></a>输入参数


无。

## <a name="output-parameters"></a>输出参数


**Parameters.PowerSequence**指向**电源\_序列**结构包含下列成员：

<a href="" id="sequenced1"></a>**SequenceD1**  
设备已在 D1 或更低的电源状态次数。

<a href="" id="sequenced2"></a>**SequenceD2**  
设备已电源状态下 D2 或更低版本次数。

<a href="" id="sequenced3"></a>**SequenceD3**  
设备已电源状态下 D3 次数。

序列值跟踪设备已在相应的电源状态或低功率状态最小次数。

总线驱动程序中的值会递增**SequenceD1**， **SequenceD2**，并**SequenceD3**至少每次设备进入相应的电源状态或更低版本中电源状态。

## <a name="io-status-block"></a>I/O 状态块


驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功以指示它已返回所需的信息，或状态\_不\_，指示它的实现不支持此 IRP。

<a name="operation"></a>操作
---------

此 IRP 返回设备的 power 序列值。 总线驱动程序可以根据需要处理它;函数和筛选器驱动程序可以根据需要将其发送。

对于需要很长时间，以更改状态的设备，此 IRP 提供了一项实用优化。 每次设备更改其电源状态，其总线驱动程序递增该电源状态的序列值。 总线驱动程序在启动时初始化序列值和连续此后; 递增它们需要不重置为零。

设备策略所有者可以一次发送此 IRP，若要关闭设备之前获取的序列值，并再一次还原到设备的电源时获取新值。 通过比较值的两个集，该驱动程序可以确定设备是否确实进入低功率状态。 如果设备不会失去 power，驱动程序可以避免耗时重新初始化设备返回到 D0 状态时。

例如，如果设备需要较长时间才能恢复电源达到 D2 状态后的，可以存储驱动程序**SequenceD2**值之前它设置设备状态进入 D2 或更低。 更高版本，当时 power 正在恢复到该设备，该驱动程序可比较的新**SequenceD2**值，该值具有其存储的值以确定设备状态是否实际删除 D2 的下方。 如果值匹配，该设备没有实际输入电源状态 D2 或较低的状态，并驱动程序可以避免重新初始化该设备。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h 中 （包括 wdm.h 中、 Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

 

 




