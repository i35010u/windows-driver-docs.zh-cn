---
title: 'IRP_MJ_PNP (IFS) '
description: IRP\_MJ\_PNP
keywords:
- IRP_MJ_PNP 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_PNP
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78b6ca00388957efcfcb09c5f815fb8a8ac27a03
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826537"
---
# <a name="irp_mj_pnp-ifs"></a>IRP \_ MJ \_ PNP (IFS) 


## <a name="when-sent"></a>发送时间


\_ \_ 当系统上发生即插即用活动时，即插即用管理器将发送 IRP MJ PNP 请求。 其他操作系统组件以及其他内核模式驱动程序还可以发送某些 IRP \_ MJ \_ PNP 请求，具体取决于次要函数代码。

有关即插即用的对驱动程序的 IRP 处理要求的详细信息，请参阅 [即插即用](../kernel/introduction-to-plug-and-play.md)。

有关 IRP \_ MJ \_ PNP 次要功能代码的参考信息，请参阅 [即插即用次 irp](../kernel/plug-and-play-minor-irps.md)。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统应检查次要函数代码以确定请求的操作。 文件系统必须处理以下次要函数代码：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IRP_MN_CANCEL_REMOVE_DEVICE</p></td>
<td align="left"><p>指示之前的查询删除设备请求已取消。 如果需要执行任何与取消相关的清理操作，则发送此请求以提醒文件系统。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_REMOVE_DEVICE</p></td>
<td align="left"><p>指示将删除设备。 如果文件系统已装载到设备上，则 PnP 管理器会将此请求发送到文件系统和任何文件系统筛选器。 如果设备有打开的句柄，则文件系统通常无法通过查询-删除请求。 如果不是，则文件系统通常会锁定卷，以防以后创建请求成功。 如果已装载的文件系统不支持查询删除请求，则 PnP 管理器将无法对设备执行查询删除请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_REMOVE_DEVICE</p></td>
<td align="left"><p>指示将删除设备。 如果文件系统已装载到设备上，则 PnP 管理器会将此 IRP 发送到文件系统和任何文件系统筛选器。 文件系统应立即将此 IRP 传递到设备的存储驱动程序，设置一个完成例程，然后文件系统将在其中卸载卷。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_START_DEVICE</p></td>
<td align="left"><p>指示设备正在启动。 文件系统应将此 IRP 传递到设备的存储驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_SURPRISE_REMOVAL</p></td>
<td align="left"><p>指示已删除设备。 如果文件系统已装载到设备上，则 PnP 管理器会将此 IRP 发送到文件系统和任何文件系统筛选器。 文件系统应立即将此 IRP 传递到设备的存储驱动程序，设置一个完成例程，然后文件系统将在其中卸载卷。</p></td>
</tr>
</tbody>
</table>

 

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


文件系统筛选器驱动程序应根据以下指导原则处理 PnP Irp：

-   当用户要正常删除卷时，PnP 管理器会发送 IRP \_ MN \_ 查询 \_ 删除 \_ 设备请求。 接收到此 IRP 后，筛选器必须关闭卷上的所有打开的句柄，然后将 IRP 向下传递到堆栈上的下一个较低版本的驱动程序。 这一点非常重要。 如果驱动程序无法关闭所有打开的句柄，这会阻止卸载卷，进而阻止物理设备被弹出。

> [!NOTE]
> 收到 IRP \_ MN \_ 查询 \_ 删除 \_ 设备请求后，FAT 文件系统立即卸载可以安全删除的所有卷。 因此，附加到 FAT 卷的任何筛选器都应该在调用筛选器的完成例程之前释放其筛选器设备对象。 NTFS 文件系统不会执行此操作。 因此，附加到 NTFS 卷的筛选器会预计在调用筛选器的完成例程时，其设备对象仍将附加到该卷。

     

-   在 IRP \_ MN \_ 查询 \_ 删除 \_ 设备请求之后但 \_ 收到 irp MN \_ CANCEL \_ remove \_ device 或 Irp \_ MN REMOVE device 请求之前收到的 \_ irp \_ ，可以安全地向下传递堆栈 (会被存储设备堆栈) 或保留在队列中，直到收到取消删除或删除设备请求。

-   如果筛选器 \_ \_ \_ \_ 在已关闭卷的所有打开句柄以响应 irp MN 查询删除设备请求后收到 irp MN CANCEL remove device \_ 请求 \_ \_ \_ ，则它可以重新打开该句柄。 但是，在完成 IRP 后，筛选器可以在其完成例程中完成此操作。

-   当某个筛选器收到 IRP \_ MN \_ REMOVE \_ 设备请求时，它通常不需要对 IRP 执行任何处理，除非在收到 irp \_ MN \_ 查询 " \_ 删除设备" 请求后，它已将 irp 保存在队列中 \_ 。 如果它在队列中持有 Irp，则筛选器必须取消对该卷的所有 Irp 的排队，并在将 &lt; &gt; &lt; &gt; irp 向下传递到堆栈上的下一个较低版本之前，使其失败。

-   收到 IRP \_ MN \_ 意外 \_ 删除请求后，筛选器应执行以下操作：

    -   关闭卷的所有打开的句柄，因为文件系统无法清理堆栈，直到没有未完成的引用。

    -   如果筛选器在队列中持有 Irp，则它可能会失败或将其向下传递到堆栈 (会由存储设备堆栈) 失败。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序与给定的 IRP 一起调用 [**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的 *IrpSp*[**堆栈位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。  (IRP 显示为 *irp*。 ) 驱动程序可以使用在处理即插即用请求中的以下 irp 成员和 irp 堆栈位置设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--iostatus"></a>*Irp- &gt; IoStatus*  
指向 [**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block) 结构的指针，该结构接收最终完成状态和有关请求的操作的信息。

<a href="" id="irpsp--fileobject"></a>*IrpSp- &gt; FileObject*  
对于 PnP Irp，此指针应为 **NULL** 。

<a href="" id="irpsp--majorfunction"></a>*IrpSp- &gt; MajorFunction*  
指定 IRP \_ MJ \_ PNP。

<a href="" id="irpsp--minorfunction"></a>*IrpSp- &gt; MinorFunction*  
下列情况之一：

-   IRP \_ MN \_ 取消 \_ 删除 \_ 设备
-   IRP \_ MN \_ 查询 \_ 删除 \_ 设备
-   IRP \_ MN \_ 删除 \_ 设备
-   IRP \_ MN \_ 启动 \_ 设备
-   IRP \_ MN \_ 意外 \_ 删除

## <a name="see-also"></a>请参阅


[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ \_ PNP (WDK 内核参考)**](../kernel/irp-mj-pnp.md)

[**IRP \_ MN \_ 取消 \_ 删除 \_ 设备**](../kernel/irp-mn-cancel-remove-device.md)

[**IRP \_ MN \_ 查询 \_ 删除 \_ 设备**](../kernel/irp-mn-query-remove-device.md)

[**IRP \_ MN \_ 删除 \_ 设备**](../kernel/irp-mn-remove-device.md)

[**IRP \_ MN \_ 启动 \_ 设备**](../kernel/irp-mn-start-device.md)

[**IRP \_ MN \_ 意外 \_ 删除**](../kernel/irp-mn-surprise-removal.md)

