---
title: 动态枚举
description: 动态枚举
ms.assetid: 6e46b456-7d2d-4c6e-8692-7f310366387d
keywords:
- 动态枚举 WDK KMDF
- 子说明 WDK KMDF
- 地址说明 WDK KMDF
- 标识说明 WDK KMDF
- 动态子列表 WDK KMDF
- 遍历动态子列表 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6dc1417e1626e318757746f406d42b088004063
ms.sourcegitcommit: 9796f75f8e83f4c9cc1f055056910a3ae6292f18
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93066351"
---
# <a name="dynamic-enumeration"></a>动态枚举


*动态枚举* 是驱动程序在系统运行时对连接到系统的设备的数量和类型进行检测和报告更改的能力。

如果连接到父设备的设备数取决于系统的配置，则总线驱动程序必须使用动态枚举。 其中一些设备可能始终连接到系统，某些设备可能会在系统运行时插入并拔下。

例如，插入到系统 PCI 总线中的设备的数量和类型与系统相关，但它们是永久性的，除非用户关闭电源、打开机箱，并使用螺丝刀添加或删除设备。 另一方面，在系统运行时，用户可以通过插入或拔出电缆来添加或删除 USB 设备。

### <a name="dynamic-child-lists"></a>动态子列表

使用框架，驱动程序可通过提供框架子列表对象支持动态枚举。 每个子列表对象代表连接到父设备的子设备的列表。 父设备的总线驱动程序必须标识父设备的子设备，将其添加到父设备的子列表，并为每个子设备 (PDO) 创建物理设备对象。

每当驱动程序创建一个表示设备的 FDO 的框架设备对象时，框架都会为该设备创建一个空的默认子列表。 你的驱动程序可以通过调用 [**WdfFdoGetDefaultChildList**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdogetdefaultchildlist)来获取设备的默认子列表的句柄。 通常，如果您正在编写枚举设备子项的总线驱动程序，则您的驱动程序可以将子项添加到默认子列表中。 如果需要创建其他子列表，则驱动程序可以调用 [**WdfChildListCreate**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistcreate)。

在驱动程序可以使用子列表之前，它必须通过初始化 [**WDF \_ 子 \_ 列表 \_**](/windows-hardware/drivers/ddi/wdfchildlist/ns-wdfchildlist-_wdf_child_list_config) 配置结构并将该结构传递给 [**WdfFdoInitSetDefaultChildListConfig**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitsetdefaultchildlistconfig)（对于默认子列表）或 [**WdfChildListCreate**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistcreate)（对于其他子列表）来配置子列表对象。

### <a name="dynamic-child-descriptions"></a>动态子说明

每次总线驱动程序标识子设备时，它必须将子设备的说明添加到子列表中。 *子说明* 由所需的 *标识说明* 和可选 *地址说明* 组成。

<a href="" id="identification-description"></a>*标识描述* 标识说明是一个结构，其中包含用于唯一标识驱动程序所枚举的每个设备的信息。 驱动程序定义此结构，但它的第一个成员必须是 [**WDF \_ 子 \_ 标识 \_ 说明 \_ 标头**](/windows-hardware/drivers/ddi/wdfchildlist/ns-wdfchildlist-_wdf_child_identification_description_header) 结构。

通常，标识描述包含设备的 [设备标识字符串](../install/device-identification-strings.md)，可能是序列号，以及有关设备在总线上的位置的信息，如插槽号。

驱动程序可以提供以下回调函数集，这允许框架在标识说明中操作信息：

-   [*EvtChildListIdentificationDescriptionCompare*](/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_identification_description_compare)，用于比较两个标识描述结构的内容。

-   [*EvtChildListIdentificationDescriptionCopy*](/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_identification_description_copy)，它将一个标识说明结构的内容复制到另一个。

-   [*EvtChildListIdentificationDescriptionDuplicate*](/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_identification_description_duplicate)，它通过复制现有标识描述结构并在必要时分配其他缓冲区来创建新的标识描述。

-   [*EvtChildListIdentificationDescriptionCleanup*](/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_identification_description_cleanup)，用于释放由 [*EvtChildListIdentificationDescriptionDuplicate*](/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_identification_description_duplicate) 回调函数分配的缓冲区。

通常，如果驱动程序的标识说明结构包含动态分配的缓冲区的指针，则需要提供这些回调函数。 有关这些回调函数用途的详细信息，请参阅其引用页面。

<a href="" id="address-description"></a>*地址说明* 地址说明是一个结构，其中包含驱动程序所需的信息，以便在设备接通电源的情况下可以在设备总线上访问设备。 驱动程序定义此结构，但其第一个成员必须为 [**WDF \_ 子 \_ 地址 \_ 说明 \_ 标头**](/windows-hardware/drivers/ddi/wdfchildlist/ns-wdfchildlist-_wdf_child_address_description_header) 结构。

地址说明是可选的。 如果设备的地址信息无法在设备接通电源与拔下设备的时间之间更改，则所有设备的地址信息都可以存储在标识描述中。 例如，当设备接通电源时，USB 控制器会将地址分配给设备，并且这些地址不会更改。

另一方面，某些总线使用可以更改的寻址信息。 例如，IEEE 1394 总线使用 "生成计数"，这是已发生的总线重置次数。 对 IEEE 1394 设备的每个异步 i/o 请求都必须包括生成计数。 由于此地址信息可能会更改，因此你的驱动程序必须将其存储在地址说明中。

驱动程序可以提供下列一组回调函数来处理地址说明中的信息：

-   [*EvtChildListAddressDescriptionCopy*](/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_address_description_copy)，它将一个地址说明结构的内容复制到另一个地址说明结构。

-   [*EvtChildListAddressDescriptionDuplicate*](/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_address_description_duplicate)，它通过复制现有地址说明结构并在必要时分配其他缓冲区来创建新的地址说明。

-   [*EvtChildListAddressDescriptionCleanup*](/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_address_description_cleanup)，用于释放由 [*EvtChildListAddressDescriptionDuplicate*](/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_address_description_duplicate) 回调函数分配的缓冲区。

通常，如果驱动程序的地址说明结构包含动态分配的缓冲区的指针，则需要提供这些回调函数。 有关这些回调函数用途的详细信息，请参阅其引用页面。

### <a name="adding-devices-to-a-dynamic-child-list"></a>向动态子列表添加设备

当框架调用总线驱动程序的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数时，回调函数必须调用 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate) 来为父设备创建 FDO，这通常是一个总线适配器。 有关创建 FDO 的详细信息，请参阅 [在函数驱动程序中创建设备对象](creating-device-objects-in-a-function-driver.md)。 然后，该驱动程序必须枚举父设备的子节点并将该子项添加到子列表中。

或者，驱动程序可以调用 [**WdfDeviceSetBusInformationForChildren**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetbusinformationforchildren) 来向框架提供有关总线的信息。 建议这样做，因为这样可以更轻松地让子设备和应用识别总线。

若要向子列表添加子级，驱动程序必须为它找到的每个子设备调用 [**WdfChildListAddOrUpdateChildDescriptionAsPresent**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistaddorupdatechilddescriptionaspresent) 。 此调用通知框架驱动程序已发现连接到父设备的子设备。 当你的驱动程序调用 **WdfChildListAddOrUpdateChildDescriptionAsPresent** 时，它将提供标识说明并根据需要提供地址说明。

驱动程序调用 [**WdfChildListAddOrUpdateChildDescriptionAsPresent**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistaddorupdatechilddescriptionaspresent) 来报告新设备后，框架会通知 PnP 管理器新设备已存在。 然后，PnP 管理器将为新设备生成设备堆栈和驱动程序堆栈。 作为此过程的一部分，框架将调用总线驱动程序的 [*EvtChildListCreateDevice*](/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device) 回调函数。 此回调函数必须调用 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate) 来创建新设备的 PDO。

通常，多个子设备连接到一个父设备，因此总线驱动程序将需要多次调用 [**WdfChildListAddOrUpdateChildDescriptionAsPresent**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistaddorupdatechilddescriptionaspresent) 。 最有效的方法是执行以下操作：

1.  调用 [**WdfChildListBeginScan**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistbeginscan)。

2.  为每个子设备调用 [**WdfChildListAddOrUpdateChildDescriptionAsPresent**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistaddorupdatechilddescriptionaspresent) 。

3.  调用 [**WdfChildListEndScan**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistendscan)。

如果你在驱动程序的动态枚举中包含对 [**WdfChildListBeginScan**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistbeginscan) 和 [**WdfChildListEndScan**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistendscan)的调用，则该框架会将所有更改存储到子列表，并在驱动程序调用 **WdfChildListEndScan** 时，通知 PnP 经理发生的更改。 稍后，框架将为子列表中的每个设备调用总线驱动程序的 [*EvtChildListCreateDevice*](/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device) 回调函数。 此回调函数调用 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate) 为每个新设备创建一个 PDO。

当驱动程序调用 [**WdfChildListBeginScan**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistbeginscan)时，框架会将以前报告的所有设备标记为不再存在。 因此，驱动程序必须为驱动程序可以检测到的所有子级（而不只是新发现的子项）调用 [**WdfChildListAddOrUpdateChildDescriptionAsPresent**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistaddorupdatechilddescriptionaspresent) 。 若要向子列表添加单个子级，驱动程序可以对 [**WdfChildListUpdateAllChildDescriptionsAsPresent**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistupdateallchilddescriptionsaspresent) 进行单一调用，而无需先调用 **WdfChildListBeginScan** 。

### <a name="updating-a-dynamic-child-list"></a>更新动态子列表

更新动态子列表中的信息有两种常用方法：

1.  当父设备收到指示到达或移除某个子节点的中断时，如果设备已接通电源，驱动程序的 [*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) 回调函数会调用 [**WdfChildListAddOrUpdateChildDescriptionAsPresent**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistaddorupdatechilddescriptionaspresent) ，如果设备已拔出，则会调用 [**WdfChildListUpdateChildDescriptionAsMissing**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistupdatechilddescriptionasmissing) 。

2.  驱动程序可以提供一个 [*EvtChildListScanForChildren*](/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_scan_for_children) 回调函数，框架在每次父设备进入其工作 (D0) 状态时都将调用此函数。 此回调函数应通过调用 [**WdfChildListBeginScan**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistbeginscan)、 [**WdfChildListAddOrUpdateChildDescriptionAsPresent**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistaddorupdatechilddescriptionaspresent) (或 [**WdfChildListUpdateAllChildDescriptionsAsPresent**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistupdateallchilddescriptionsaspresent)) 和 [**WdfChildListEndScan**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistendscan)枚举所有子设备。

您可以在您的驱动程序中使用这两种方法中的一种或两种。

### <a name="traversing-a-dynamic-child-list"></a>遍历动态子列表

如果希望驱动程序检查子列表的内容，则可以使用以下技术之一遍历该列表：

-   若要获取每个子设备说明的内容（一次一个），驱动程序可以：

    1.  调用 [**WdfChildListBeginIteration**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistbeginiteration)。
    2.  尽可能多地调用 [**WdfChildListRetrieveNextDevice**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistretrievenextdevice)。
    3.  调用 [**WdfChildListEndIteration**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistenditeration)。

    当调用 [**WdfChildListBeginIteration**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistbeginiteration)时，驱动程序将指定一个 [**WDF \_ 检索 \_ 子 \_ 标记**](/windows-hardware/drivers/ddi/wdfchildlist/ne-wdfchildlist-_wdf_retrieve_child_flags)类型的标志，该标志指示框架是应检索所有设备说明还是仅检索子集。 当 [**WdfChildListRetrieveNextDevice**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistretrievenextdevice) 找到匹配项时，它将检索子设备的标识和地址说明以及其设备对象的句柄。

-   如果需要获取当前包含在子设备说明中的地址说明，则驱动程序可以调用 [**WdfChildListRetrieveAddressDescription**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistretrieveaddressdescription)，并指定标识描述。 框架遍历子列表，直到找到具有匹配标识说明的子设备，然后检索地址说明。

-   如果需要获取与特定子设备关联的框架设备对象的句柄，则驱动程序可以调用 [**WdfChildListRetrievePdo**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistretrievepdo)。 框架遍历子列表，直到找到具有匹配标识说明的子设备，然后返回设备对象句柄。 请确保将调用包装在 [**WdfChildListBeginIteration**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistbeginiteration) 和 [**WdfChildListEndIteration**](/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistenditeration) 中，以防止调用方突然将 PDO 移到另一个线程上。

### <a name="accessing-a-pdos-identification-and-address-descriptions"></a>访问 PDO 的标识和地址说明

你的驱动程序可以调用以下方法来访问 PDO 的标识说明或地址说明：

-   [**WdfPdoRetrieveIdentificationDescription**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoretrieveidentificationdescription)，用于检索与 PDO 关联的标识说明。

-   [**WdfPdoRetrieveAddressDescription**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoretrieveaddressdescription)，用于检索与 PDO 关联的地址说明。

-   [**WdfPdoUpdateAddressDescription**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoupdateaddressdescription)，用于更新与 PDO 关联的地址说明。

### <a name="handling-re-enumeration-requests"></a>处理重新枚举请求

支持动态枚举的基于框架的总线驱动程序可以接收通过 [**REENUMERATE_SELF_INTERFACE_STANDARD**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_reenumerate_self_interface_standard) 接口对特定子设备进行 reenumerate 的请求。 有关详细信息，请参阅 [处理枚举请求](./handling-enumeration-requests.md)