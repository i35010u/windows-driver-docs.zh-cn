---
title: 中断相关性
description: 中断相关性
keywords:
- 中断服务例程 WDK 内核，相关性
- Isr WDK 内核，相关性
- 关联策略 WDK 中断
- IRQ_DEVICE_POLICY
- 处理器关联 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: caa77c2f90ca3562d0b45476c3755e624f206d9d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815275"
---
# <a name="interrupt-affinity"></a>中断相关性


中断的 *关联* 是可以为中断服务的处理器集。 每个设备都有一个 *关联策略*。 操作系统使用关联策略来计算该设备中断的相关性。 可以在设备的 INF 文件或注册表设置中指定关联策略。

从 Windows Vista 开始，管理员可以使用注册表为中断设置关联策略。

管理员可以在 **\\ 中断管理 \\ 关联策略** 注册表项下设置以下各项：

-   **DevicePolicy** 是一个 \_ 指定关联策略的 REG DWORD 值。 每个可能的设置对应于 [**IRQ \_ 设备 \_ 策略**](/windows-hardware/drivers/ddi/wdm/ne-wdm-_irq_device_policy) 值。


-   **AssignmentSetOverride** 是 \_ 指定 [**KAFFINITY**](#about-kaffinity) 掩码的注册表二进制值。 如果 **DevicePolicy** 为 0X04 (**IrqPolicySpecifiedProcessors**) ，则此掩码指定要向其分配设备中断的一组处理器。

下表列出了 [**IRQ \_ 设备 \_ 策略**](/windows-hardware/drivers/ddi/wdm/ne-wdm-_irq_device_policy) 值，以及 **DevicePolicy** 的相应注册表设置。 有关每个值的含义的详细信息，请参阅 [**IRQ \_ 设备 \_ 策略**](/windows-hardware/drivers/ddi/wdm/ne-wdm-_irq_device_policy)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>IRQ_DEVICE_POLICY 值</th>
<th>注册表中的数值</th>
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

 

驱动程序的 INF 文件可以提供注册表值的默认设置。 下面是如何在 INF 文件中将 **DevicePolicy** 值设置为 **IrqPolicyOneCloseProcessor** 的示例。 有关详细信息，请参阅 [**INF AddReg 指令**](../install/inf-addreg-directive.md)。

```cpp
[install-section-name.HW]
AddReg=add-registry-section 

[add-registry-section]
HKR, "Interrupt Management\Affinity Policy", DevicePolicy, 0x00010001, 2
```

系统在将 [**irp \_ MN \_ FILTER \_ 资源 \_ 需求**](./irp-mn-filter-resource-requirements.md) irp 发送到驱动程序时，使注册表设置对设备的驱动程序可用。 操作系统为 **类型** 成员设置为 **CmResourceTypeInterrupt** 的每个中断提供 [**IO \_ 资源 \_ 说明符**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_resource_descriptor)结构。 对于消息发出信号中断， \_ \_ \_ 将设置 **标志** 成员的 CM 资源中断消息位; 否则，将会清除。 **U. 中断** 成员描述中断的设置。

下表提供了注册表设置和 **u** 成员之间的对应关系。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>注册表值</th>
<th>你的成员。中断</th>
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

## <a name="about-kaffinity"></a>关于 KAFFINITY

KAFFINITY 类型是一个关联掩码，它表示组中的一组逻辑处理器。

```cpp
typedef ULONG_PTR  KAFFINITY;
```

KAFFINITY 在32位版本的 Windows 上为32位，在 Windows 的64版本上为64位。

如果一个组包含 n 个逻辑处理器，则处理器编号从0到 n-1。 组中的处理器编号 i 在关联掩码中用位 i 表示，其中 i 介于0到 n-1 之间。 与逻辑处理器不对应的关联掩码位始终为零。

例如，如果 KAFFINITY 值标识组中的活动处理器，则处理器的掩码位为1，如果处理器处于活动状态，则为零，如果处理器处于非活动状态，则为零。

关联掩码中的位数确定组中的逻辑处理器的最大数目。 对于64位版本的 Windows，每个组的最大处理器数为64。 对于32位版本的 Windows，每个组的最大处理器数为32。 调用 [**KeQueryMaximumProcessorCountEx**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kequerymaximumprocessorcountex) 例程以获取每个组的最大处理器数。 此数值取决于多处理器系统的硬件配置，但绝不能超过64位32和 Windows 版本的 Windows 的64的固定和32的限制。

[**GROUP_AFFINITY**](/windows-hardware/drivers/ddi/miniport/ns-miniport-_group_affinity)结构包含一个关联掩码和一个组号。 组号用于标识关联掩码应用到的组。

使用 KAFFINITY 类型的内核例程包括 [**IoConnectInterrupt**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterrupt)、 [**KeQueryActiveProcessorCount**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kequeryactiveprocessorcount)和 [**KeQueryActiveProcessors**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kequeryactiveprocessors)。 

 

 

