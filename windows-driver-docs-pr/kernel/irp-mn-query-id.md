---
title: IRP_MN_QUERY_ID
description: 总线驱动程序必须处理 (子 PDOs) 子设备的 BusQueryDeviceID 请求。 总线驱动程序可以为其子设备处理 BusQueryHardwareIDs、BusQueryCompatibleIDs 和 BusQueryInstanceID 的请求。
ms.date: 08/12/2017
ms.assetid: 3135cb30-a696-4201-8dfc-cdc1a29fe52b
keywords:
- IRP_MN_QUERY_ID 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 9446f562058fed642aa1e95ceb70ec00a0fb5365
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103148"
---
# <a name="irp_mn_query_id"></a>IRP \_ MN \_ 查询 \_ ID


总线驱动程序必须处理 (子 PDOs) 子设备的 **BusQueryDeviceID** 请求。 总线驱动程序可以为其子设备处理 **BusQueryHardwareIDs**、 **BusQueryCompatibleIDs**和 **BusQueryInstanceID** 的请求。

从 Windows 7 开始，总线驱动程序还必须处理其子 PDOs 的 BusQueryContainerID 请求。

有关这些标识符 (Id) 的详细信息，请参阅 [设备标识字符串](../install/device-identification-strings.md)。

**注意**   函数驱动程序和筛选器驱动程序不处理此 IRP。

 ## <a name="value"></a>“值”

0x13


<a name="major-code"></a>主要代码
----------

[**IRP \_ MJ \_ PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>发送时间
---------

在枚举设备时，PnP 管理器会发送此 IRP。 驱动程序可能会发送此 IRP，以检索其某个设备的实例 ID。

PnP 管理器和驱动程序将此 IRP 以 IRQL 被动级别发送到 \_ 任意线程上下文中。

## <a name="input-parameters"></a>输入参数


[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)结构的**QueryId. IdType**成员指定 () 请求的 ID 类型。 可能的值包括 BusQueryDeviceID、BusQueryHardwareIDs、BusQueryCompatibleIDs、BusQueryInstanceID 和 BusQueryContainerID。 保留以下 ID 类型： BusQueryDeviceSerialNumber。

## <a name="output-parameters"></a>输出参数


在 i/o 状态块中返回。

## <a name="io-status-block"></a>I/o 状态块


驱动程序将 **Irp- &gt; IoStatus** 设置为状态 " \_ 成功" 或相应的 "错误" 状态。

成功时，驱动程序将 ** &gt; IoStatus** 设置为指向所请求信息的 WCHAR 指针。 出现错误时，驱动程序将 **Irp- &gt; IoStatus** 设置为零。

<a name="operation"></a>操作
---------

如果驱动程序返回 ID (s 为响应此 IRP) ，则它会从分页池分配 WCHAR 结构，以包含) 的 (ID。 当不再需要该结构时，PnP 管理器会将其释放。

驱动程序返回以下项之一：

-   作为 \_ BusQueryDeviceID、BusQueryInstanceID 或 BusQueryContainerID 请求的响应的 REG SZ 字符串。

-   \_ \_ 用于响应 BusQueryHardwareIDs 或 BusQueryCompatibleIDs 请求的 REG 多 SZ 字符串。

如果驱动程序返回的 ID 具有非法字符，系统将检查错误。 具有以下值的字符在此 IRP 的 ID 中是非法的：

-   小于或等于 0x20 ( "" ) 

-   大于0x7F

-   等于 0x2C ( '，' ) 

驱动程序必须符合以下 Id 长度限制：

-   驱动程序在此 IRP 中返回的每个硬件 ID 或兼容 ID 的长度必须小于 \_ 设备 id 长度的最大 \_ \_ 字符数。 此常量当前的值为200，如 sdk inc. cfgmgr32 中所定义 \\ \\ 。

-   驱动程序在此 IRP 中返回的容器 ID 必须设置为 (GUID) 全局唯一标识符，并且必须是最大 \_ guid \_ 字符串 \_ 长度字符，其中包含 null 终止符。

-   如果总线驱动程序为其子设备提供全局唯一的实例 Id (即，驱动程序将设置 [**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)**。**) 设备的 UniqueID，则设备 id 加实例 ID 的组合必须小于 (MAX \_ 设备 \_ id \_ LEN-1) 字符。 操作系统要求使用其他字符作为路径分隔符。

-   如果总线驱动程序未提供其子设备的全局唯一实例 Id，则设备 ID 加上实例 ID 的组合必须小于 (最大 \_ 设备 \_ id \_ 长度-28) 。 此公式的值目前为172。

在枚举设备后，应该立即准备好总线驱动程序为子设备处理此 IRP。

**指定 BusQueryDeviceID 和 BusQueryInstanceID**

总线驱动程序为 BusQueryDeviceID 和 BusQueryInstanceID 提供的值允许操作系统将设备与计算机上的其他设备区分开来。 操作系统使用 **irp \_ MN \_ query \_ ID** IRP 中返回的设备 id 和实例 id，并使用 [**irp \_ MN \_ 查询 \_ 功能**](irp-mn-query-capabilities.md) irp 中返回的唯一 ID 字段来查找设备的注册表信息。

对于 **BusQueryDeviceID**，总线驱动程序提供设备的 *设备 ID*。 设备 ID 应该包含设备的最特定说明，其中包含用于标识制造商、设备、修订、包装器和封装产品的枚举器名称和字符串（如果可能）。 例如，PCI 总线驱动程序以 PCI 即使 xxxx 的设备 Id 进行响应 \\ \_&DEV \_ xxxx&子系统 \_ xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx&REV \_ xx，并对上面提到的五项内容进行编码。 不过，设备 ID 不应包含足够的信息来区分两个相同的设备。 此信息应在实例 ID 中进行编码。

对于 BusQueryInstanceID，总线驱动程序应提供包含设备 *实例 ID* 的字符串。 安装程序和总线驱动程序使用实例 ID 和其他信息来区分计算机上两个相同的设备。 实例 ID 在整个计算机中是唯一的，或者只在设备的父总线上是唯一的。

如果实例 ID 只在总线上是唯一的，则总线驱动程序会为 BusQueryInstanceID 指定该字符串，同时为响应对设备的[**IRP \_ MN \_ 查询 \_ 功能**](irp-mn-query-capabilities.md)请求指定**UniqueID**值**FALSE** 。 如果 **UniqueID** 为 **FALSE**，则 PnP 管理器会通过添加有关设备父节点的信息来增强实例 ID，从而使 id 在计算机上是唯一的。 在这种情况下，总线驱动程序不应执行额外的步骤来使其设备的实例 Id 全局唯一;只需返回相应的功能信息，操作系统就会对其进行处理。

如果总线驱动程序可以为每个子设备提供全局唯一 ID （如序列号），则总线驱动程序会为 BusQueryInstanceID 指定这些字符串，并为响应每个设备的[**IRP \_ MN \_ 查询 \_ 功能**](irp-mn-query-capabilities.md)请求指定**UniqueID**值**TRUE** 。

**指定 BusQueryHardwareIDs 和 BusQueryCompatibleIDs**

总线驱动程序为 BusQueryHardwareIDs 和 BusQueryCompatibleIDs 提供的值允许安装程序查找总线子设备的相应驱动程序。

总线驱动程序使用用于描述设备的注册表 Id 的 REG \_ 多 SZ 列表来响应每个请求 \_ 。 Id 列表的最大长度（以字符为单位），其中包括终止列表的两个 NULL 字符，最大值为 REGSTR \_ \_ \_ \_ 。

返回多个 *硬件 id* 和/或多个 *兼容 ID*时，总线驱动程序应按照从最具体到最常见的顺序列出 id，以便为设备选择最佳的驱动程序匹配项。 硬件 Id 列表中的第一项是设备的最特定说明，因此，它通常与设备 ID 完全相同。

安装程序将根据 INF 文件中列出的 Id 检查 Id 以查找可能的匹配项。 安装程序首先扫描硬件 Id 列表，然后扫描兼容 Id 列表。 更早的条目被视为更具体的设备描述，更高的条目作为更常规的 (，因此与设备的最佳) 匹配更少。 如果在硬件 Id 列表中找不到匹配项，则安装程序可能会提示用户安装媒体，然后再转到兼容 Id 列表。

请参阅 [即插即用](./introduction-to-plug-and-play.md) ，了解用于处理 [即插即用次要 irp](plug-and-play-minor-irps.md)的一般规则。

**指定 BusQueryContainerIDs**

从 Windows 7 开始，总线驱动程序应为包含设备 [容器 ID](../install/container-ids.md) 的 BusQueryContainerID 提供一个字符串。 容器 ID 允许操作系统将所有功能设备从一个可移动物理设备进行分组。 例如，从可移动多功能设备获得的所有功能设备具有相同的容器 ID。 有关在特殊情况下报告容器 Id 的详细信息，例如可能跨多个容器中多个磁盘但不属于任何容器的卷设备，请参阅 [容器 Id 概述](../install/overview-of-container-ids.md)。

可移动的物理设备被定义为一个子设备，该设备的总线驱动程序为响应[**IRP \_ MN \_ 查询 \_ 功能**](irp-mn-query-capabilities.md)请求而指定了**TRUE**的**可移动**功能。 有关 **可移动** 值的详细信息，请参阅 [**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)。

总线驱动程序根据设备提供的特定于总线的唯一 ID 创建容器 ID。 有关详细信息，请参阅 [如何生成容器 id](../install/how-container-ids-are-generated.md)。

**IoStatus.Status** \_ \_ 如果满足以下任一条件，则驱动程序必须使 IRP 请求失败并将 IoStatus 设置为状态。

-   设备不支持总线驱动程序可用于生成容器 ID 的特定于总线的唯一 ID。

-   总线驱动程序以前指定了**FALSE**的**可移动**功能，以响应对设备的[**IRP \_ MN \_ 查询 \_ 功能**](irp-mn-query-capabilities.md)请求。

**正在发送此 IRP**

通常，只有 PnP 管理器发送此 IRP。

若要获取设备的硬件 Id 或兼容 Id，请调用 [**IoGetDeviceProperty**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty) 而不是发送此 IRP。

驱动程序可能会发送此 IRP，以检索其某个设备的实例 ID。 例如，请考虑其功能不单独操作的多功能 PnP ISA 设备。 PnP 管理器将函数枚举为单独的设备，但可能需要此类设备的驱动程序来关联一个或多个函数。 由于 PnP ISA 保证唯一的实例 ID，因此此类多功能设备的驱动程序可以使用实例 Id 来查找驻留在同一设备上的函数。 此类设备的驱动程序还必须通过调用 [**IoGetDeviceProperty**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)来获取设备的枚举器名称，以确认该设备是否为 PnP ISA 设备。

有关发送 Irp 的信息，请参阅 [处理 irp](./handling-irps.md) 。 以下步骤专门适用于此 IRP：

-   设置 IRP 的下一个 i/o 堆栈位置中的值：将 **MajorFunction** 设置为 [**irp \_ MJ \_ PNP**](irp-mj-pnp.md)，将 **MinorFunction** 设置为 irp \_ MN \_ 查询 \_ ID，并将 **QueryId** 设置为 **IdType**。

-   将 **IoStatus** 设置为 \_ 不 \_ 受支持的状态。

除了发送查询 ID IRP 外，驱动程序还必须调用 [**IoGetDeviceProperty**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty) 来获取设备的 **DevicePropertyEnumeratorName** 。

IRP 完成并且驱动程序已使用 ID 完成后，驱动程序必须释放由驱动程序返回的 ID 结构， (处理查询 IRP 的) 。

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


[设备标识字符串](../install/device-identification-strings.md)

[**IoGetDeviceProperty**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)

 

