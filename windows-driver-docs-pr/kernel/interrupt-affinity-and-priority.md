---
title: 中断相关性
description: 中断相关性
ms.assetid: e36a52d0-3a94-4017-b4a1-0b41f737523c
keywords:
- 中断服务例程 WDK 内核相关性
- Isr WDK 内核相关性
- 关联策略 WDK 中断
- IRQ_DEVICE_POLICY
- 处理器关联 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0993e0338afb3d191a755f6b642c4f8cb4762d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369771"
---
# <a name="interrupt-affinity"></a>中断相关性


*相关性*中断是可以为服务中断的处理器组。 每台设备都*相关性策略*。 操作系统使用的关联策略来计算该设备的中断的关联。 关联策略可以指定设备的 INF 文件或注册表设置。

从 Windows Vista 开始，管理员可以使用注册表设置中断的关联策略。

管理员可以设置下的以下条目 **\\中断管理\\关联策略**注册表项：

-   **DevicePolicy**是 REG\_DWORD 值，该值指定的关联策略。 每个可能的设置对应于[ **IRQ\_设备\_策略**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_irq_device_policy)值。


-   **AssignmentSetOverride**是 REG\_二进制值，该值指定[ **KAFFINITY** ](#about-kaffinity)掩码。 如果**DevicePolicy**是 0x04 (**IrqPolicySpecifiedProcessors**)，则此掩码指定一组处理器，若要将分配到设备的中断。

下表列出[ **IRQ\_设备\_策略**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_irq_device_policy)值和相应的注册表设置为**DevicePolicy**。 每个值的含义的详细信息，请参阅[ **IRQ\_设备\_策略**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_irq_device_policy)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>IRQ_DEVICE_POLICY 值</th>
<th>在注册表中的数字值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>IrqPolicyMachineDefault</strong></p></td>
<td><p>0x00</p></td>
</tr>
<tr class="even">
<td><p><strong>IrqPolicyAllCloseProcessors</strong></p></td>
<td><p>0x01</p></td>
</tr>
<tr class="odd">
<td><p><strong>IrqPolicyOneCloseProcessor</strong></p></td>
<td><p>0x02</p></td>
</tr>
<tr class="even">
<td><p><strong>IrqPolicyAllProcessorsInMachine</strong></p></td>
<td><p>0x03</p></td>
</tr>
<tr class="odd">
<td><p><strong>IrqPolicySpecifiedProcessors</strong></p></td>
<td><p>0x04</p></td>
</tr>
<tr class="even">
<td><p><strong>IrqPolicySpreadMessagesAcrossAllProcessors</strong></p></td>
<td><p>0x05</p></td>
</tr>
</tbody>
</table>

 

驱动程序的 INF 文件可以提供的注册表值的默认设置。 下面是如何设置的示例**DevicePolicy**值设置为**IrqPolicyOneCloseProcessor** INF 文件中。 有关详细信息，请参阅[ **INF AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)。

```cpp
[install-section-name.HW]
AddReg=add-registry-section 

[add-registry-section]
HKR, "Interrupt Management\Affinity Policy", DevicePolicy, 0x00010001, 2
```

系统提供的注册表设置到设备的驱动程序会在发送时[ **IRP\_MN\_筛选器\_资源\_要求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)IRP 到驱动程序。 操作系统提供[ **IO\_资源\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_resource_descriptor)结构与每个中断**类型**成员设置为**CmResourceTypeInterrupt**。 消息信号中断，CM\_资源\_中断\_消息位**标志**成员设置; 否则，很明显。 **U.Interrupt**成员描述中断的设置。

下表提供了注册表设置和成员之间的对应关系**u.Interrupt**。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>注册表值</th>
<th>You.Interrupt 的成员</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DevicePolicy</strong></p></td>
<td><p><strong>AffinityPolicy</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>AssignmentSetOverride</strong></p></td>
<td><p><strong>TargetedProcessors</strong></p></td>
</tr>
</tbody>
</table>

## <a name="about-kaffinity"></a>有关 KAFFINITY

KAFFINITY 类型是表示一组在组中的逻辑处理器的关联掩码。

```cpp
typedef ULONG_PTR  KAFFINITY;
```

KAFFINITY 类型为 32 位版本的 Windows 上的 32 位和为 64 位版本的 Windows 上的 64 位。

如果一个组中包含 n 个逻辑处理器，处理器编号从 0 到 n-1。 中的关联掩码，其中范围 0 到 n-1 是 i 位 i 表示组中的处理器数 i。 不对应于逻辑处理器的关联掩码位将始终为零。

例如，如果 KAFFINITY 值标识的组中活动的处理器，处理器掩码位是一个处理器处于活动状态，并且如果处理器未处于活动状态为零。

在关联掩码中比特数确定的最大组中的逻辑处理器数。 有关 Windows 的 64 位版本，每个组的处理器的最大数目为 64。 有关 Windows 的 32 位版本，每个组的处理器的最大数目为 32。 调用[ **KeQueryMaximumProcessorCountEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-kequerymaximumprocessorcountex)例程，以获取每个组的处理器的最大数目。 此数字取决于硬件配置的多处理器系统，但永远不会超过 64 位和 32 位版本的 Windows，分别设置的固定的 64 处理器和 32 处理器限制。

[ **GROUP_AFFINITY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/miniport/ns-miniport-_group_affinity)结构包含的关联掩码和组编号。 组号标识的关联掩码应用到的组。

内核例程使用 KAFFINITY 类型包括[ **IoConnectInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterrupt)， [ **KeQueryActiveProcessorCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-kequeryactiveprocessorcount)，和[**KeQueryActiveProcessors**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-kequeryactiveprocessors)。 

 

 

 




