---
title: GPIO 控制器驱动程序的中断同步
description: GPIO 控制器驱动程序可以调用 GPIO_CLX_AcquireInterruptLock 和 GPIO_CLX_ReleaseInterruptLock 方法来获取和释放由 GPIO framework 扩展（GpioClx）在内部实现的中断锁。
ms.assetid: D9698A50-7CC2-463C-9E46-7FE428F3193E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 564b456369b600ae0ba23ebfe38616f52f6f9f6e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824937"
---
# <a name="interrupt-synchronization-for-gpio-controller-drivers"></a>GPIO 控制器驱动程序的中断同步


GPIO 控制器驱动程序可以调用[**gpio\_CLX\_AcquireInterruptLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_acquireinterruptlock)和[**gpio\_CLX\_ReleaseInterruptLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_releaseinterruptlock)方法来获取和释放由 GPIO 内部实现的中断锁framework 扩展（GpioClx）。 在 IRQL = 被动\_级别运行的驱动程序代码可以调用这些方法以同步到 GpioClx 中的中断服务例程（ISR）。 GpioClx 专用在 GPIO 控制器中的每个引脚插槽之间单独中断锁定。

如果 GPIO 控制器的硬件注册是内存映射的，则 GpioClx 中的 ISR 将在 DIRQL 调用某些驱动程序实现的事件回调函数;GpioClx 在被动\_级别调用回调函数的其余部分。 访问寄存器银行的被动级别回调函数可能需要使用中断锁来同步到在 DIRQL 上运行并访问相同寄存器的回调函数。

例如，被动级[*客户端\_EnableInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_enable_interrupt)和[*客户端\_DisableInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_disable_interrupt)回调函数修改硬件设置，这些设置会影响在 DIRQL 上运行的其他中断相关回调例程的操作。 *客户端\_EnableInterrupt*和*客户端\_DisableInterrupt*函数通常使用银行中断锁来同步其寄存器访问。

GpioClx 会自动序列化发生在 DIRQL 上的与中断相关的和与 i/o 相关的回调。 GpioClx 在 DIRQL 调用回调函数之前获取目标 bank 的中断锁，并在函数返回后释放该锁。 调用 DIRQL 时调用的回调函数尝试 **\_通过\_AcquireInterruptLock**重新获取 bank 中断锁，这是一个错误。

同样，GpioClx 会自动序列化被动\_级别发生的回调。 GpioClx 在内部实现每个银行的等待锁。 GpioClx 在被动\_级别调用回调函数之前获取目标 bank 的等待锁，并在该函数返回时释放该锁。 对于内存映射的 GPIO 控制器，GpioClx 代表驱动程序管理银行等待锁，但不允许驱动程序显式获取和释放锁。

但是，对于非内存映射的 GPIO 控制器， **GPIO\_CLX\_AcquireInterruptLock**和**GPIO\_CLX\_ReleaseInterruptLock**获取并释放等待锁，而不是中断锁。 GpioClx 为 GPIO 控制器中的每个 pin bank 实现一个单独的等待锁。 由于寄存器不是内存映射的，因此，所有与中断相关的回调函数和与 i/o 相关的回调函数都是在被动\_级别调用的，因此它们可以使用 i/o 请求通过串行总线（例如 I I I C）访问寄存器。 GpioClx 在调用其中一个回调函数之前获取目标 bank 的等待锁，并在函数返回后释放该锁。

非内存映射控制器的回调函数尝试通过调用**GPIO\_CLX\_AcquireInterruptLock**来重新获取银行等待锁是错误的。 但是，回调函数之外的被动级驱动程序代码可以调用**GPIO\_CLX\_*Xxx*InterruptLock**方法以同步到回调函数。 由于 GpioClx 在被动\_级别调用所有中断相关和与 i/o 相关的回调函数，因此，bank wait 锁定会有效地取代非内存映射控制器的银行中断锁。

非内存映射控制器的另一个选项是控制器驱动程序实现一组等待锁。 通过这些等待锁，回调例程可以对共享资源进行更精细的锁定和解锁，而不是使用 GpioClx 实现的等待锁。

在调用[*客户端\_QueryControllerBasicInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)回调例程期间，GPIO 控制器驱动程序会向 GpioClx 报告控制器寄存器是否为内存映射。 有关详细信息，请参阅客户端\_控制器中的**MemoryMappedController**标志的说明[ **\_基本\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/ns-gpioclx-_client_controller_basic_information)。

有关中断锁和等待锁的详细信息，请参阅[使用框架锁](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-framework-locks)。

下表提供了有关在 DIRQL 而不是在被动\_级别调用的回调函数的更详细信息（如果寄存器为内存映射）。 表后面的注释说明了被动级别回调函数应使用中断锁的时间。

-   [与中断相关的回调函数](#interrupt-related-callback-functions)
-   [与 i/o 相关的回调函数](#io-related-callback-functions)
-   [GPIO 初始化和与安装程序相关的回调函数](#gpio-initialization-and-setup-related-callback-functions)
-   [与 GPIO 电源管理相关的回调函数](#gpio-power-management-related-callback-functions)
-   [其他回调函数](#other-callback-functions)

## <a name="interrupt-related-callback-functions"></a>与中断相关的回调函数


为了支持配置为中断输入的 GPIO pin，GPIO 控制器驱动程序实现了一组事件回调函数以通过这些 pin 管理中断请求。 在下表中，中间列指示在 GPIO 控制器的硬件注册为内存映射的情况下调用函数的 IRQL。 最右边的列指示在下列情况中调用函数的 IRQL：寄存器未进行内存映射，并且必须通过串行总线进行访问。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>回调函数</th>
<th>如果内存映射（MemoryMappedController = 1），则为 IRQL</th>
<th>如果连续访问，则为 IRQL （MemoryMappedController = 0）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_enable_interrupt" data-raw-source="[&lt;em&gt;CLIENT_EnableInterrupt&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_enable_interrupt)"><em>CLIENT_EnableInterrupt</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_disable_interrupt" data-raw-source="[&lt;em&gt;CLIENT_DisableInterrupt&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_disable_interrupt)"><em>CLIENT_DisableInterrupt</em></a></p></td>
<td><p>PASSIVE_LEVEL</p>
<p>（请参阅注释1）。</p></td>
<td><p>PASSIVE_LEVEL</p>
<p>（请参阅备注2。）</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_clear_active_interrupts" data-raw-source="[&lt;em&gt;CLIENT_ClearActiveInterrupts&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_clear_active_interrupts)"><em>CLIENT_ClearActiveInterrupts</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_mask_interrupts" data-raw-source="[&lt;em&gt;CLIENT_MaskInterrupts&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_mask_interrupts)"><em>CLIENT_MaskInterrupts</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_active_interrupts" data-raw-source="[&lt;em&gt;CLIENT_QueryActiveInterrupts&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_active_interrupts)"><em>CLIENT_QueryActiveInterrupts</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_enabled_interrupts" data-raw-source="[&lt;em&gt;CLIENT_QueryEnabledInterrupts&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_enabled_interrupts)"><em>CLIENT_QueryEnabledInterrupts</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_reconfigure_interrupt" data-raw-source="[&lt;em&gt;CLIENT_ReconfigureInterrupt&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_reconfigure_interrupt)"><em>CLIENT_ReconfigureInterrupt</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_unmask_interrupt" data-raw-source="[&lt;em&gt;CLIENT_UnmaskInterrupt&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_unmask_interrupt)"><em>CLIENT_UnmaskInterrupt</em></a></p></td>
<td><p>DIRQL</p>
<p>（请参阅备注3。）</p></td>
<td><p>PASSIVE_LEVEL</p>
<p>（请参阅备注4。）</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_pre_process_controller_interrupt" data-raw-source="[&lt;em&gt;CLIENT_PreProcessControllerInterrupt&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_pre_process_controller_interrupt)"><em>CLIENT_PreProcessControllerInterrupt</em></a></p></td>
<td><p>DIRQL</p>
<p>（请参阅注释5。）</p></td>
<td><p>DIRQL</p>
<p>（请参阅备注6。）</p></td>
</tr>
</tbody>
</table>

 

**注意**

1.  在调用此回调函数之前，GpioClx 不会获取银行中断锁。 如果需要，回调函数可以获取银行中断锁，以同步与在 DIRQL 运行的回调函数共享的寄存器的访问。

2.  GpioClx 将对此回调函数的调用与在被动\_级别调用的、与中断相关的或与 i/o 相关的回调函数序列化。 因此，回调函数不应尝试获取 bank wait 锁。

3.  GpioClx 在调用此回调函数之前获取银行中断锁，并在函数返回后释放该锁。 因此，回调函数不应尝试获取银行中断锁。

4.  GpioClx 将对此回调函数的调用与在被动\_级别调用的、与中断相关的或与 i/o 相关的回调函数序列化。 因此，回调函数不应尝试获取 bank wait 锁。

5.  GpioClx 在调用此回调函数之前获取银行中断锁，并在函数返回后释放该锁。 因此，回调函数不应尝试获取银行中断锁。

6.  在调用此回调函数之前，GpioClx 不会获取银行中断锁。 GPIO 控制器驱动程序负责提供可能需要的任何同步。

## <a name="io-related-callback-functions"></a>与 i/o 相关的回调函数


为了支持配置为数据 i/o 引脚的 GPIO pin，GPIO 控制器驱动程序实现了一组事件回调函数以管理通过这些 pin 的 i/o 操作。 在下表中，中间列指示在 GPIO 控制器的硬件注册为内存映射的情况下调用函数的 IRQL。 最右边的列指示在下列情况中调用函数的 IRQL：寄存器未进行内存映射，并且必须通过串行总线进行访问。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>回调函数</th>
<th>如果内存映射（MemoryMappedController = 1），则为 IRQL</th>
<th>如果连续访问，则为 IRQL （MemoryMappedController = 0）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_connect_io_pins" data-raw-source="[&lt;em&gt;CLIENT_ConnectIoPins&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_connect_io_pins)"><em>CLIENT_ConnectIoPins</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_disconnect_io_pins" data-raw-source="[&lt;em&gt;CLIENT_DisconnectIoPins&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_disconnect_io_pins)"><em>CLIENT_DisconnectIoPins</em></a></p></td>
<td><p>PASSIVE_LEVEL</p>
<p>（请参阅注释1）。</p></td>
<td><p>PASSIVE_LEVEL</p>
<p>（请参阅备注2。）</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_read_pins" data-raw-source="[&lt;em&gt;CLIENT_ReadGpioPins&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_read_pins)"><em>CLIENT_ReadGpioPins</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_read_pins_mask" data-raw-source="[&lt;em&gt;CLIENT_ReadGpioPinsUsingMask&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_read_pins_mask)"><em>CLIENT_ReadGpioPinsUsingMask</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_write_pins" data-raw-source="[&lt;em&gt;CLIENT_WriteGpioPins&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_write_pins)"><em>CLIENT_WriteGpioPins</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_write_pins_mask" data-raw-source="[&lt;em&gt;CLIENT_WriteGpioPinsUsingMask&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_write_pins_mask)"><em>CLIENT_WriteGpioPinsUsingMask</em></a></p></td>
<td><p>DIRQL</p>
<p>（请参阅备注3。）</p></td>
<td><p>PASSIVE_LEVEL</p>
<p>（请参阅备注4。）</p></td>
</tr>
</tbody>
</table>

 

**注意**

1.  在调用此回调函数之前，GpioClx 不会获取银行中断锁。 如果需要，回调函数可以获取中断锁，以同步与在 DIRQL 运行的回调函数共享的寄存器的访问。

2.  GpioClx 将对此回调函数的调用与在被动\_级别调用的、与中断相关的或与 i/o 相关的回调函数序列化。 因此，回调函数不应尝试获取 bank wait 锁。

3.  GpioClx 在调用此回调函数之前获取银行中断锁，并在函数返回后释放该锁。 因此，回调函数不应尝试获取银行中断锁。

4.  GpioClx 将对此回调函数的调用与在被动\_级别调用的、与中断相关的或与 i/o 相关的回调函数序列化。 因此，回调函数不应尝试获取 bank wait 锁。

## <a name="gpio-initialization-and-setup-related-callback-functions"></a>GPIO 初始化和与安装程序相关的回调函数


若要设置 GPIO 控制器以执行 i/o 和中断操作，GPIO 控制器驱动程序将实现一组事件回调函数以初始化控制器。 在下表中，中间列指示在 GPIO 控制器的硬件注册为内存映射的情况下调用函数的 IRQL。 最右边的列指示在下列情况中调用函数的 IRQL：寄存器未进行内存映射，并且必须通过串行总线进行访问。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>回调函数</th>
<th>如果内存映射（MemoryMappedController = 1），则为 IRQL</th>
<th>如果连续访问，则为 IRQL （MemoryMappedController = 0）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_prepare_controller" data-raw-source="[&lt;em&gt;CLIENT_PrepareController&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_prepare_controller)"><em>CLIENT_PrepareController</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_release_controller" data-raw-source="[&lt;em&gt;CLIENT_ReleaseController&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_release_controller)"><em>CLIENT_ReleaseController</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_start_controller" data-raw-source="[&lt;em&gt;CLIENT_StartController&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_start_controller)"><em>CLIENT_StartController</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_stop_controller" data-raw-source="[&lt;em&gt;CLIENT_StopController&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_stop_controller)"><em>CLIENT_StopController</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information" data-raw-source="[&lt;em&gt;CLIENT_QueryControllerBasicInformation&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)"><em>CLIENT_QueryControllerBasicInformation</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_set_controller_information" data-raw-source="[&lt;em&gt;CLIENT_QuerySetControllerInformation&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_set_controller_information)"><em>CLIENT_QuerySetControllerInformation</em></a></p></td>
<td><p>PASSIVE_LEVEL</p>
<p>（请参阅注释1）。</p></td>
<td><p>PASSIVE_LEVEL</p>
<p>（请参阅备注2。）</p></td>
</tr>
</tbody>
</table>

 

**注意**

1.  当 GpioClx 调用这些回调函数中的任何一个时，银行中断锁将不可用。 因此，这些回调函数不应尝试获取银行中断锁。

2.  调用这些回调函数时，GpioClx bank 等待锁不可用。 因此，驱动程序不应尝试获取 bank wait 锁以同步到这些回调函数。

## <a name="gpio-power-management-related-callback-functions"></a>与 GPIO 电源管理相关的回调函数


为了使 GPIO 控制器能够更改设备电源状态，GPIO 控制器驱动程序实现了一组事件回调函数来保存和还原这些更改期间的硬件设置。 在下表中，中间列指示在 GPIO 控制器的硬件注册为内存映射的情况下调用函数的 IRQL。 最右边的列指示在下列情况中调用函数的 IRQL：寄存器未进行内存映射，并且必须通过串行总线进行访问。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>回调函数</th>
<th>如果内存映射（MemoryMappedController = 1），则为 IRQL</th>
<th>如果连续访问，则为 IRQL （MemoryMappedController = 0）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_restore_bank_hardware_context" data-raw-source="[&lt;em&gt;CLIENT_RestoreBankHardwareContext&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_restore_bank_hardware_context)"><em>CLIENT_RestoreBankHardwareContext</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_save_bank_hardware_context" data-raw-source="[&lt;em&gt;CLIENT_SaveBankHardwareContext&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_save_bank_hardware_context)"><em>CLIENT_SaveBankHardwareContext</em></a></p></td>
<td><p>DIRQL 或 HIGH_LEVEL</p>
<p>（请参阅说明。）</p></td>
<td><p>不支持。</p></td>
</tr>
</tbody>
</table>

 

**注意**

-   对于常规 F 状态转换：使用在 DIRQL 上由 GpioClx 持有的银行中断锁调用保存/还原回调函数。 因此，两个回调函数都不应尝试获取银行中断锁。

<!-- -->

-   对于关键 F 状态转换：当调用 power engine 插件（PEP）来保存和还原 GPIO 状态时，将调用保存/还原回调。 保存/还原回调函数在上一个处理器处于空闲状态的最高\_级别调用，后者在平台深度空闲转换序列的后期进行。 因此，两个回调函数都不应尝试获取银行中断锁。

有关 F 状态的详细信息，请参阅[组件级电源管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/component-level-power-management)。 有关 PEP 的详细信息，请参阅[**PoFxPowerControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxpowercontrol)。

## <a name="other-callback-functions"></a>其他回调函数


为了使 GPIO 控制器支持特定于控制器的操作，GPIO 控制器驱动程序实现\_ControllerSpecificFunction 事件回调函数的[*客户端*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_controller_specific_function)。 在下表中，中间列指示在 GPIO 控制器的硬件注册为内存映射的情况下调用函数的 IRQL。 最右边的列指示在下列情况中调用函数：如果寄存器未进行内存映射，并且必须通过串行总线进行访问。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>回调函数</th>
<th>如果内存映射（MemoryMappedController = 1），则为 IRQL</th>
<th>如果连续访问，则为 IRQL （MemoryMappedController = 0）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_controller_specific_function" data-raw-source="[&lt;em&gt;CLIENT_ControllerSpecificFunction&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_controller_specific_function)"><em>CLIENT_ControllerSpecificFunction</em></a></p></td>
<td><p>PASSIVE_LEVEL</p>
<p>（请参阅注释1）。</p></td>
<td><p>PASSIVE_LEVEL</p>
<p>（请参阅备注2。）</p></td>
</tr>
</tbody>
</table>

 

**注意**

1.  在调用此回调函数之前，GpioClx 不会获取银行中断锁。 如果需要，回调函数可以获取银行中断锁，以同步与在 DIRQL 运行的回调函数共享的寄存器的访问。

2.  GpioClx 将对此回调函数的调用与在被动\_级别调用的、与中断相关的或与 i/o 相关的回调函数序列化。 因此，回调函数不应尝试获取 bank wait 锁。

 

 




