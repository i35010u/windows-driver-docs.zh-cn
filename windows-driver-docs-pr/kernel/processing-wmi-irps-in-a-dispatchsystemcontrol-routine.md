---
title: 处理 DispatchSystemControl 例程中的 WMI IRP
description: 处理 DispatchSystemControl 例程中的 WMI IRP
keywords:
- WMI WDK 内核，请求
- 请求 WDK WMI
- Irp WDK WMI
- DispatchSystemControl 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64068017ca7ef604bca08692635436e38ec30265
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805407"
---
# <a name="processing-wmi-irps-in-a-dispatchsystemcontrol-routine"></a>处理 DispatchSystemControl 例程中的 WMI IRP





仅当 **参数. ProviderId** 中的设备对象指针与驱动程序在其对 [**IoWMIRegistrationControl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)的调用中传递的指针匹配时，处理其 [*DispatchSystemControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程中的 WMI irp 的驱动程序才能处理此类 irp。 否则，驱动程序必须将 IRP 转发到下一个较低版本的驱动程序。

如果驱动程序处理请求，则必须执行以下操作：

检查 **数据路径** 中的 GUID，以确定它是否代表驱动程序支持的数据块，如果不是，则会失败，并且 \_ \_ \_ 找不到状态为 WMI GUID 的状态 \_ 。

在处理以下任何请求时，驱动程序应在 **参数. Buffer** 中检查输入的 **WNODE \_ * XXX*** 结构：

[**IRP \_MN \_ 查询 \_ 单 \_ 实例**](./irp-mn-query-single-instance.md) 
 [**irp \_ MN \_ 更改 \_ 单一 \_ 实例**](./irp-mn-change-single-instance.md) 
 [**irp \_ MN \_ 更改 \_ 单一 \_ 项**](./irp-mn-change-single-item.md) 
 [**irp \_ MN \_ EXECUTE \_ 方法**](./irp-mn-execute-method.md)驱动程序应按如下所示检查实例名称：

- 如果 \_ \_ \_ \_ 在 **WnodeHeader** 中设置了 WNODE 标志静态实例名称，请使用 **InstanceIndex** 作为该块的静态实例名称列表中的索引。

- 如果 WNODE \_ 标记 \_ 静态 \_ 实例 \_ 名称在 **WnodeHeader** 中清楚，请使用 **OffsetInstanceName** 作为输入 **WNODE \_ * XXX*** 结构中实例名称字符串的偏移量。 **OffsetInstanceName** 是从结构开始到 USHORT 的偏移量（以字节为单位），该偏移量表示实例名称字符串的长度（以字节为单位） (不) 个字符，包括 NUL 终止符（如果存在），后跟 Unicode 中的字符串本身。

如果驱动程序找不到 **InstanceIndex** 或 **OffsetInstanceName** 指定的实例，则它必须失败，并且找不到状态为 \_ WMI 实例的 \_ 实例 \_ \_ 。

对于 [**IRP \_ MN \_ EXECUTE \_ 方法**](./irp-mn-execute-method.md)请求，请在 input [**WNODE \_ 方法 \_ 项**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)中检查 **MethodID** ，如果该方法对于该数据块无效，则会使 IRP 失败，状态为 " \_ WMI ITEMID 找 \_ \_ 不到" \_ 。

如果请求生成输出，驱动程序应在处理以下任何请求时，检查 **参数.** node.js 的缓冲区大小。

[**IRP \_MN \_ query \_ ALL \_ DATA**](./irp-mn-query-all-data.md) 
 [**IRP \_ MN \_ query \_ 单一 \_ 实例**](./irp-mn-query-single-instance.md) 
 [**IRP \_ MN \_ EXECUTE \_ 方法**](./irp-mn-execute-method.md)如果缓冲区太小而无法接收输出，但至少 **sizeof** (**WNODE \_ 太 \_ 小**) ，则驱动程序应成功完成 IRP，并将一个 [**WNODE \_ 太 \_ 小**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_too_small)的结构写入缓冲区中的 **Parameters.WMI.Buffer**。 如果缓冲区小于 **sizeof** (**WNODE \_ 太 \_ 小**) ，则驱动程序将使用状态缓冲区的 NTSTATUS 代码 \_ \_ 太小而失败 \_ 。

如果请求生成输出并且缓冲区大小充足，请将以下输出写入缓冲区中的 **参数. buffer**：
-   对于 **IRP \_ MN \_ 查询 \_ 所有 \_ 数据** 请求，驱动程序会写入一个 [**WNODE，该结构包含指定数据块的所有 \_ \_**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data) 实例的数据。
-   对于 **IRP \_ MN \_ 查询 \_ 单 \_ 实例** 请求，驱动程序将写入一个 [**WNODE \_ 单 \_ 实例**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance) 结构，该结构包含数据块的指定实例的数据。
-   对于 **IRP \_ MN \_ EXECUTE \_ 方法** ，如果该方法生成输出，则驱动程序会在缓冲区中的输入 [**WNODE \_ 方法 \_ 项**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item) 后写入驱动程序确定格式的方法输出， (覆盖输入数据（如果) 有）。

将 **&gt; IoStatus** 设置为写入缓冲区中的字节数，其值为 **&gt; IoStatus** ，**并在** 状态为 "成功"。 \_

调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 完成 IRP。

有关详细信息，请参阅 [WMI WNODE \_ *XXX* 结构](wmi-wnode-xxx-structures.md)。

 

