---
title: IRP_MN_QUERY_ID
description: 总线驱动程序必须处理其子设备（子 PDOs）对 BusQueryDeviceID 的请求。 总线驱动程序可以为其子设备处理 BusQueryHardwareIDs、BusQueryCompatibleIDs 和 BusQueryInstanceID 的请求。
ms.date: 08/12/2017
ms.assetid: 3135cb30-a696-4201-8dfc-cdc1a29fe52b
keywords:
- IRP_MN_QUERY_ID 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 9caa4d0e24eca9d73f3058b366e945c1799877e7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828024"
---
# <a name="irp_mn_query_id"></a>IRP\_MN\_查询\_ID


总线驱动程序必须处理其子设备（子 PDOs）对**BusQueryDeviceID**的请求。 总线驱动程序可以为其子设备处理**BusQueryHardwareIDs**、 **BusQueryCompatibleIDs**和**BusQueryInstanceID**的请求。

从 Windows 7 开始，总线驱动程序还必须处理其子 PDOs 的 BusQueryContainerID 请求。

有关这些标识符（Id）的详细信息，请参阅[设备标识字符串](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings)。

**请注意**  函数驱动程序和筛选器驱动程序不处理此 IRP。

 

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)发送时间
---------

在枚举设备时，PnP 管理器会发送此 IRP。 驱动程序可能会发送此 IRP，以检索其某个设备的实例 ID。

PnP 管理器和驱动程序以 IRQL 被动\_级别将此 IRP 发送到任意线程上下文中。

## <a name="input-parameters"></a>输入参数


[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)结构的**QueryId. IdType**成员指定请求的 ID 类型。 可能的值包括 BusQueryDeviceID、BusQueryHardwareIDs、BusQueryCompatibleIDs、BusQueryInstanceID 和 BusQueryContainerID。 保留以下 ID 类型： BusQueryDeviceSerialNumber。

## <a name="output-parameters"></a>输出参数


在 i/o 状态块中返回。

## <a name="io-status-block"></a>I/O 状态块


驱动程序将**Irp&gt;IoStatus**设置为 STATUS\_SUCCESS 或相应的错误状态。

成功时，驱动程序将**Irp&gt;IoStatus**设置为指向所请求信息的 WCHAR 指针。 出现错误时，驱动程序将**Irp&gt;IoStatus**设置为零。

<a name="operation"></a>操作
---------

如果驱动程序返回 ID 以响应此 IRP，则会从分页池分配 WCHAR 结构以包含 ID。 当不再需要该结构时，PnP 管理器会将其释放。

驱动程序返回以下项之一：

-   REG\_SZ string，用于响应 BusQueryDeviceID、BusQueryInstanceID 或 BusQueryContainerID 请求。

-   REG\_多\_SZ 字符串来响应 BusQueryHardwareIDs 或 BusQueryCompatibleIDs 请求。

如果驱动程序返回的 ID 具有非法字符，系统将检查错误。 具有以下值的字符在此 IRP 的 ID 中是非法的：

-   小于或等于0x20 （' '）

-   大于0x7F

-   等于0x2C （'，'）

驱动程序必须符合以下 Id 长度限制：

-   驱动程序在此 IRP 中返回的每个硬件 ID 或兼容 ID 的长度必须小于\_设备\_ID 长度\_长度。 此常量当前的值为200，如 sdk\\inc.\\cfgmgr32 中所定义。

-   驱动程序在此 IRP 中返回的容器 ID 必须设置为全局唯一标识符（GUID）的格式，并且必须是最大\_GUID\_字符串\_长度字符，其中包含 null 终止符。

-   如果总线驱动程序为其子设备提供全局唯一的实例 Id （即，驱动程序将[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)设置为 **。** 设备的 UniqueID），则设备 ID 加上实例 id 的组合必须小于（最大\_设备\_ID\_长度-1）个字符。 操作系统要求使用其他字符作为路径分隔符。

-   如果总线驱动程序未提供其子设备的全局唯一实例 Id，则设备 ID 加上实例 ID 的组合必须小于（最大\_设备\_ID\_长度为28）。 此公式的值目前为172。

在枚举设备后，应该立即准备好总线驱动程序为子设备处理此 IRP。

**指定 BusQueryDeviceID 和 BusQueryInstanceID**

总线驱动程序为 BusQueryDeviceID 和 BusQueryInstanceID 提供的值允许操作系统将设备与计算机上的其他设备区分开来。 操作系统使用**irp\_MN\_QUERY\_id** IRP 中返回的设备 id 和实例 id，并在[**irp\_MN\_query\_功能**](irp-mn-query-capabilities.md)IRP 中返回，以定位设备的注册表信息。

对于**BusQueryDeviceID**，总线驱动程序提供设备的*设备 ID*。 设备 ID 应该包含设备的最特定说明，其中包含用于标识制造商、设备、修订、包装器和封装产品的枚举器名称和字符串（如果可能）。 例如，PCI 总线驱动程序以 PCI\\即使\_xxxx & 开发\_xxxx & 子系统\_xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx & 的设备 Id 来响应以上提到的所有五项。\_ 不过，设备 ID 不应包含足够的信息来区分两个相同的设备。 此信息应在实例 ID 中进行编码。

对于 BusQueryInstanceID，总线驱动程序应提供包含设备*实例 ID*的字符串。 安装程序和总线驱动程序使用实例 ID 和其他信息来区分计算机上两个相同的设备。 实例 ID 在整个计算机中是唯一的，或者只在设备的父总线上是唯一的。

如果实例 ID 只在总线上是唯一的，则总线驱动程序会为 BusQueryInstanceID 指定 string，还会**将 MN 值指定** **为响应** [**IRP\_\_查询\_功能**](irp-mn-query-capabilities.md)请求。 如果**UniqueID**为**FALSE**，则 PnP 管理器会通过添加有关设备父节点的信息来增强实例 ID，从而使 id 在计算机上是唯一的。 在这种情况下，总线驱动程序不应执行额外的步骤来使其设备的实例 Id 全局唯一;只需返回相应的功能信息，操作系统就会对其进行处理。

如果总线驱动程序可以为每个子设备提供全局唯一 ID （如序列号），则总线驱动程序会为 BusQueryInstanceID 指定这些字符串，并为响应[**IRP\_MN\_查询\_** ](irp-mn-query-capabilities.md)每个设备请求功能请求指定**UniqueID**值为**TRUE** 。

**指定 BusQueryHardwareIDs 和 BusQueryCompatibleIDs**

总线驱动程序为 BusQueryHardwareIDs 和 BusQueryCompatibleIDs 提供的值允许安装程序查找总线子设备的相应驱动程序。

总线驱动程序使用 REG\_多\_SZ 的 Id 列表（用于描述设备的 Id）来响应每个请求。 Id 列表的最大长度（以字符为单位），包括终止列表的两个 NULL 字符，REGSTR\_VAL\_MAX\_HCID\_长度。

返回多个*硬件 id*和/或多个*兼容 ID*时，总线驱动程序应按照从最具体到最常见的顺序列出 id，以便为设备选择最佳的驱动程序匹配项。 硬件 Id 列表中的第一项是设备的最特定说明，因此，它通常与设备 ID 完全相同。

安装程序将根据 INF 文件中列出的 Id 检查 Id 以查找可能的匹配项。 安装程序首先扫描硬件 Id 列表，然后扫描兼容 Id 列表。 更早的条目被视为设备的更具体的说明，更高的条目作为设备的更常规（因而不太理想）。 如果在硬件 Id 列表中找不到匹配项，则安装程序可能会提示用户安装媒体，然后再转到兼容 Id 列表。

请参阅[即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)，了解用于处理[即插即用次要 irp](plug-and-play-minor-irps.md)的一般规则。

**指定 BusQueryContainerIDs**

从 Windows 7 开始，总线驱动程序应为包含设备[容器 ID](https://docs.microsoft.com/windows-hardware/drivers/install/container-ids)的 BusQueryContainerID 提供一个字符串。 容器 ID 允许操作系统将所有功能设备从一个可移动物理设备进行分组。 例如，从可移动多功能设备获得的所有功能设备具有相同的容器 ID。 有关在特殊情况下报告容器 Id 的详细信息，例如可能跨多个容器中多个磁盘但不属于任何容器的卷设备，请参阅[容器 Id 概述](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-container-ids)。

可移动的物理设备被定义为一个子设备，该设备的总线驱动程序为响应[**IRP\_MN\_QUERY\_功能**](irp-mn-query-capabilities.md)请求而指定了**TRUE**的**可移动**功能。 有关**可移动**值的详细信息，请参阅[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)。

总线驱动程序根据设备提供的特定于总线的唯一 ID 创建容器 ID。 有关详细信息，请参阅[如何生成容器 id](https://docs.microsoft.com/windows-hardware/drivers/install/how-container-ids-are-generated)。

如果满足以下任一条件，则驱动程序必须使 IRP 请求失败并将**IoStatus**设置为状态\_不\_支持：

-   设备不支持总线驱动程序可用于生成容器 ID 的特定于总线的唯一 ID。

-   总线驱动程序以前指定了**FALSE**的**可移动**功能，以响应[**IRP\_MN\_查询设备\_功能**](irp-mn-query-capabilities.md)请求。

**正在发送此 IRP**

通常，只有 PnP 管理器发送此 IRP。

若要获取设备的硬件 Id 或兼容 Id，请调用[**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)而不是发送此 IRP。

驱动程序可能会发送此 IRP，以检索其某个设备的实例 ID。 例如，请考虑其功能不单独操作的多功能 PnP ISA 设备。 PnP 管理器将函数枚举为单独的设备，但可能需要此类设备的驱动程序来关联一个或多个函数。 由于 PnP ISA 保证唯一的实例 ID，因此此类多功能设备的驱动程序可以使用实例 Id 来查找驻留在同一设备上的函数。 此类设备的驱动程序还必须通过调用[**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)来获取设备的枚举器名称，以确认该设备是否为 PnP ISA 设备。

有关发送 Irp 的信息，请参阅[处理 irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps) 。 以下步骤专门适用于此 IRP：

-   在 IRP 的下一个 i/o 堆栈位置设置值：将**MajorFunction**设置为[**irp\_MJ\_PNP**](irp-mj-pnp.md)，将**MINORFUNCTION**设置为 IRP\_MN\_查询\_ID，并将**QueryId**设置为**IdType**。

-   将**IoStatus**设置为\_不\_支持的状态。

除了发送查询 ID IRP 外，驱动程序还必须调用[**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)来获取设备的**DevicePropertyEnumeratorName** 。

完成 IRP 并且驱动程序使用 ID 完成后，驱动程序必须释放由处理 query IRP 的驱动程序返回的 ID 结构。

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
<td>Wdm.h（包括 Wdm.h、Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[设备标识字符串](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings)

[**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)

 

 




