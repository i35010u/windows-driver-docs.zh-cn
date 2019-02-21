---
title: 动态枚举
description: 动态枚举
ms.assetid: 6e46b456-7d2d-4c6e-8692-7f310366387d
keywords:
- 动态枚举 WDK KMDF
- 子说明 WDK KMDF
- 地址说明 WDK KMDF
- 标识说明 WDK KMDF
- 动态子列出 WDK KMDF
- 遍历动态子列出 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fa6659f7cac4e5bd15aa28a1d7cdc07a47c3792
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541673"
---
# <a name="dynamic-enumeration"></a>动态枚举


*动态枚举*是检测和更改报告给的数量和类型的系统运行时连接到系统的设备驱动程序的能力。

如果的数量或连接到父设备的设备的类型取决于系统的配置，总线驱动程序必须使用动态枚举。 这些设备的一些可能始终连接到系统，以及一些可能已插入和拔出系统运行时。

例如的数量和类型的插入到系统的 PCI 总线的设备是依赖于系统的但它们是永久的除非用户关闭电源、 打开这种情况，并添加或删除设备时使用螺丝刀。 但是，用户可以添加或删除 USB 设备插入或拔出电缆系统运行时。

### <a name="dynamic-child-lists"></a>动态子列表

该框架支持驱动程序以支持动态枚举通过提供框架子列表对象。 子列表的每个对象表示的子设备连接到父设备的列表。 父设备的总线驱动程序必须标识父级的子设备、 将它们添加到父设备的子列表中，并为每个子级创建的物理设备对象 (PDO)。

驱动程序创建 framework 设备对象表示一台设备，FDO 每次框架将创建一个空、 为设备的默认子列表。 您的驱动程序可以通过调用获取设备的默认子列表的句柄[ **WdfFdoGetDefaultChildList**](https://msdn.microsoft.com/library/windows/hardware/ff547235)。 通常情况下，如果你正在编写枚举设备的子级的总线驱动程序，您的驱动程序可以将子级添加到默认子列表。 如果需要创建其他子列表，可以调用您的驱动程序[ **WdfChildListCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545615)。

驱动程序可以使用子列表之前，它必须配置的子列表对象初始化[ **WDF\_子\_列表\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551227)结构和传递为结构[ **WdfFdoInitSetDefaultChildListConfig**](https://msdn.microsoft.com/library/windows/hardware/ff547258)，默认子列表中，或为[ **WdfChildListCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545615)，其他子列表。

### <a name="dynamic-child-descriptions"></a>动态子说明

每次总线驱动程序标识子设备，它必须将子设备的说明添加到子列表。 一个*子描述*由必需*标识说明*和可选*解决说明*。

<a href="" id="identification-description"></a>*标识说明*  
标识描述是一种结构，其中包含唯一标识该驱动程序枚举每个设备的信息。 该驱动程序定义了此结构，但其第一个成员必须是[ **WDF\_子\_标识\_说明\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff551223)结构。

通常情况下，标识说明包含的设备[设备标识字符串](https://msdn.microsoft.com/library/windows/hardware/ff541224)，可能是一个序列号和总线，如槽号上的设备的位置信息。

该驱动程序可以提供以下一组回调函数，这样的框架来操作中的标识描述的信息：

-   [*EvtChildListIdentificationDescriptionCompare*](https://msdn.microsoft.com/library/windows/hardware/ff540833)，这比较两个标识描述结构的内容。

-   [*EvtChildListIdentificationDescriptionCopy*](https://msdn.microsoft.com/library/windows/hardware/ff540834)，其中一个标识描述结构的内容复制到另一个。

-   [*EvtChildListIdentificationDescriptionDuplicate*](https://msdn.microsoft.com/library/windows/hardware/ff540836)，其创建新标识说明通过复制现有标识描述结构，并根据需要分配额外的缓冲区。

-   [*EvtChildListIdentificationDescriptionCleanup*](https://msdn.microsoft.com/library/windows/hardware/ff540832)，这将释放所分配的缓冲区[ *EvtChildListIdentificationDescriptionDuplicate* ](https://msdn.microsoft.com/library/windows/hardware/ff540836)回调函数。

通常情况下，需要提供这些回调函数，如果您的驱动程序的标识描述结构包含动态分配的缓冲区的指针。 有关这些回调函数的用途的详细信息，请参阅其参考页。

<a href="" id="address-description"></a>*地址说明*  
地址描述是一种结构，其中包含驱动程序要求，以便它可以访问其总线上的设备，如果在插入设备时，可以更改信息的信息。 该驱动程序定义了此结构，但其第一个成员必须是[ **WDF\_子\_地址\_说明\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff551219)结构。

地址说明是可选的。 如果设备的地址信息不能更改在插入设备的时间被拔出的时间之间，可以标识说明中存储的所有设备的地址信息。 例如，USB 控制器将地址分配给设备时设备都插入，并且这些地址不会更改。

但是，某些总线使用可以更改的寻址信息。 例如，IEEE 1394 总线使用"生成计数，"总线重置所做的数。 IEEE 1394 设备的每个异步 I/O 请求必须包括生成计数。 可以更改此地址信息，因为您的驱动程序必须将其存储在地址描述。

该驱动程序可以提供以下一组回调函数来操作中的地址描述的信息：

-   [*EvtChildListAddressDescriptionCopy*](https://msdn.microsoft.com/library/windows/hardware/ff540824)，其中一个地址描述结构的内容复制到另一个。

-   [*EvtChildListAddressDescriptionDuplicate*](https://msdn.microsoft.com/library/windows/hardware/ff540826)，其创建新地址说明通过复制现有地址描述结构，并根据需要分配额外的缓冲区。

-   [*EvtChildListAddressDescriptionCleanup*](https://msdn.microsoft.com/library/windows/hardware/ff540823)，这将释放所分配的缓冲区[ *EvtChildListAddressDescriptionDuplicate* ](https://msdn.microsoft.com/library/windows/hardware/ff540826)回调函数.

通常情况下，需要提供这些回调函数，如果您的驱动程序的地址描述结构包含动态分配的缓冲区的指针。 有关这些回调函数的用途的详细信息，请参阅其参考页。

### <a name="adding-devices-to-a-dynamic-child-list"></a>将设备添加到动态子列表

当框架将调用总线驱动程序[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调函数，必须调用的回调函数[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)若要创建 FDO 父设备，这通常是总线适配器。 有关创建 FDO 的详细信息，请参阅[功能驱动程序中创建设备对象](creating-device-objects-in-a-function-driver.md)。 然后，驱动程序必须枚举父设备的子级，并将子项添加到子列表。

（可选） 该驱动程序可以调用[ **WdfDeviceSetBusInformationForChildren** ](https://msdn.microsoft.com/library/windows/hardware/ff546868)框架向提供关于总线的信息。 建议执行此操作，因为这样可以更轻松子设备和应用来标识在总线。

若要将子项添加到子列表中，该驱动程序必须调用[ **WdfChildListAddOrUpdateChildDescriptionAsPresent** ](https://msdn.microsoft.com/library/windows/hardware/ff545591)为每个找到的子设备。 此调用会通知框架驱动程序已发现的子设备连接到父设备。 当您的驱动程序调用**WdfChildListAddOrUpdateChildDescriptionAsPresent**，它会提供一个标识说明和地址描述 （可选）。

驱动程序调用后[ **WdfChildListAddOrUpdateChildDescriptionAsPresent** ](https://msdn.microsoft.com/library/windows/hardware/ff545591)若要报告的新设备，该框架将告知存在新的设备的即插即用管理器。 PnP 管理器然后构建设备堆栈和新设备的驱动程序堆栈。 作为此过程的一部分，框架将调用总线驱动程序[ *EvtChildListCreateDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540828)回调函数。 必须调用此回调函数[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)若要创建的新设备 PDO。

通常情况下，多个子设备连接到一个父级，因此总线驱动程序将需要调用[ **WdfChildListAddOrUpdateChildDescriptionAsPresent** ](https://msdn.microsoft.com/library/windows/hardware/ff545591)几次。 执行此操作的最有效方法是以下：

1.  调用[ **WdfChildListBeginScan**](https://msdn.microsoft.com/library/windows/hardware/ff545608)。

2.  调用[ **WdfChildListAddOrUpdateChildDescriptionAsPresent** ](https://msdn.microsoft.com/library/windows/hardware/ff545591)为每个子设备。

3.  调用[ **WdfChildListEndScan**](https://msdn.microsoft.com/library/windows/hardware/ff545626)。

如果您的驱动程序通过调用动态枚举括住[ **WdfChildListBeginScan** ](https://msdn.microsoft.com/library/windows/hardware/ff545608)并[ **WdfChildListEndScan**](https://msdn.microsoft.com/library/windows/hardware/ff545626)、框架将存储的所有更改到子列表中，并在驱动程序调用时通知所做的更改的即插即用管理器**WdfChildListEndScan**。 在某些更高版本时，框架将调用总线驱动程序[ *EvtChildListCreateDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540828)子列表中每个设备的回调函数。 此回调函数将调用[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)来创建 PDO 为每个新设备。

当您的驱动程序调用[ **WdfChildListBeginScan**](https://msdn.microsoft.com/library/windows/hardware/ff545608)，框架将标记为不再存在的所有先前报告的设备。 因此，该驱动程序必须调用[ **WdfChildListAddOrUpdateChildDescriptionAsPresent** ](https://msdn.microsoft.com/library/windows/hardware/ff545591)为驱动程序可以检测到的所有子项，不仅仅是新发现子级。 要将单个子级添加到子列表中，该驱动程序可以进行调用一次[ **WdfChildListUpdateAllChildDescriptionsAsPresent** ](https://msdn.microsoft.com/library/windows/hardware/ff545667)而无需第一个调用**WdfChildListBeginScan**.

### <a name="updating-a-dynamic-child-list"></a>正在更新动态子列表

有两种常用方法，以更新动态子列表中的信息：

1.  当父设备收到指示的到达或删除子级，该驱动程序的中断[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)回调函数调用[ **WdfChildListAddOrUpdateChildDescriptionAsPresent** ](https://msdn.microsoft.com/library/windows/hardware/ff545591)如果在插入设备或[ **WdfChildListUpdateChildDescriptionAsMissing** ](https://msdn.microsoft.com/library/windows/hardware/ff545674)如果设备已被拔出。

2.  该驱动程序可以提供[ *EvtChildListScanForChildren* ](https://msdn.microsoft.com/library/windows/hardware/ff540838)回调函数，框架将调用每次父设备进入其工作 (D0) 状态。 此回调函数应通过调用枚举所有子设备[ **WdfChildListBeginScan**](https://msdn.microsoft.com/library/windows/hardware/ff545608)， [ **WdfChildListAddOrUpdateChildDescriptionAsPresent**](https://msdn.microsoft.com/library/windows/hardware/ff545591) (或[ **WdfChildListUpdateAllChildDescriptionsAsPresent**](https://msdn.microsoft.com/library/windows/hardware/ff545667))，和[ **WdfChildListEndScan** ](https://msdn.microsoft.com/library/windows/hardware/ff545626).

可以在您的驱动程序中使用一个或这两种方法。

### <a name="traversing-a-dynamic-child-list"></a>遍历动态子列表

如果您希望您的驱动程序来检查子列表的内容，它可以通过以下方法之一来遍历列表：

-   若要获取设备描述，一次一个的每个子级的内容驱动程序可以：

    1.  调用[ **WdfChildListBeginIteration**](https://msdn.microsoft.com/library/windows/hardware/ff545601)。
    2.  调用[ **WdfChildListRetrieveNextDevice**](https://msdn.microsoft.com/library/windows/hardware/ff545655)、 根据需要尽可能多的时间。
    3.  调用[ **WdfChildListEndIteration**](https://msdn.microsoft.com/library/windows/hardware/ff545618)。

    调用时[ **WdfChildListBeginIteration**](https://msdn.microsoft.com/library/windows/hardware/ff545601)，该驱动程序指定[ **WDF\_检索\_子\_标志**](https://msdn.microsoft.com/library/windows/hardware/ff552507)-类型化标志，指示框架是否应检索所有设备说明或只是一个子集。 当[ **WdfChildListRetrieveNextDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff545655)找到的匹配项，它将检索子设备标识和地址的说明，以及其设备对象的句柄。

-   如果你需要获取当前子设备说明中包含的地址说明，可以调用您的驱动程序[ **WdfChildListRetrieveAddressDescription**](https://msdn.microsoft.com/library/windows/hardware/ff545648)，并指定标识说明。 Framework 会遍历子列表，直到它找到具有匹配的标识描述的子设备，然后它检索地址描述。

-   如果你需要获取与特定子设备相关联的 framework 设备对象的句柄，可以调用您的驱动程序[ **WdfChildListRetrievePdo**](https://msdn.microsoft.com/library/windows/hardware/ff545663)。 该框架会遍历子列表，直到找到具有匹配的标识描述的子设备，然后返回设备对象句柄。

### <a name="accessing-a-pdos-identification-and-address-descriptions"></a>访问 PDO 的标识和地址说明

您的驱动程序可以调用以下方法来访问 PDO 标识说明或地址描述：

-   [**WdfPdoRetrieveIdentificationDescription**](https://msdn.microsoft.com/library/windows/hardware/ff548824)，检索与 PDO 相关联的标识说明。

-   [**WdfPdoRetrieveAddressDescription**](https://msdn.microsoft.com/library/windows/hardware/ff548820)，检索与 PDO 相关联的地址说明。

-   [**WdfPdoUpdateAddressDescription**](https://msdn.microsoft.com/library/windows/hardware/ff548826)，该更新与 PDO 相关联的地址说明。

 

 





