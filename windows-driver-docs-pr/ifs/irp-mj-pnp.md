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
ms.openlocfilehash: 4ecc03dacfa436a958c8eeda4e360a64cfef8d97
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545371"
---
# <a name="irpmjpnp"></a>IRP\_MJ\_PNP


## <a name="when-sent"></a>发送时间


插 Manager 发送 IRP\_MJ\_每当插活动发生在系统上的即插即用请求。 其他操作系统组件，以及其他内核模式驱动程序，还可以发送某些 IRP\_MJ\_即插即用的请求，具体取决于次要函数代码。

驱动程序的即插即用和播放 IRP 处理要求的详细信息，请参阅[插](https://msdn.microsoft.com/library/windows/hardware/ff547125)。

有关参考信息 IRP\_MJ\_PNP 次要函数代码，请参阅[即插即用和播放次要 Irp](https://msdn.microsoft.com/library/windows/hardware/ff558807)。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统应检查次要函数代码，以确定请求的操作。 文件系统必须处理以下次要函数代码：

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
<td align="left"><p>指示以前的查询删除设备请求已取消。 此请求发送警报的文件系统，以防它需要执行任何取消操作相关的清理。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_REMOVE_DEVICE</p></td>
<td align="left"><p>指示要删除设备。 如果在设备上装载文件系统后，即插即用管理器将此请求发送到文件系统和任何文件系统筛选器。 如果有打开的句柄到设备，文件系统通常会失败的查询删除请求。 如果不是，文件系统通常锁定以防止将来的卷创建成功的请求。 如果已装载的文件系统不支持查询和删除请求，即插即用管理器进行故障设备的查询删除请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_REMOVE_DEVICE</p></td>
<td align="left"><p>指示要删除设备。 如果在设备上装载文件系统后，即插即用管理器将发送此 IRP 到文件系统和任何文件系统筛选器。 文件系统应立即将此 IRP 传递给设备，设置文件系统然后卸除卷完成例程的存储驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_START_DEVICE</p></td>
<td align="left"><p>指示正在启动设备。 文件系统应将此 IRP 传递给设备的存储驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_SURPRISE_REMOVAL</p></td>
<td align="left"><p>指示设备已删除。 如果在设备上已装载文件系统，即插即用管理器将发送此 IRP 到文件系统和任何文件系统筛选器。 文件系统应立即将此 IRP 传递给设备，设置文件系统然后卸除卷完成例程的存储驱动程序。</p></td>
</tr>
</tbody>
</table>

 

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


文件系统筛选器驱动程序应处理 PnP Irp，按照以下原则：

-   当卷要适当地删除用户时，即插即用管理器将发送 IRP\_MN\_查询\_删除\_设备的请求。 在接收到此 IRP，筛选器必须关闭卷上所有打开的句柄并传递到下一步低驱动程序 IRP 堆栈上。 这一点非常重要。 如果该驱动程序无法关闭所有打开的句柄，这样可以防止中卸除，这反过来会阻止物理设备正在弹出的卷。

    &gt; \[!请注意\]&gt;在接收 IRP\_MN\_查询\_删除\_设备请求，FAT 文件系统就会立即卸载它可以安全地删除的所有卷。 因此附加到 FAT 卷的任何筛选器应调用的筛选器完成例程之前，将释放其筛选设备对象。 NTFS 文件系统不会执行此操作。 因此筛选器附加到 NTFS 卷可能会将调用筛选器完成例程时，其设备对象仍将附加到该卷。

     

-   IRP 后未收到的 Irp\_MN\_查询\_删除\_设备请求，但之前 IRP\_MN\_取消\_删除\_设备或 IRP\_MN\_删除\_或设备请求收到，可以安全地传递堆栈 （以存储设备堆栈的失败） 或取消按钮删除之前保留在队列中收到删除设备的请求。

-   如果筛选器接收 IRP\_MN\_取消\_删除\_设备请求后它已关闭所有打开的句柄，以响应 IRP 卷\_MN\_查询\_删除\_设备请求，它可以重新打开句柄。 但是，筛选器可以仅执行此操作在其完成例程中，通过它下面堆栈中的驱动程序已成功完成 IRP 后。

-   当筛选器收到 IRP\_MN\_删除\_设备请求，它通常不需要执行任何处理 IRP，除非它具有已持有 Irp 队列中接收 IRP 以来\_MN\_查询\_删除\_设备的请求。 如果它在队列中持有 Irp，筛选器必须取消排队所有卷的 Irp 和&lt;我&gt;失败&lt;/i&gt;它们之前将向下一步低驱动程序 IRP 传递到堆栈上。

-   在接收 IRP\_MN\_惊讶\_删除请求，该筛选器应执行以下操作：

    -   关闭所有打开的句柄到卷，因为文件系统无法清理堆栈，直到没有任何未完成的引用。

    -   如果筛选器在队列中持有 Irp，它可以对其进行故障，或将其传递堆栈 （用于存储设备堆栈的失败）。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序调用[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)与给定 IRP，若要获取一个指向其自己[**堆栈位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)中，在以下列表中所示*IrpSp*。 (显示为 IRP *Irp*。)该驱动程序可以使用以下成员的 IRP 和 IRP 堆栈位置中处理插请求中设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象指针。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
指向[ **IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)接收最终完成状态以及有关请求的操作信息的结构。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
此指针应**NULL** PnP Irp 的。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
指定 IRP\_MJ\_PNP。

<a href="" id="irpsp--minorfunction"></a>*IrpSp-&gt;MinorFunction*  
下列情况之一：

-   IRP\_MN\_CANCEL\_REMOVE\_DEVICE
-   IRP\_MN\_查询\_删除\_设备
-   IRP\_MN\_REMOVE\_DEVICE
-   IRP\_MN\_START\_DEVICE
-   IRP\_MN\_SURPRISE\_REMOVAL

## <a name="see-also"></a>另请参阅


[**IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_PNP （WDK 内核参考）**](https://msdn.microsoft.com/library/windows/hardware/ff550772)

[**IRP\_MN\_CANCEL\_REMOVE\_DEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff550823)

[**IRP\_MN\_查询\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551705)

[**IRP\_MN\_REMOVE\_DEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff551738)

[**IRP\_MN\_START\_DEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff551749)

[**IRP\_MN\_SURPRISE\_REMOVAL**](https://msdn.microsoft.com/library/windows/hardware/ff551760)

 

 






