---
title: 处理 DispatchSystemControl 例程中的 WMI IRP
description: 处理 DispatchSystemControl 例程中的 WMI IRP
ms.assetid: 9f1fc209-ee32-4270-87e5-e360ca5eca17
keywords:
- WMI WDK 内核，请求
- 请求 WDK WMI
- Irp WDK WMI
- DispatchSystemControl 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f4aa0d0d368a36a5a52c265406c82b2493c410d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827585"
---
# <a name="processing-wmi-irps-in-a-dispatchsystemcontrol-routine"></a>处理 DispatchSystemControl 例程中的 WMI IRP





仅当**参数. ProviderId**中的设备对象指针与驱动程序在其对[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)的调用中传递的指针匹配时，处理其[*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程中的 WMI irp 的驱动程序才能处理此类 irp。 否则，驱动程序必须将 IRP 转发到下一个较低版本的驱动程序。

如果驱动程序处理请求，则必须执行以下操作：

检查**数据路径**中的 GUID，以确定它是否代表驱动程序支持的数据块，如果不是，则会使\_IRP\_GUID\_找不到\_。

在处理以下任何请求时，驱动程序应在 WNODE 中**检查**实例名称的输入 **\_* XXX*** 结构：

[**Irp\_MN\_QUERY\_单一\_实例**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)
[**irp\_MN\_更改\_单个\_实例**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-instance)
[**irp\_MN\_更改\_单个\_ITEM**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-item)
[**IRP\_MN\_执行\_方法**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method)，驱动程序应按如下所示检查实例名称：

- 如果 WNODE\_标记\_静态\_实例在**WnodeHeader**中设置\_名称，请使用**InstanceIndex**作为该块的静态实例名称列表中的索引。

- 如果 WNODE\_标记\_静态\_\_实例在**WnodeHeader**中为空，则使用**OffsetInstanceName**作为输入**WNODE\_* XXX*** 结构中实例名称字符串的偏移量。 **OffsetInstanceName**是从结构开始到 USHORT 的偏移量（以字节为单位），该偏移量表示实例名称字符串的长度（以字节为单位，其中包含 NUL 终止符，如存在），后跟 Unicode 中的字符串本身。

如果驱动程序找不到**InstanceIndex**或**OffsetInstanceName**指定的实例，则它必须使 IRP\_实例的状态\_WMI 实例\_但找不到\_。

对于[**IRP\_MN\_执行\_方法**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method)请求，请在 input [**WNODE\_方法\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)中检查**MethodID** ，如果该方法对于该数据块无效，则会使 IRP 的状态\_WMI\_\_找不到 ITEMID\_。

如果请求生成输出，驱动程序应在处理以下任何请求时，检查**参数.** node.js 的缓冲区大小。

[**IRP\_MN\_query\_所有\_数据**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data)
[**irp\_MN\_查询\_单个\_实例**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)
[**irp\_MN\_执行\_方法**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method)如果缓冲区太小而无法接收输出，但至少为**sizeof**（**WNODE\_太少**），则驱动程序应成功完成 IRP，并将[**WNODE\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_too_small) **Parameters。** \_\_ 如果缓冲区小于**sizeof**（**WNODE\_太小\_** ），则驱动程序将无法使用 NTSTATUS 状态的 NTSTATUS 代码将 IRP\_缓冲区\_\_太小。

如果请求生成输出并且缓冲区大小充足，请将以下输出写入缓冲区中的**参数. buffer**：
-   对于**IRP\_MN\_QUERY\_所有\_数据**请求，驱动程序将写入包含指定数据块所有实例的数据的[**所有\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data)结构的 WNODE。\_
-   对于**IRP\_MN\_QUERY\_单一\_实例**请求，驱动程序将写入包含数据块指定实例的数据的[**WNODE\_单个\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)结构。
-   对于**IRP\_MN\_执行\_方法**，前提是该方法生成输出时，驱动程序会在缓冲区中的输入[**WNODE\_\_方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)之后以驱动程序确定的格式写入方法输出（覆盖输入数据（如果有）。

将**Irp&gt;IoStatus**设置为写入缓冲区中的字节数。 **IoStatus&gt;** **，并将**\_状态设置为 "成功"。

调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)完成 IRP。

有关详细信息，请参阅[WMI WNODE\_*XXX*结构](wmi-wnode-xxx-structures.md)。

 

 




