---
title: IRP_MN_QUERY_DEVICE_RELATIONS
description: PnP 管理器将发送此请求，以确定特定设备之间的关系。
ms.date: 08/12/2017
ms.assetid: 32437c5a-ad92-433c-8255-83775751a44d
keywords:
- IRP_MN_QUERY_DEVICE_RELATIONS 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 6c2452df3c64fc1bdaf3f1aae2765353e28ccd2b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524194"
---
# <a name="irpmnquerydevicerelations"></a>IRP\_MN\_查询\_设备\_关系


PnP 管理器将发送此请求，以确定特定设备之间的关系。 以下类型的驱动程序处理此请求：

-   总线驱动程序必须处理**BusRelations**其适配器或控制器 （总线 FDO） 的请求。 筛选器驱动程序可能会处理**BusRelations**请求。

-   总线驱动程序必须处理**TargetDeviceRelation**其子设备 (子 PDOs) 的请求。

-   函数和筛选器驱动程序可能会处理**RemovalRelations**并**PowerRelations**请求。

-   总线驱动程序可能会处理**EjectionRelations**其子设备 (子 PDOs) 的请求。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md) When Sent
---------

PnP 管理器将发送此 IRP 到指定的设备收集有关具有关系的设备的信息。

PnP 管理器将查询的设备**BusRelations** （子设备） 设备时枚举和在其他时间，同时在设备处于活动状态，例如当驱动程序调用[ **IoInvalidateDeviceRelations** ](https://msdn.microsoft.com/library/windows/hardware/ff549353)例程，以指示子设备已到达或离开。

PnP 管理器将查询的设备**RemovalRelations**它会删除设备的驱动程序之前。 PnP 管理器中查询**RemovalRelations**并**EjectionRelations**弹出设备之前。

PnP 管理器将查询的设备**TargetDeviceRelation**驱动程序或用户模式应用程序时注册的即插即用通知**EventCategoryTargetDeviceChange**在设备上。 对与特定的文件对象相关联的设备的即插即用管理器查询。 **IRP\_MN\_查询\_设备\_关系**是唯一的 PnP IRP 具有有效的文件对象参数。 驱动程序可以查询的设备堆栈**TargetDeviceRelation**。 驱动程序不需要发送时提供一个文件对象及其**TargetDeviceRelation**查询。

PnP 管理器将查询的设备**PowerRelations**当设备的驱动程序调用**IoInvalidateDeviceRelations**指示与此设备有隐式电源的设备组管理关系已更改。 **PowerRelations**从 Windows 7 开始支持请求。

有关**BusRelations**， **RemovalRelations**， **EjectionRelations**，以及**PowerRelations**请求时，即插即用管理器将发送**IRP\_MN\_查询\_设备\_关系**在 IRQL = 被动\_级别在系统线程的上下文中。

有关**TargetDeviceRelation**请求时，即插即用管理器将此 IRP 发送在 IRQL = 被动\_级别在任意线程上下文中。

## <a name="input-parameters"></a>输入参数


**Parameters.QueryDeviceRelations.Type**的成员[ **IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)结构指定的关系类型正在查询的。 可能的值包括**BusRelations**， **EjectionRelations**， **RemovalRelations**， **TargetDeviceRelation**，和**PowerRelations**。

**的文件对象**的当前成员**IO\_堆栈\_位置**结构指向有效的文件对象仅当**Parameters.QueryDeviceRelations.Type**是**TargetDeviceRelation**。

## <a name="output-parameters"></a>输出参数


返回在 I/O 状态块中。

## <a name="io-status-block"></a>I/O 状态块


驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功或失败状态，如状态\_不足\_资源。

如果成功，驱动程序设置**Irp-&gt;IoStatus.Information**到 PDEVICE\_指向请求的关系信息的关系指针。 **设备\_关系**结构定义，如下所示：

```cpp
typedef struct _DEVICE_RELATIONS {
  ULONG  Count;
  PDEVICE_OBJECT  Objects[1];  // variable length
} DEVICE_RELATIONS, *PDEVICE_RELATIONS;
```

<a name="operation"></a>操作
---------

如果驱动程序中对此响应返回的关系**IRP\_MN\_查询\_设备\_关系**，该驱动程序分配**设备\_关系**从包含计数和适当数量的设备对象指针的分页内存的结构。 当不再需要时，即插即用管理器释放结构。 如果驱动程序取代**设备\_关系**结构，该分配的另一个驱动程序、 驱动程序必须释放以前的结构。

驱动程序必须引用的任何设备。 它报告在此 IRP PDO ([**ObReferenceObject**](https://msdn.microsoft.com/library/windows/hardware/ff558678))。 PnP 管理器中移除引用在适当的时候。

函数或筛选器驱动程序应准备好处理此 IRP 设备之后的任何时间及其[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)设备已完成例程。 总线驱动程序应准备好处理的查询**BusRelations**立即枚举设备后。

有关处理的常规规则[即插即用次要 Irp](plug-and-play-minor-irps.md)请参阅[插](https://msdn.microsoft.com/library/windows/hardware/ff547125)。

以下各小节描述了用于处理各种查询的特定操作。

**BusRelations 请求**

当适配器或控制器的总线关系 （子设备） 的即插即用管理器查询，总线驱动程序必须返回的指针的列表到实际存在的任何设备的 PDOs 在总线上。 总线驱动程序将报告所有设备，而不考虑是否启动它们。 总线驱动程序可能需要开启其总线的设备，以确定哪些子活动都存在。

**警告**  的设备对象不能传递给 PDO 将作为参数，直到 PnP 管理器创建一个设备节点的任何例程 (*devnode*) 为该对象。 (如果该驱动程序 pass 设备对象，系统将 bug 与复选[ **Bug 检查位 0xCA:PNP\_已检测\_严重\_错误**](https://msdn.microsoft.com/library/windows/hardware/ff560209)。)PnP 管理器在响应中创建 devnode **IRP\_MN\_查询\_设备\_关系**请求。 该驱动程序可以安全地假定在接收时，已创建的 PDO devnode [ **IRP\_MN\_查询\_资源\_要求**](irp-mn-query-resource-requirements.md)请求。

 

响应此 IRP 的总线驱动程序是总线适配器或控制器功能驱动程序，不是父总线驱动程序的适配器或控制器连接到总线。 函数的非总线设备驱动程序不处理此查询。 此类驱动程序只需将 IRP 传递给下一个较低的驱动程序。 （请参阅下图。）筛选器驱动程序通常不会处理此查询。

在 Windows Vista 和更高版本操作系统上，我们建议，驱动程序始终挂起**IRP\_MN\_查询\_设备\_关系**IRP 并完成其处理更高版本。 此顺序可让系统以进行异步处理总线关系查询。 (在 Windows Vista 之前的操作系统、 驱动程序可以安全返回状态\_PENDING 其调度例程，而即插即用管理器中的不重叠总线关系查询与任何其他操作。)

下图显示了驱动程序如何处理查询的总线关系。

![说明驱动程序处理查询的总线关系的关系图](images/qdrstaks.png)

在图中所示示例中，即插即用管理器将发送**IRP\_MN\_查询\_设备\_关系**有关**BusRelations**的驱动程序USB 集线器设备。 PnP 管理器正在请求的中心设备的子级的列表。

1.  作为与所有 PnP Irp PnP 管理器将发送 IRP 到设备的设备堆栈中的顶部驱动程序。

2.  可选的筛选器驱动程序可能在堆栈中顶部的驱动程序。 筛选器驱动程序通常不会处理此 IRP;它将传递在堆栈的下层 IRP。 筛选器驱动程序可能会处理此 IRP，例如，如果该驱动程序将公开总线上的非可枚举设备。

3.  USB 集线器总线驱动程序处理 IRP。

    USB 集线器总线驱动程序：

    -   创建任何子设备还没有一个的 PDO。

    -   将 PDO 标记不再存在总线上的任何设备处于非活动状态。 总线驱动程序不会删除有关何时删除 PDOs，详细信息，请参阅此类 PDOs.For[删除设备](https://msdn.microsoft.com/library/windows/hardware/ff561046)。

    -   报告在总线存在任何子设备。

        对于每个子设备，总线驱动程序引用 PDO，并将指针放到设备中的 PDO\_关系结构。

        在此示例中有两个 PDOs： 一个用于游戏杆设备，另一个用于键盘设备。

        总线驱动程序应检查是否另一个驱动程序已创建了一个设备\_此 IRP 的关系结构。 如果是这样，总线驱动程序必须将添加到现有的信息。

        如果不存在子设备总线上存在，驱动程序的计数设置为零的设备中\_关系结构，并返回成功。

    -   在 I/O 状态块中设置相应的值并将 IRP 传递给下一个较低的驱动程序。 适配器或控制器的总线驱动程序不会完成 IRP。

4.  可选的低层筛选器，如果存在，通常不处理此 IRP。 这样的筛选器驱动程序将在堆栈的下层 IRP 传递。 如果低筛选器驱动程序处理此 IRP，它可以将 PDO(s) 添加到子设备的列表，但不得删除任何 PDOs 创建的其他驱动程序。

5.  父总线驱动程序不处理此 IRP，除非它是设备堆栈 （设备为 raw 模式） 中的唯一驱动程序。 与所有 PnP Irp，父总线驱动程序完成后使用 IRP [ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)。

    如果设备堆栈中有一个或多个总线筛选器驱动程序，此类驱动程序可能会处理 IRP 手向总线驱动程序和/或 IRP 的方式重新启动设备堆栈上 (如果有[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程）。 根据 PnP IRP 规则，这样的驱动程序可以将 PDOs 添加到堆栈的下层手 IRP 和/或修改 IRP 的方式备份在堆栈上的关系列表 (在*IoCompletion*例程)。

**EjectionRelations 请求**

驱动程序返回 PDOs 可能以物理方式从系统中删除时弹出指定的设备的任何设备的指针。 不报告设备; 子级的 PDOsPnP 管理器始终请求在其父设备之前删除子设备。

PnP 管理器将发送[ **IRP\_MN\_弹出**](irp-mn-eject.md) IRP 正在弹出的设备。 此类设备的驱动程序还会收到删除 IRP。 设备的弹出关系接收[ **IRP\_MN\_删除\_设备**](irp-mn-remove-device.md) IRP (不**IRP\_MN\_弹出**IRP)。

只有一个父总线驱动程序可以响应**EjectionRelations**查询其子设备之一。 函数和筛选器驱动程序必须将其传递给设备堆栈中的下一个较低驱动程序中。 如果总线驱动程序作为其适配器或控制器功能驱动程序收到此 IRP，总线驱动程序执行功能驱动程序的任务，并必须将 IRP 传递给下一个较低的驱动程序。

**PowerRelations 请求**

从 Windows 7 开始**PowerRelations**查询还可实现驱动程序来指定支持即插即用枚举父总线和枚举的子之间的常规关系之外的电源管理关系总线上的设备。 例如，如果总线驱动程序无法枚举在总线上的子设备或设备是多个总线的子级**PowerRelations**查询可以描述使用总线或总线子设备的电源关系。

即插即用 manager 问题**PowerRelations**查询设备的设备驱动程序调用时[ **IoInvalidateDeviceRelations** ](https://msdn.microsoft.com/library/windows/hardware/ff549353)例程，并指定*类型*的参数值**PowerRelations**。

此查询的响应，目标设备 （即查询的目标设备） 的驱动程序提供**设备\_关系**结构，其中包含指向的必须是任何其他设备 PDOs通过电源管理器之前打开目标设备已打开。 相反，这些其他设备必须关闭状态只有在目标设备处于关闭状态后。 电源管理器使用查询中的信息以保证，这些设备开启和关闭以正确的顺序。

这种顺序保证仅适用于全局系统睡眠状态转换，其中包括转换到和从 S1、 S2、 S3 (*睡眠*)，S4 (*休眠*)，和 S5 (*关闭*)系统电源状态。 **PowerRelations**排序保证不适用于如果目标设备或任何其他设备为提供其 PDO **PowerRelations**查询执行从低功耗 Dx 设备之间的转换时系统将保留在 S0 电源状态 (*运行*) 系统状态。

如果目标设备上的特殊文件的设备路径 （如页面文件、 休眠文件或崩溃转储文件），当它处理时，目标设备的驱动程序必须执行附加步骤[ **IRP\_MN\_设备\_使用情况\_通知**](irp-mn-device-usage-notification.md)所在的 IRP **InPath**是**TRUE**。 此驱动程序必须确保的设备为提供其 PDOs **PowerRelations**查询还可以支持在特殊的文件的设备路径。 若要确认是否提供此支持，目标设备的驱动程序必须首先发送**IRP\_MN\_设备\_用法\_通知**IRP 到每个这些设备，且此 IRP 必须指定相同**UsageNotification.Type**作为目标设备。 仅当接收此 IRP 的所有设备都完成 IRP，成功状态代码可以都完成的目标设备的驱动程序及其**IRP\_MN\_设备\_用法\_通知**IRP 成功。 否则，此驱动程序必须完成此 IRP，失败状态代码。

当此相同的驱动程序处理**IRP\_MN\_设备\_用法\_通知**IRP 为其**InPath**是**FALSE**，该驱动程序必须发送**IRP\_MN\_设备\_使用情况\_通知**IRP 到一组相同的哪些中的大小写与依赖于设备**InPath**是**TRUE**。 但是，该驱动程序应永远不会完成此 IRP 失败状态代码何时**InPath**是**FALSE**。

驱动程序用于响应**PowerRelations**查询应注册为提供其 PDOs 的所有设备上的目标设备更改通知**PowerRelations**查询。 若要注册这些通知，该驱动程序可以调用[ **IoRegisterPlugPlayNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff549526)例程，并指定*EventCategory* 的参数值**EventCategoryTargetDeviceChange**。

**RemovalRelations 请求**

驱动程序返回的任何设备中删除指定设备的驱动程序时，必须删除其驱动程序 PDOs 指针。 不报告设备; 子级的 PDOsPnP 管理器已请求删除子设备之前删除设备。

未在其中删除关系会删除的顺序。

设备堆栈中的任何驱动程序可以处理此类型的关系查询。 函数或筛选器驱动程序并向其传递到下一个较低的驱动程序之前处理 IRP。 总线驱动程序处理 IRP，然后将其完成。

**TargetDeviceRelation 请求**

**TargetDeviceRelation**查询还可实现 PnP 管理器中，若要控制硬件即插即用设备堆栈中的 PDO 查询非 PnP 设备堆栈。

一般情况下，驱动程序将转发**IRP\_MN\_查询\_设备\_关系**IRP 下其堆栈直到 IRP 达到特定设备堆栈的底部。 在非 PnP 堆栈的底部的驱动程序，然后转发或重新发出到相关的即插即用堆栈 IRP。 例如，可能会发送 PnP 管理器**TargetDeviceRelation**到文件系统堆栈，这是一个非 PnP 堆栈顶部的设备对象的查询。 文件系统堆栈中的每个设备对象会将查询传递给其下的设备对象，直到查询到达堆栈底部的设备对象。 堆栈中的最低设备对象将转发或重新发布**TargetDeviceRelation**查询到的即插即用的存储卷堆栈顶部的设备对象，然后查询将被传递向下到底部的存储 PDO卷堆栈。

以下列表总结了在其中您可以安全地获取指向的是 PDO 即插即用设备堆栈底部的情况下：

-   中即插即用设备对象

    即插即用设备堆栈中的设备对象了解堆栈的 PDO 时[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)调用例程的设备。 该驱动程序可以安全地缓存 PDO 指向如果与传入正确同步使用指针[ **IRP\_MN\_删除\_设备**](irp-mn-remove-device.md)消息通过使用[删除锁定例程](https://msdn.microsoft.com/library/windows/hardware/ff561042)。

-   非 PnP 堆栈，不是在堆栈的底部中的设备对象

    对于设备对象不在非 PnP 堆栈的底部，驱动程序可以发送**TargetDeviceRelation**查询以获取相应的即插即用设备堆栈底部 PDO 的指针。

-   设备的文件对象

    为设备提供的文件对象，则驱动程序可以调用[ **IoGetRelatedDeviceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff549277)若要获取的设备对象，然后按照前面的列表项中的说明。

-   设备对象的句柄

    提供给设备对象的句柄，则驱动程序可以调用[ **ObReferenceObjectByHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff558679)获取设备的文件对象，并遵循前面的列表项中的说明。

父总线驱动程序必须处理**TargetDeviceRelation**关系查询其子设备。 总线驱动程序引用具有子设备的 PDO [ **ObReferenceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff558678)并返回一个指向 PDO**设备\_关系**结构。 此关系类型的结构中没有只有一个 PDO 指针。 当驱动程序或应用程序中取消注册设备上的通知，即插即用管理器删除对 PDO 的引用。

只有一个父总线驱动程序响应**TargetDeviceRelation**查询。 函数和筛选器驱动程序必须将其传递给设备堆栈中的下一个较低驱动程序中。 如果总线驱动程序作为其适配器或控制器功能驱动程序收到此 IRP，总线驱动程序执行功能驱动程序的任务，并必须将 IRP 传递给下一个较低的驱动程序。

如果驱动程序不是基于 PDO 的堆栈，该驱动程序中发送新的目标的设备的关系查询 IRP 到与该驱动程序在其执行 I/O 的文件句柄关联的设备对象。

**发送此 IRP**

驱动程序不能发送**IRP\_MN\_查询\_设备\_关系**请求**BusRelations**。 驱动程序可以不受限制发送此 IRP **RemovalRelations**或**EjectionRelations**，但它不可能，驱动程序将执行此操作。

驱动程序可以查询的设备堆栈**TargetDeviceRelation**。 请参阅[处理 Irp](https://msdn.microsoft.com/library/windows/hardware/ff546847)有关发送 Irp 信息。 专门针对此 IRP 可以采用以下步骤：

-   IRP 的下一步 I/O 堆栈位置中设置的值： 设置**MajorFunction**到[ **IRP\_MJ\_PNP**](irp-mj-pnp.md)，将**MinorFunction**到**IRP\_MN\_查询\_设备\_关系**，将**Parameters.QueryDeviceRelations.Type**到**TargetDeviceRelation**，并设置**Irp-&gt;的文件对象**到有效的文件对象。

-   初始化**IoStatus.Status**于状态\_不\_受支持。

如果驱动程序发送到响应中获取报表 PDO 此 IRP **IRP\_MN\_查询\_设备\_关系**有关**TargetDeviceRelation**接收，驱动程序然后驱动程序报告 PDO 和 IRP 完成时释放返回的关系结构。 如果驱动程序的另一个原因发起此 IRP，当 IRP 完成后将不再需要时取消引用 PDO 驱动程序将释放关系结构。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wdm.h 中 （包括 wdm.h 中、 Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[*AddDevice*](https://msdn.microsoft.com/library/windows/hardware/ff540521)

[**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)

[**IoGetRelatedDeviceObject**](https://msdn.microsoft.com/library/windows/hardware/ff549277)

[**IoInvalidateDeviceRelations**](https://msdn.microsoft.com/library/windows/hardware/ff549353)

[**IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526)

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

[**IRP\_MN\_DEVICE\_USAGE\_NOTIFICATION**](irp-mn-device-usage-notification.md)

[**IRP\_MN\_EJECT**](irp-mn-eject.md)

[**IRP\_MN\_查询\_资源\_要求**](irp-mn-query-resource-requirements.md)

[**IRP\_MN\_REMOVE\_DEVICE**](irp-mn-remove-device.md)

[**IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**ObReferenceObject**](https://msdn.microsoft.com/library/windows/hardware/ff558678)

[**ObReferenceObjectByHandle**](https://msdn.microsoft.com/library/windows/hardware/ff558679)

 

 




