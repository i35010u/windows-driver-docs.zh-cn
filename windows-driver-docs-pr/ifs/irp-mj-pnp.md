---
title: IRP_MJ_PNP
description: IRP\_MJ\_PNP
ms.assetid: aec2f309-02a1-460a-b674-33ad18286347
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
ms.openlocfilehash: ca7a088ebcade4b4211e39b8dd349bbf36c5cfc4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841171"
---
# <a name="irp_mj_pnp"></a>IRP\_MJ\_PNP


## <a name="when-sent"></a>发送时间


每当系统上发生即插即用活动时，即插即用管理器都将 IRP\_MJ\_PNP 请求发送。 其他操作系统组件以及其他内核模式驱动程序还可以将某些 IRP\_MJ 发送\_PNP 请求，具体取决于次要函数代码。

有关即插即用的对驱动程序的 IRP 处理要求的详细信息，请参阅[即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)。

有关 IRP\_MJ\_PNP 次要函数代码的参考信息，请参阅[即插即用次要 irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/plug-and-play-minor-irps)。

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

-   当用户要正常删除卷时，PnP 管理器会发送 IRP\_MN\_查询\_删除\_设备请求。 接收到此 IRP 后，筛选器必须关闭卷上的所有打开的句柄，然后将 IRP 向下传递到堆栈上的下一个较低版本的驱动程序。 这一点非常重要。 如果驱动程序无法关闭所有打开的句柄，这会阻止卸载卷，进而阻止物理设备被弹出。

    &gt; \[！请注意\] &gt; 接收 IRP\_MN\_查询\_删除\_设备请求，FAT 文件系统会立即卸载可以安全删除的所有卷。 因此，附加到 FAT 卷的任何筛选器都应该在调用筛选器的完成例程之前释放其筛选器设备对象。 NTFS 文件系统不会执行此操作。 因此，附加到 NTFS 卷的筛选器会预计在调用筛选器的完成例程时，其设备对象仍将附加到该卷。

     

-   Irp\_MN\_QUERY 后收到的 Irp\_删除\_设备请求，但在 IRP\_MN 之前\_取消\_删除\_设备或 IRP\_MN\_删除 @no__接收到 t_10_ 设备请求，可以安全地向下传递堆栈（以由存储设备堆栈失败），也可以保留在队列中，直到接收到取消删除或删除设备请求。

-   如果筛选器收到 IRP\_MN\_"取消"\_\_删除该卷的所有打开句柄，以响应 IRP\_MN\_查询\_删除\_设备请求，它可以重新打开句柄。 但是，在完成 IRP 后，筛选器可以在其完成例程中完成此操作。

-   当某个筛选器接收到 IRP\_MN\_删除\_设备请求时，它通常不需要对 IRP 执行任何处理，除非在接收 IRP\_MN\_查询后，该请求在队列中持有了 Irp\_删除\_设备请求。 如果它在队列中持有 Irp，筛选器必须取消对该卷的所有 Irp 的排队，&lt;并在将 IRP 向下传递到堆栈上的下一个较低版本的驱动程序之前&gt;失败&lt;/i&gt; 它们。

-   收到 IRP\_MN\_意外\_删除请求，筛选器应执行以下操作：

    -   关闭卷的所有打开的句柄，因为文件系统无法清理堆栈，直到没有未完成的引用。

    -   如果筛选器在队列中持有 Irp，则它可能会失败或将其沿堆栈向下传递（由存储设备堆栈失败）。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序与给定的 IRP 一起调用[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。 （IRP 显示为*irp*。）驱动程序可以使用 IRP 的下列成员中设置的信息，并使用 IRP 堆栈位置来处理即插即用请求：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
指向[**IO\_状态的指针\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)结构，它接收最终完成状态和有关请求的操作的信息。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
对于 PnP Irp，此指针应为**NULL** 。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
指定 IRP\_MJ\_PNP。

<a href="" id="irpsp--minorfunction"></a>*IrpSp-&gt;MinorFunction*  
下列情况之一：

-   IRP\_MN\_取消\_删除\_设备
-   IRP\_MN\_查询\_删除\_设备
-   IRP\_MN\_删除\_设备
-   IRP\_MN\_启动\_设备
-   IRP\_MN\_意外\_删除

## <a name="see-also"></a>另请参阅


[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状态\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_PNP （WDK 内核引用）** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)

[**IRP\_MN\_取消\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-remove-device)

[**IRP\_MN\_查询\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)

[**IRP\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)

[**IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)

[**IRP\_MN\_意外\_删除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)

 

 






