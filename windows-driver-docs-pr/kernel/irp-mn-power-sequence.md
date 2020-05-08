---
title: IRP_MN_POWER_SEQUENCE
description: 此 IRP 返回设备的电源序列值。
ms.date: 08/12/2017
ms.assetid: f00c0021-a909-4d76-9114-6710e1aa4307
keywords:
- IRP_MN_POWER_SEQUENCE 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 7780e8ded4c29646520fa95ae8243ec5bdd86bcd
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922464"
---
# <a name="irp_mn_power_sequence"></a>IRP\_MN\_幂\_序列


此 IRP 返回设备的电源序列值。

<a name="major-code"></a>主要代码
----------

[**IRP\_MJ\_POWER**](irp-mj-power.md)

<a name="when-sent"></a>发送时间
---------

驱动程序以优化形式发送此 IRP，以确定其设备是否实际进入了特定电源状态。 此 IRP 的支持是可选的。

若要发送此 IRP，驱动程序必须调用[**IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)来分配 irp，同时指定主要 Irp 代码[**irp\_MJ\_功能**](irp-mj-power.md)和次要 irp 代码**irp\_MN\_电源\_序列**。 然后，驱动程序必须调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) （windows Vista）或[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) （Windows SERVER 2003、windows XP 和 WINDOWS 2000）将 IRP 传递到下一个较低版本的驱动程序。 Power manager 无法发送此 IRP。

此 IRP 的发送方必须以 IRQL &lt;= 调度\_级别运行。

## <a name="input-parameters"></a>输入参数


无。

## <a name="output-parameters"></a>输出参数


**PowerSequence**指向具有以下成员的**幂\_序列**结构：

<a href="" id="sequenced1"></a>**SequenceD1**  
设备处于电源状态 D1 或更低状态的次数。

<a href="" id="sequenced2"></a>**SequenceD2**  
设备处于电源状态 D2 或更低状态的次数。

<a href="" id="sequenced3"></a>**SequenceD3**  
设备处于电源状态 D3 的次数。

序列值跟踪设备处于相应电源状态或降低电源状态的最小次数。

总线驱动程序会在每次设备进入相应电源状态或降低电源状态时，增加**SequenceD1**、 **SequenceD2**和**SequenceD3**中的值。

## <a name="io-status-block"></a>I/o 状态块


驱动程序将**Irp-&gt;IOSTATUS**设置为状态\_"成功" 以指示该状态为 "已返回请求的信息"\_，\_或设置为 "未实现的状态" 以指示它不支持此 Irp。

<a name="operation"></a>操作
---------

此 IRP 返回设备的电源序列值。 总线驱动程序可以选择对其进行处理;函数和筛选器驱动程序可以选择发送。

对于需要很长时间才能更改状态的设备，此 IRP 提供了一个有用的优化。 每次设备更改其电源状态时，其总线驱动程序会递增该电源状态的序列值。 总线驱动程序会在启动时对序列值进行初始化，并在此后持续递增这些值;不需要将其重置为零。

设备策略所有者可以发送此 IRP 一次，以便在关闭设备之前获得序列值，并在恢复设备的电源时再次获取新值。 通过比较两组值，驱动程序可以确定设备是否确实进入了低于电源的状态。 如果设备未断电，则当设备恢复到 D0 状态时，驱动程序可以避免耗时的重新初始化。

例如，如果设备在达到 D2 状态时需要很长的时间来恢复电源，则驱动程序可以在将设备状态设置为 D2 或更低之前存储**SequenceD2**值。 稍后，在将电源恢复到设备时，驱动程序可将新的**SequenceD2**值与存储的值进行比较，以确定设备状态是否确实已被放置在 D2 下面。 如果值匹配，则设备不会实际输入电源状态 D2 或更低的状态，并且驱动程序可以避免重新初始化设备。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wdm.h（包括 Wdm.h、Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

 

 




