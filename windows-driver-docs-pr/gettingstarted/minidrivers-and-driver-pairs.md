---
title: 微型驱动程序、微型端口驱动程序和驱动程序对
description: 微型驱动程序或微型端口驱动程序可以用作半个驱动程序对。
ms.assetid: 33387A72-5278-4637-AED4-C010E4C1616B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 049d302fc49376d4f22b44fc709773dc93578781
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "63371308"
---
# <a name="minidrivers-miniport-drivers-and-driver-pairs"></a>微型驱动程序、微型端口驱动程序和驱动程序对


微型驱动程序或微型端口驱动程序可以用作半个驱动程序对。 诸如（微型端口、端口）的驱动程序对可以简化驱动程序开发。 在驱动程序对中，一个驱动程序处理整个设备集合共同的常规任务，而另一个驱动程序处理特定于单个设备的任务。 处理设备特定任务的驱动程序有多个名称，包括微型端口驱动程序、微型类驱动程序和微型驱动程序。

Microsoft 提供一般驱动程序，而独立的硬件供应商通常提供特定驱动程序。 在阅读本主题之前，应了解[设备节点和设备堆栈](device-nodes-and-device-stacks.md)和 [I/O 请求数据包](i-o-request-packets.md)中介绍的理念。

每个内核模式驱动程序都必须实现名为 [**DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff544113) 的函数，该函数在加载驱动程序之后会立即得到调用。 **DriverEntry** 函数使用指向驱动程序实现的一些其他函数的指针来填充 [**DRIVER\_OBJECT**](https://msdn.microsoft.com/library/windows/hardware/ff544174) 结构的某些成员。 例如，**DriverEntry** 函数使用指向驱动程序的 [*Unload*](https://msdn.microsoft.com/library/windows/hardware/ff564886) 函数的指针来填充 **DRIVER\_OBJECT** 结构的 **Unload** 成员，如下图所示。

![显示 driver\-object 结构和 Unload 成员的图](images/driverfunctionpointers02.png)

[**DRIVER\_OBJECT**](https://msdn.microsoft.com/library/windows/hardware/ff544174) 结构的 **MajorFunction** 成员为指向函数的大量指针，这些函数处理 I/O 请求数据包 ([**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694))，如下图所示。 通常，驱动程序使用指向函数（由驱动程序实现）的指针来填充 **MajorFunction** 数组的多个成员，这些函数处理各种 IRP。

![显示 driver\-object 结构和 MajorFunction 成员的图](images/driverfunctionpointers03.png)

可以根据 IRP 的主要函数代码对 IRP 进行分类，该代码由常量标识，例如 **IRP\_MJ\_READ**、**IRP\_MJ\_WRITE** 或 **IRP\_MJ\_PNP**。 标识主要函数代码的常量用作 **MajorFunction** 数组中的索引。 例如，假设驱动程序实现调度函数以处理具有主要函数代码 **IRP\_MJ\_WRITE** 的 IRP。 在这种情形下，驱动程序必须使用指向调度函数的指针来填充数组的 **MajorFunction**\[IRP\_MJ\_WRITE\] 元素。

通常，驱动程序填充 **MajorFunction** 数组的某些元素并使剩下的元素设置为 I/O 管理器提供的默认值。 以下示例说明了如何使用 [ **!drvobj**](https://msdn.microsoft.com/library/windows/hardware/ff562408) 调试程序扩展来检查用于 parport 驱动程序的函数指针。

``` syntax
0: kd> !drvobj parport 2
Driver object (fffffa80048d9e70) is for:
 \Driver\Parport
DriverEntry:   fffff880065ea070 parport!GsDriverEntry
DriverStartIo: 00000000 
DriverUnload:  fffff880065e131c parport!PptUnload
AddDevice:     fffff880065d2008 parport!P5AddDevice

Dispatch routines:
[00] IRP_MJ_CREATE                      fffff880065d49d0    parport!PptDispatchCreateOpen
[01] IRP_MJ_CREATE_NAMED_PIPE           fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[02] IRP_MJ_CLOSE                       fffff880065d4a78    parport!PptDispatchClose
[03] IRP_MJ_READ                        fffff880065d4bac    parport!PptDispatchRead
[04] IRP_MJ_WRITE                       fffff880065d4bac    parport!PptDispatchRead
[05] IRP_MJ_QUERY_INFORMATION           fffff880065d4c40    parport!PptDispatchQueryInformation
[06] IRP_MJ_SET_INFORMATION             fffff880065d4ce4    parport!PptDispatchSetInformation
[07] IRP_MJ_QUERY_EA                    fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[08] IRP_MJ_SET_EA                      fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[09] IRP_MJ_FLUSH_BUFFERS               fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[0a] IRP_MJ_QUERY_VOLUME_INFORMATION    fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[0b] IRP_MJ_SET_VOLUME_INFORMATION      fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[0c] IRP_MJ_DIRECTORY_CONTROL           fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[0d] IRP_MJ_FILE_SYSTEM_CONTROL         fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[0e] IRP_MJ_DEVICE_CONTROL              fffff880065d4be8    parport!PptDispatchDeviceControl
[0f] IRP_MJ_INTERNAL_DEVICE_CONTROL     fffff880065d4c24    parport!PptDispatchInternalDeviceControl
[10] IRP_MJ_SHUTDOWN                    fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[11] IRP_MJ_LOCK_CONTROL                fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[12] IRP_MJ_CLEANUP                     fffff880065d4af4    parport!PptDispatchCleanup
[13] IRP_MJ_CREATE_MAILSLOT             fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[14] IRP_MJ_QUERY_SECURITY              fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[15] IRP_MJ_SET_SECURITY                fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[16] IRP_MJ_POWER                       fffff880065d491c    parport!PptDispatchPower
[17] IRP_MJ_SYSTEM_CONTROL              fffff880065d4d4c    parport!PptDispatchSystemControl
[18] IRP_MJ_DEVICE_CHANGE               fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[19] IRP_MJ_QUERY_QUOTA                 fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[1a] IRP_MJ_SET_QUOTA                   fffff80001b6ecd4    nt!IopInvalidDeviceRequest
[1b] IRP_MJ_PNP                         fffff880065d4840    parport!PptDispatchPnp
```

在调试程序输出中，可以看到 parport.sys 实现 **GsDriverEntry**，驱动程序的入口点。 **GsDriverEntry**（在生成驱动程序时自动生成）执行一些初始化，然后调用 [**DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff544113)（由驱动程序开发人员实现）。

还可以看到 parport 驱动程序（位于其 [**DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff544113) 函数中）为指向调度函数的指针提供了以下主要函数代码：

-   IRP\_MJ\_CREATE
-   IRP\_MJ\_CLOSE
-   IRP\_MJ\_READ
-   IRP\_MJ\_WRITE
-   IRP\_MJ\_QUERY\_INFORMATION
-   IRP\_MJ\_SET\_INFORMATION
-   IRP\_MJ\_DEVICE\_CONTROL
-   IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL
-   IRP\_MJ\_CLEANUP
-   IRP\_MJ\_POWER
-   IRP\_MJ\_SYSTEM\_CONTROL
-   IRP\_MJ\_PNP

**MajorFunction** 数组的其余元素包含指向默认调度函数 **nt!IopInvalidDeviceRequest** 的指针。

在调试程序输出中，可以看到 parport 驱动程序提供了用于 [*Unload*](https://msdn.microsoft.com/library/windows/hardware/ff564886) 和 [*AddDevice*](https://msdn.microsoft.com/library/windows/hardware/ff540521) 的函数指针，但未提供用于 [*StartIo*](https://msdn.microsoft.com/library/windows/hardware/ff563858) 的函数指针。 *AddDevice* 函数很独特，原因是其函数指针未存储在 [**DRIVER\_OBJECT**](https://msdn.microsoft.com/library/windows/hardware/ff544174) 结构中， 而是存储在 **DRIVER\_OBJECT** 结构扩展的 **AddDevice** 成员中。 下图说明了 parport 驱动程序在其 [**DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff544113) 函数中提供的函数指针。 parport 提供的函数指针被阴影遮蔽。

![图：driver\-object 结构中的函数指针](images/driverfunctionpointers01.png)

## <a name="span-idmakingiteasierbyusingdriverpairsspanspan-idmakingiteasierbyusingdriverpairsspanspan-idmakingiteasierbyusingdriverpairsspanmaking-it-easier-by-using-driver-pairs"></a><span id="Making_it_easier_by_using_driver_pairs"></span><span id="making_it_easier_by_using_driver_pairs"></span><span id="MAKING_IT_EASIER_BY_USING_DRIVER_PAIRS"></span>使用驱动程序对使其更轻松


在一段时间内，当驱动程序开发者身处 Microsoft 获取的 Windows 驱动程序模型 (WDM) 体验内外时，他们意识到有关调度函数的一些事项：

-   调度函数很大程度上为样本。 例如，用于 IRP\_MJ\_PNP 的调度函数中的很多代码对于所有驱动程序而言相同。 它仅为即插即用 (PnP) 代码的一小部分，该代码特定于单个驱动程序，该驱动程序控制硬件的单个部分。
-   调度函数比较复杂且难以用对。 实现功能（如线程同步、IRP 排队以及 IRP 取消）具有挑战性，需要对操作系统的工作原理有着较深的了解。

为了使驱动程序开发者更轻松，Microsoft 创建了多个技术特定的驱动程序模型。 初看之下，技术特定模型似乎彼此差异很大，但细看之后会发现多个模型都基于此范例：

-   驱动程序拆分为两个部分：一部分负责通用处理，另一部分负责特定于特殊设备的处理。
-   通用部分由 Microsoft 编写。
-   特定部分由 Microsoft 或独立硬件供应商编写。

假设 Proseware 和 Contoso 公司生产的机器人玩具都需要使用 WDM 驱动程序。 另假设 Microsoft 提供了名为 GeneralRobot.sys 的通用机器人驱动程序。 Proseware 和 Contoso 各自都可以编写小的驱动程序，用于处理其特定机器人的需求。 例如，Proseware 可以编写 ProsewareRobot.sys，驱动程序对（ProsewareRobot.sys、GeneralRobot.sys）可以合并形成单个的 WDM 驱动程序。 同样，驱动程序对（ContosoRobot.sys、GeneralRobot.sys）可以合并形成单个的 WDM 驱动程序。 在大部分的通用形式中，理念是可以使用（specific.sys、general.sys）对来创建驱动程序。

## <a name="span-idfunctionpointersindriverpairsspanspan-idfunctionpointersindriverpairsspanspan-idfunctionpointersindriverpairsspanfunction-pointers-in-driver-pairs"></a><span id="Function_pointers_in_driver_pairs"></span><span id="function_pointers_in_driver_pairs"></span><span id="FUNCTION_POINTERS_IN_DRIVER_PAIRS"></span>驱动程序对中的函数指针


在（specific.sys、general.sys）对中，Windows 会加载 specific.sys 并调用其 [**DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff544113) 函数。 specific.sys 的 **DriverEntry** 函数会收到指向 [**DRIVER\_OBJECT**](https://msdn.microsoft.com/library/windows/hardware/ff544174) 结构的指针。 正常情况下，你期望 **DriverEntry** 使用指向调度函数的指针来填充 **MajorFunction** 数组的多个元素。 你还期望 **DriverEntry** 填充 **DRIVER\_OBJECT** 结构的 **Unload** 成员（和可能的 **StartIo** 成员）和驱动程序对象扩展的 **AddDevice** 成员。 但是，在驱动程序对模型中，**DriverEntry** 不需这样做， 只需通过 specific.sys 的 **DriverEntry** 函数将 **DRIVER\_OBJECT** 结构传递至 general.sys 实现的初始化函数即可。 以下代码示例说明了在（ProsewareRobot.sys、GeneralRobot.sys）对中如何调用初始化函数。

```ManagedCPlusPlus
PVOID g_ProsewareRobottCallbacks[3] = {DeviceControlCallback, PnpCallback, PowerCallback};

// DriverEntry function in ProsewareRobot.sys
NTSTATUS DriverEntry (DRIVER_OBJECT *DriverObject, PUNICODE_STRING RegistryPath)
{
   // Call the initialization function implemented by GeneralRobot.sys.
   return GeneralRobotInit(DriverObject, RegistryPath, g_ProsewareRobottCallbacks);
}
```

GeneralRobot.sys 中的初始化函数编写指向 [**DRIVER\_OBJECT**](https://msdn.microsoft.com/library/windows/hardware/ff544174) 结构（及其扩展）的相应成员和 **MajorFunction** 数组的相应元素的函数指针。 理念为当 I/O 管理器将 IRP 发送至驱动程序对时，IRP 首先转至由 GeneralRobot.sys 实现的调度函数。 如果 GeneralRobot.sys 可以自行处理 IRP，则无需涉及到特定驱动程序 ProsewareRobot.sys。 如果 GeneralRobot.sys 可以处理部分但不是全部的 IRP 处理，则它会从由 ProsewareRobot.sys 实现的回调函数之一获取帮助。 GeneralRobot.sys 接收指向 GeneralRobotInit 调用中 ProsewareRobot 回调的指针。

在 [**DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff544113) 返回的某个点，会构造用于 Proseware Robot 设备节点的设备堆栈。 设备堆栈可能如下所示。

![图：Proseware Robot 设备节点，显示设备堆栈中的三个设备对象：afterthought.sys (filter do)、prosewarerobot.sys、generalrobot.sys (FDO) 以及 pci.sys (PDO)](images/driverpairs01.png)

如上图所示，Proseware Robot 的设备堆栈有三个设备对象。 顶部设备对象为与筛选器驱动程序 AfterThought.sys 关联的筛选器设备对象（筛选器 DO）。 中间设备对象为与驱动程序对（ProsewareRobot.sys、GeneralRobot.sys）关联的功能设备对象 (FDO)。 驱动程序对用作设备堆栈的函数驱动程序。 底部设备对象为与 Pci.sys 关联的物理设备对象 (PDO)。

注意，驱动程序对仅占用设备堆栈中的一层并且仅与一个设备对象关联：FDO。 当 GeneralRobot.sys 处理 IRP 时，它可能会调用 ProsewareRobot.sys 以获取帮助，但这不同于沿着设备堆栈向下传递请求。 驱动程序对形成单个的 WDM 驱动程序，该驱动程序位于设备堆栈中的一层。 驱动程序对完成 IRP 或沿着设备堆栈向下传递 IRP 至与 Pci.sys 关联的 PDO。

## <a name="span-idexampleofadriverpairspanspan-idexampleofadriverpairspanspan-idexampleofadriverpairspanexample-of-a-driver-pair"></a><span id="Example_of_a_driver_pair"></span><span id="example_of_a_driver_pair"></span><span id="EXAMPLE_OF_A_DRIVER_PAIR"></span>驱动程序对示例


假设笔记本电脑中有无线网卡，并且通过在“设备管理器”中查找，你确定 netwlv64.sys 为网卡驱动程序。 可以使用 [ **!drvobj**](https://msdn.microsoft.com/library/windows/hardware/ff562408) 调试程序扩展来检查用于 netwlv64.sys 的函数指针。

``` syntax
1: kd> !drvobj netwlv64 2
Driver object (fffffa8002e5f420) is for:
 \Driver\netwlv64
DriverEntry:   fffff8800482f064 netwlv64!GsDriverEntry
DriverStartIo: 00000000 
DriverUnload:  fffff8800195c5f4 ndis!ndisMUnloadEx
AddDevice:     fffff88001940d30 ndis!ndisPnPAddDevice
Dispatch routines:
[00] IRP_MJ_CREATE                      fffff880018b5530 ndis!ndisCreateIrpHandler
[01] IRP_MJ_CREATE_NAMED_PIPE           fffff88001936f00 ndis!ndisDummyIrpHandler
[02] IRP_MJ_CLOSE                       fffff880018b5870 ndis!ndisCloseIrpHandler
[03] IRP_MJ_READ                        fffff88001936f00 ndis!ndisDummyIrpHandler
[04] IRP_MJ_WRITE                       fffff88001936f00 ndis!ndisDummyIrpHandler
[05] IRP_MJ_QUERY_INFORMATION           fffff88001936f00 ndis!ndisDummyIrpHandler
[06] IRP_MJ_SET_INFORMATION             fffff88001936f00 ndis!ndisDummyIrpHandler
[07] IRP_MJ_QUERY_EA                    fffff88001936f00 ndis!ndisDummyIrpHandler
[08] IRP_MJ_SET_EA                      fffff88001936f00 ndis!ndisDummyIrpHandler
[09] IRP_MJ_FLUSH_BUFFERS               fffff88001936f00 ndis!ndisDummyIrpHandler
[0a] IRP_MJ_QUERY_VOLUME_INFORMATION    fffff88001936f00 ndis!ndisDummyIrpHandler
[0b] IRP_MJ_SET_VOLUME_INFORMATION      fffff88001936f00 ndis!ndisDummyIrpHandler
[0c] IRP_MJ_DIRECTORY_CONTROL           fffff88001936f00 ndis!ndisDummyIrpHandler
[0d] IRP_MJ_FILE_SYSTEM_CONTROL         fffff88001936f00 ndis!ndisDummyIrpHandler
[0e] IRP_MJ_DEVICE_CONTROL              fffff8800193696c ndis!ndisDeviceControlIrpHandler
[0f] IRP_MJ_INTERNAL_DEVICE_CONTROL     fffff880018f9114 ndis!ndisDeviceInternalIrpDispatch
[10] IRP_MJ_SHUTDOWN                    fffff88001936f00 ndis!ndisDummyIrpHandler
[11] IRP_MJ_LOCK_CONTROL                fffff88001936f00 ndis!ndisDummyIrpHandler
[12] IRP_MJ_CLEANUP                     fffff88001936f00 ndis!ndisDummyIrpHandler
[13] IRP_MJ_CREATE_MAILSLOT             fffff88001936f00 ndis!ndisDummyIrpHandler
[14] IRP_MJ_QUERY_SECURITY              fffff88001936f00 ndis!ndisDummyIrpHandler
[15] IRP_MJ_SET_SECURITY                fffff88001936f00 ndis!ndisDummyIrpHandler
[16] IRP_MJ_POWER                       fffff880018c35e8 ndis!ndisPowerDispatch
[17] IRP_MJ_SYSTEM_CONTROL              fffff880019392c8 ndis!ndisWMIDispatch
[18] IRP_MJ_DEVICE_CHANGE               fffff88001936f00 ndis!ndisDummyIrpHandler
[19] IRP_MJ_QUERY_QUOTA                 fffff88001936f00 ndis!ndisDummyIrpHandler
[1a] IRP_MJ_SET_QUOTA                   fffff88001936f00 ndis!ndisDummyIrpHandler
[1b] IRP_MJ_PNP                         fffff8800193e518 ndis!ndisPnPDispatch
```

在调试程序输出中，可以看到 netwlv64.sys 实现 **GsDriverEntry**，驱动程序的入口点。 **GsDriverEntry**（在生成驱动程序时自动生成）执行一些初始化，然后调用 [**DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff544113)（由驱动程序开发人员编写）。

在本示例中，netwlv64.sys 实现 [**DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff544113)，但 ndis.sys 实现 [*AddDevice*](https://msdn.microsoft.com/library/windows/hardware/ff540521)、[*Unload*](https://msdn.microsoft.com/library/windows/hardware/ff564886) 以及多个调度函数。 Netwlv64.sys 称为 NDIS 微型端口驱动程序，ndis.sys 称为 NDIS 库。 两个模块共同形成（NDIS 微型端口、NDIS 库）对。

此图表示无线网卡的设备堆栈。 注意，驱动程序对（netwlv64.sys、ndis.sys）仅占用设备堆栈中的一层并且仅与一个设备对象关联：FDO。

![图：无线网卡设备堆栈，显示 netwlv64.sys、作为与 FDO 关联的驱动程序对的 ndis.sys 以及与 PDO 关联的 pci.sys ](images/driverpairs02a.png)

## <a name="span-idavailabledriverpairsspanspan-idavailabledriverpairsspanspan-idavailabledriverpairsspanavailable-driver-pairs"></a><span id="Available_driver_pairs"></span><span id="available_driver_pairs"></span><span id="AVAILABLE_DRIVER_PAIRS"></span>可用驱动程序对


不同技术特定的驱动程序模型将大量名称用于驱动程序对的特定部分和通用部分。 在很多情形下，对的特定部分都有前缀“微型”。 以下是可用的一些（特定、通用）对：

-   （屏幕微型端口驱动程序，屏幕端口驱动程序）
-   （音频微型端口驱动程序、音频端口驱动程序）
-   （存储微型端口驱动程序，存储端口驱动程序）
-   （电池微型类驱动程序，电池类驱动程序）
-   （HID 微型驱动程序，HID 类驱动程序）
-   （转换器微型类驱动程序、转换器端口驱动程序）
-   （NDIS 微型端口驱动程序、NDIS 库）

**注意**  正如你在列表中看到的一样，多个模型将术语“类驱动程序”  用作驱动程序对的通用部分。 此种类驱动程序不同于独立类驱动程序，也不同于类筛选器驱动程序。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[适用于所有驱动程序开发人员的概念](concepts-and-knowledge-for-all-driver-developers.md)

[设备节点和设备堆栈](device-nodes-and-device-stacks.md)

[驱动程序堆栈](driver-stacks.md)

 

 






