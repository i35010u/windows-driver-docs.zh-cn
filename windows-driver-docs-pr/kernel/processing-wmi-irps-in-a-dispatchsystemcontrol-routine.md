---
title: 处理 DispatchSystemControl 例程中的 WMI IRP
description: 处理 DispatchSystemControl 例程中的 WMI IRP
ms.assetid: 9f1fc209-ee32-4270-87e5-e360ca5eca17
keywords:
- WMI WDK 内核请求
- 请求 WDK WMI
- Irp WDK WMI
- DispatchSystemControl 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94e6c988e4ea5272eeb8f5df88948309cc0cb03a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378793"
---
# <a name="processing-wmi-irps-in-a-dispatchsystemcontrol-routine"></a>处理 DispatchSystemControl 例程中的 WMI IRP





处理中的 WMI Irp 的驱动程序及其[ *DispatchSystemControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程必须处理此类 IRP 仅当处的设备对象指针**Parameters.WMI.ProviderId**匹配由驱动程序对其调用中传递的指针[ **IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)。 否则，该驱动程序必须转发到下一个较低的驱动程序 IRP。

如果该驱动程序将处理该请求，则它必须：

检查在 GUID **Parameters.WMI.DataPath**若要确定它是否表示驱动程序支持的数据块和，如果不是，失败，状态 IRP\_WMI\_GUID\_不\_找到。

驱动程序应检查输入**WNODE\_* XXX*** 在结构**Parameters.WMI.Buffer**实例名称时处理任何以下请求：

[**IRP\_MN\_查询\_单个\_实例**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)
[**IRP\_MN\_更改\_单一\_实例**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-instance)
[**IRP\_MN\_更改\_单一\_项**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-item) 
 [ **IRP\_MN\_EXECUTE\_方法**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method)是驱动程序应检查实例名称，如下所示：

- 如果 WNODE\_标志\_静态\_实例\_中设置的名称**WnodeHeader.Flags**，使用**InstanceIndex**作为驱动程序的列表中的索引该块的静态实例名称。

- 如果 WNODE\_标志\_静态\_实例\_名称是明确**WnodeHeader.Flags**，使用**OffsetInstanceName**为到实例的偏移量输入中的字符串命名**WNODE\_* XXX*** 结构。 **OffsetInstanceName**是从结构开始到指示以字节为单位 （不是字符），实例名称字符串的长度包括 NUL 终止符 （如果存在） 后, 跟字符串本身 USHORT 字节中的偏移量中Unicode。

如果该驱动程序找不到指定的实例**InstanceIndex**或**OffsetInstanceName**，它必须失败，状态 IRP\_WMI\_实例\_不\_找到。

有关[ **IRP\_MN\_EXECUTE\_方法**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method)请求，检查**MethodID**输入中[ **WNODE\_方法\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_method_item)并为该数据块，该方法无效，如果失败，状态 IRP\_WMI\_ITEMID\_不\_找到。

如果该请求将生成输出，驱动程序应检查在缓冲区的大小**Parameters.WMI.BufferSize**时处理任何以下请求：

[**IRP\_MN\_查询\_所有\_数据**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data)
[**IRP\_MN\_查询\_单一\_实例**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)
[**IRP\_MN\_EXECUTE\_方法**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method)如果缓冲区太小，无法接收输出中，但至少**sizeof**(**WNODE\_过\_小**)，该驱动程序应成功 IRP 和写入[ **WNODE\_过\_小**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_too_small)结构在缓冲区**Parameters.WMI.Buffer**。 如果缓冲区小于**sizeof**(**WNODE\_过\_小**)，该驱动程序失败，状态 NTSTATUS 代码 IRP\_缓冲区\_过\_小。

如果该请求将生成输出缓冲区大小为足够，编写以下代码输出到的缓冲区**Parameters.WMI.Buffer**:
-   有关**IRP\_MN\_查询\_所有\_数据**请求、 驱动程序写入[ **WNODE\_所有\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_all_data)结构，其中包含的所有实例指定的数据块的数据。
-   有关**IRP\_MN\_查询\_单个\_实例**请求、 驱动程序写入[ **WNODE\_单一\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_instance)结构，其中包含一个数据块的指定实例数据。
-   有关**IRP\_MN\_EXECUTE\_方法**如果此方法将生成输出，该驱动程序会写入后面输入的驱动程序确定格式输出的方法[ **WNODE\_方法\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_method_item)缓冲区 （如果有，则覆盖输入的数据） 中。

设置**Irp-&gt;IoStatus.Information**写入的缓冲区的字节数**Parameters.WMI.Buffer**并**Irp-&gt;IoStatus.Status**到状态\_成功。

调用[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)完成 IRP。

有关详细信息，请参阅[WMI WNODE\_*XXX*结构](wmi-wnode-xxx-structures.md)。

 

 




