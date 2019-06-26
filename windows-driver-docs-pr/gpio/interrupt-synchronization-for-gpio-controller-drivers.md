---
title: GPIO 控制器驱动程序的中断同步
description: GPIO 控制器驱动程序可以调用 GPIO_CLX_AcquireInterruptLock 和 GPIO_CLX_ReleaseInterruptLock 方法来获取和释放由 GPIO 框架扩展 (GpioClx) 在内部实现的中断锁。
ms.assetid: D9698A50-7CC2-463C-9E46-7FE428F3193E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37124c974c93ceb2c5120ad56ea8aef5e4bcec0f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363578"
---
# <a name="interrupt-synchronization-for-gpio-controller-drivers"></a>GPIO 控制器驱动程序的中断同步


GPIO 控制器驱动程序可以调用[ **GPIO\_CLX\_AcquireInterruptLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_acquireinterruptlock)并[ **GPIO\_CLX\_ReleaseInterruptLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_releaseinterruptlock)方法来获取和释放中断由 GPIO 框架扩展 (GpioClx) 在内部实现的锁。 驱动程序代码运行在 IRQL = 被动\_级别可以调用这些方法来同步到 GpioClx 中断服务例程 (ISR)。 GpioClx 到引脚 GPIO 控制器中的每个插槽将专用的单独的中断锁。

如果 GPIO 控制器的硬件寄存器内存映射，在 GpioClx ISR 调用某些驱动程序实现事件回调函数在 DIRQL;GpioClx 调用回调函数的其余部分的被动\_级别。 访问为寄存器的插槽的被动级别回调函数可能需要中断锁用于同步对回调函数，在 DIRQL 运行并访问同一个寄存器。

例如，被动级别[*客户端\_EnableInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_enable_interrupt)并[*客户端\_DisableInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_disable_interrupt)回调函数修改硬件设置会影响在 DIRQL 运行其他中断相关的回调例程的操作。 *客户端\_EnableInterrupt*并*客户端\_DisableInterrupt*函数通常使用银行中断锁来同步其注册访问。

GpioClx 自动序列化在 DIRQL 发生的中断与和 O 相关回调。 GpioClx DIRQL，在调用回调函数之前获取目标库的中断锁定，并在函数返回之后释放的锁。 则在 DIRQL 以尝试重新获取通过调用银行中断锁时调用的回调函数返回错误**GPIO\_CLX\_AcquireInterruptLock**。

同样，GpioClx 自动序列化回调发生在被动\_级别。 GpioClx 在内部实现每个银行的等待锁。 GpioClx 在被动调用回调函数之前获取目标库的等待锁定\_级别，并在函数返回时释放锁。 对于内存映射 GPIO 控制器，GpioClx 管理代表该驱动程序的银行等待锁，但不会启用驱动程序以显式获取和释放锁。

但是，对于内存映射是 GPIO 控制器时， **GPIO\_CLX\_AcquireInterruptLock**并**GPIO\_CLX\_ReleaseInterruptLock**获取和释放而不是中断锁定等待锁。 GpioClx GPIO 控制器中实现组每组各 pin 的单独等待锁。 由于寄存器不是内存映射，所有与中断相关并且 O 相关回调函数调用在被动\_级别，以便他们可以使用 I/O 请求通过串行总线，如 I²C 访问寄存器。 GpioClx 之前调用这些回调函数之一获取目标库的等待锁，并在函数返回之后释放的锁。

它是错误的内存映射的控制器，以尝试重新获取通过调用银行等待锁的回调函数**GPIO\_CLX\_AcquireInterruptLock**。 但是，外部的回调函数的被动级驱动程序代码可以调用**GPIO\_CLX\_*Xxx*InterruptLock**方法可同步到回调函数。 因为 GpioClx 调用所有中断与和 O 相关的回调函数的被动\_级别，银行等待锁有效地考虑银行的位置中断的锁的内存映射的控制器。

内存映射的控制器的另一个选项是控制器驱动程序实现等待锁的一组。 这些等待锁可能会使执行更细粒度锁定和解锁的共享资源，不是可由 GpioClx 实现等待锁的回调例程。

在调用[*客户端\_QueryControllerBasicInformation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)回调例程 GPIO 控制器驱动程序报告给 GpioClx 控制器寄存器是否是内存映射。 有关详细信息，请参阅的说明**MemoryMappedController**中的标志[**客户端\_控制器\_BASIC\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/ns-gpioclx-_client_controller_basic_information).

有关中断锁和等待锁的详细信息，请参阅[使用 Framework 锁](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-framework-locks)。

下表提供了更多详细的信息有关的回调函数调用在 DIRQL 而不是在被动\_级别如果内存映射的寄存器。 请按照表的说明介绍被动级别回调函数应在何时使用中断锁。

-   [与中断相关的回调函数](#interrupt-related-callback-functions)
-   [O 相关回调函数](#io-related-callback-functions)
-   [GPIO 初始化和设置相关的回调函数](#gpio-initialization-and-setup-related-callback-functions)
-   [GPIO 电源管理相关的回调函数](#gpio-power-management-related-callback-functions)
-   [其他回调函数](#other-callback-functions)

## <a name="interrupt-related-callback-functions"></a>与中断相关的回调函数


若要支持配置为中断输入的 GPIO 插针，GPIO 控制器驱动程序实现了一组事件回调函数来管理通过这些引脚的中断请求。 下表中的中间列指示 IRQL 的内存映射 GPIO 控制器的硬件寄存器是否调用的函数。 最右侧的列指示 IRQL 此时如果寄存器不内存映射，并且必须通过串行总线访问调用的函数。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>回调函数</th>
<th>IRQL 如果内存映射 (MemoryMappedController = 1)</th>
<th>如果按顺序访问的 IRQL (MemoryMappedController = 0)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_enable_interrupt" data-raw-source="[&lt;em&gt;CLIENT_EnableInterrupt&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_enable_interrupt)"><em>CLIENT_EnableInterrupt</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_disable_interrupt" data-raw-source="[&lt;em&gt;CLIENT_DisableInterrupt&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_disable_interrupt)"><em>CLIENT_DisableInterrupt</em></a></p></td>
<td><p>PASSIVE_LEVEL</p>
<p>（参见备注 1）。</p></td>
<td><p>PASSIVE_LEVEL</p>
<p>（请参阅备注 2）。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_clear_active_interrupts" data-raw-source="[&lt;em&gt;CLIENT_ClearActiveInterrupts&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_clear_active_interrupts)"><em>CLIENT_ClearActiveInterrupts</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_mask_interrupts" data-raw-source="[&lt;em&gt;CLIENT_MaskInterrupts&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_mask_interrupts)"><em>CLIENT_MaskInterrupts</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_active_interrupts" data-raw-source="[&lt;em&gt;CLIENT_QueryActiveInterrupts&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_active_interrupts)"><em>CLIENT_QueryActiveInterrupts</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_enabled_interrupts" data-raw-source="[&lt;em&gt;CLIENT_QueryEnabledInterrupts&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_enabled_interrupts)"><em>CLIENT_QueryEnabledInterrupts</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_reconfigure_interrupt" data-raw-source="[&lt;em&gt;CLIENT_ReconfigureInterrupt&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_reconfigure_interrupt)"><em>CLIENT_ReconfigureInterrupt</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_unmask_interrupt" data-raw-source="[&lt;em&gt;CLIENT_UnmaskInterrupt&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_unmask_interrupt)"><em>CLIENT_UnmaskInterrupt</em></a></p></td>
<td><p>DIRQL</p>
<p>（请参阅备注 3）。</p></td>
<td><p>PASSIVE_LEVEL</p>
<p>（请参阅备注 4）。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_pre_process_controller_interrupt" data-raw-source="[&lt;em&gt;CLIENT_PreProcessControllerInterrupt&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_pre_process_controller_interrupt)"><em>CLIENT_PreProcessControllerInterrupt</em></a></p></td>
<td><p>DIRQL</p>
<p>（请参阅备注 5）。</p></td>
<td><p>DIRQL</p>
<p>（请参阅备注 6）。</p></td>
</tr>
</tbody>
</table>

 

**注意**

1.  GpioClx 不会调用此回调函数之前获取银行中断锁。 回调函数可以获取的银行中断锁，如果有必要，同步访问共享执行回调的寄存器的函数在 DIRQL 运行的。

2.  GpioClx 序列化到与其他中断与和 O 相关的回叫函数，在被动调用此回调函数的调用\_级别。 因此，回调函数不应尝试获取银行等待锁。

3.  GpioClx 之前调用此回调函数，获取银行中断锁并在函数返回之后释放的锁。 因此，回调函数不应尝试获取银行中断锁。

4.  GpioClx 序列化到与其他中断与和 O 相关的回叫函数，在被动调用此回调函数的调用\_级别。 因此，回调函数不应尝试获取银行等待锁。

5.  GpioClx 之前调用此回调函数，获取银行中断锁并在函数返回之后释放的锁。 因此，回调函数不应尝试获取银行中断锁。

6.  GpioClx 不会调用此回调函数之前获取银行中断锁。 GPIO 控制器驱动程序负责提供可能需要的任何同步。

## <a name="io-related-callback-functions"></a>O 相关回调函数


若要支持配置为数据 I/O pin 的 GPIO 插针，GPIO 控制器驱动程序实现了一组事件回调函数来管理通过这些引脚的 I/O 操作。 下表中的中间列指示 IRQL 的内存映射 GPIO 控制器的硬件寄存器是否调用的函数。 最右侧的列指示 IRQL 此时如果寄存器不内存映射，并且必须通过串行总线访问调用的函数。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>回调函数</th>
<th>IRQL 如果内存映射 (MemoryMappedController = 1)</th>
<th>如果按顺序访问的 IRQL (MemoryMappedController = 0)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_connect_io_pins" data-raw-source="[&lt;em&gt;CLIENT_ConnectIoPins&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_connect_io_pins)"><em>CLIENT_ConnectIoPins</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_disconnect_io_pins" data-raw-source="[&lt;em&gt;CLIENT_DisconnectIoPins&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_disconnect_io_pins)"><em>CLIENT_DisconnectIoPins</em></a></p></td>
<td><p>PASSIVE_LEVEL</p>
<p>（参见备注 1）。</p></td>
<td><p>PASSIVE_LEVEL</p>
<p>（请参阅备注 2）。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_read_pins" data-raw-source="[&lt;em&gt;CLIENT_ReadGpioPins&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_read_pins)"><em>CLIENT_ReadGpioPins</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_read_pins_mask" data-raw-source="[&lt;em&gt;CLIENT_ReadGpioPinsUsingMask&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_read_pins_mask)"><em>CLIENT_ReadGpioPinsUsingMask</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_write_pins" data-raw-source="[&lt;em&gt;CLIENT_WriteGpioPins&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_write_pins)"><em>CLIENT_WriteGpioPins</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_write_pins_mask" data-raw-source="[&lt;em&gt;CLIENT_WriteGpioPinsUsingMask&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_write_pins_mask)"><em>CLIENT_WriteGpioPinsUsingMask</em></a></p></td>
<td><p>DIRQL</p>
<p>（请参阅备注 3）。</p></td>
<td><p>PASSIVE_LEVEL</p>
<p>（请参阅备注 4）。</p></td>
</tr>
</tbody>
</table>

 

**注意**

1.  GpioClx 不会调用此回调函数之前获取银行中断锁。 如果有必要，同步访问共享执行回调的寄存器的函数在 DIRQL 运行的回调函数可以获取中断锁定。

2.  GpioClx 序列化到与其他中断与和 O 相关的回叫函数，在被动调用此回调函数的调用\_级别。 因此，回调函数不应尝试获取银行等待锁。

3.  GpioClx 之前调用此回调函数，获取银行中断锁并在函数返回之后释放的锁。 因此，回调函数不应尝试获取银行中断锁。

4.  GpioClx 序列化到与其他中断与和 O 相关的回叫函数，在被动调用此回调函数的调用\_级别。 因此，回调函数不应尝试获取银行等待锁。

## <a name="gpio-initialization-and-setup-related-callback-functions"></a>GPIO 初始化和设置相关的回调函数


若要设置 GPIO 控制器来执行 I/O 并中断操作，GPIO 控制器驱动程序实现了一组事件回调函数来初始化控制器。 下表中的中间列指示 IRQL 的内存映射 GPIO 控制器的硬件寄存器是否调用的函数。 最右侧的列指示 IRQL 此时如果寄存器不内存映射，并且必须通过串行总线访问调用的函数。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>回调函数</th>
<th>IRQL 如果内存映射 (MemoryMappedController = 1)</th>
<th>如果按顺序访问的 IRQL (MemoryMappedController = 0)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_prepare_controller" data-raw-source="[&lt;em&gt;CLIENT_PrepareController&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_prepare_controller)"><em>CLIENT_PrepareController</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_release_controller" data-raw-source="[&lt;em&gt;CLIENT_ReleaseController&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_release_controller)"><em>CLIENT_ReleaseController</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_start_controller" data-raw-source="[&lt;em&gt;CLIENT_StartController&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_start_controller)"><em>CLIENT_StartController</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_stop_controller" data-raw-source="[&lt;em&gt;CLIENT_StopController&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_stop_controller)"><em>CLIENT_StopController</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information" data-raw-source="[&lt;em&gt;CLIENT_QueryControllerBasicInformation&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)"><em>CLIENT_QueryControllerBasicInformation</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_set_controller_information" data-raw-source="[&lt;em&gt;CLIENT_QuerySetControllerInformation&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_set_controller_information)"><em>CLIENT_QuerySetControllerInformation</em></a></p></td>
<td><p>PASSIVE_LEVEL</p>
<p>（参见备注 1）。</p></td>
<td><p>PASSIVE_LEVEL</p>
<p>（请参阅备注 2）。</p></td>
</tr>
</tbody>
</table>

 

**注意**

1.  当 GpioClx 调用上述任何回调函数时，银行中断锁将不可用。 因此，这些回调函数不应尝试获取银行中断锁。

2.  调用这些回调函数时，GpioClx 银行等待锁不可用。 因此，该驱动程序不应尝试获取银行等待锁来同步这些回调函数。

## <a name="gpio-power-management-related-callback-functions"></a>GPIO 电源管理相关的回调函数


若要启用 GPIO 控制器来更改设备的电源状态，GPIO 控制器驱动程序实现了一组事件回调函数来保存和还原期间这些更改硬件设置。 下表中的中间列指示 IRQL 的内存映射 GPIO 控制器的硬件寄存器是否调用的函数。 最右侧的列指示 IRQL 此时如果寄存器不内存映射，并且必须通过串行总线访问调用的函数。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>回调函数</th>
<th>IRQL 如果内存映射 (MemoryMappedController = 1)</th>
<th>如果按顺序访问的 IRQL (MemoryMappedController = 0)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_restore_bank_hardware_context" data-raw-source="[&lt;em&gt;CLIENT_RestoreBankHardwareContext&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_restore_bank_hardware_context)"><em>CLIENT_RestoreBankHardwareContext</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_save_bank_hardware_context" data-raw-source="[&lt;em&gt;CLIENT_SaveBankHardwareContext&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_save_bank_hardware_context)"><em>CLIENT_SaveBankHardwareContext</em></a></p></td>
<td><p>DIRQL 或 HIGH_LEVEL</p>
<p>（请参阅注释。）</p></td>
<td><p>不支持。</p></td>
</tr>
</tbody>
</table>

 

**注意**

-   有关正则 F 状态转换：与在 DIRQL GpioClx 所持有的银行中断锁调用保存/还原回调函数。 因此，既不回调函数应尝试获取银行中断锁。

<!-- -->

-   对于关键 F 状态转换：保存/还原回调调用 power 引擎插件 (PEP) 来保存和还原的 GPIO 状态时调用。 保存/还原回调函数以高调用\_级别中的最后一个处理器处于空闲状态，较晚的平台深度空闲转换序列出现这种情况的上下文。 因此，既不回调函数应尝试获取银行中断锁。

有关 F 状态的详细信息，请参阅[组件级别电源管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/component-level-power-management)。 有关 PEP 的详细信息，请参阅[ **PoFxPowerControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxpowercontrol)。

## <a name="other-callback-functions"></a>其他回调函数


若要启用 GPIO 控制器来支持特定于控制器的操作，GPIO 控制器驱动程序实现[*客户端\_ControllerSpecificFunction* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_controller_specific_function)事件回调函数。 下表中，在中间栏中指示 IRQL 内存映射 GPIO 控制器的硬件寄存器是否调用该函数。 最右侧的列指示 IRQL 如果寄存器不内存映射，并且必须通过串行总线访问调用该函数。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>回调函数</th>
<th>IRQL 如果内存映射 (MemoryMappedController = 1)</th>
<th>如果按顺序访问的 IRQL (MemoryMappedController = 0)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_controller_specific_function" data-raw-source="[&lt;em&gt;CLIENT_ControllerSpecificFunction&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_controller_specific_function)"><em>CLIENT_ControllerSpecificFunction</em></a></p></td>
<td><p>PASSIVE_LEVEL</p>
<p>（参见备注 1）。</p></td>
<td><p>PASSIVE_LEVEL</p>
<p>（请参阅备注 2）。</p></td>
</tr>
</tbody>
</table>

 

**注意**

1.  GpioClx 不会调用此回调函数之前获取银行中断锁。 回调函数可以获取的银行中断锁，如果有必要，同步访问共享执行回调的寄存器的函数在 DIRQL 运行的。

2.  GpioClx 序列化到与其他中断与和 O 相关的回叫函数，在被动调用此回调函数的调用\_级别。 因此，回调函数不应尝试获取银行等待锁。

 

 




