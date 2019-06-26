---
title: IRP_MN_QUERY_ID
description: 总线驱动程序必须处理请求 BusQueryDeviceID 子设备 (子 PDOs)。 总线驱动程序可以处理请求 BusQueryHardwareIDs、 BusQueryCompatibleIDs，和 BusQueryInstanceID 其子设备。
ms.date: 08/12/2017
ms.assetid: 3135cb30-a696-4201-8dfc-cdc1a29fe52b
keywords:
- IRP_MN_QUERY_ID 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 0fa130fb052422e49dbde20411d8de42fe31c34b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383281"
---
# <a name="irpmnqueryid"></a>IRP\_MN\_查询\_ID


总线驱动程序必须处理的请求**BusQueryDeviceID**为其子设备 (子 PDOs)。 总线驱动程序可以处理的请求**BusQueryHardwareIDs**， **BusQueryCompatibleIDs**，并**BusQueryInstanceID**为其子设备。

从 Windows 7 开始，总线驱动程序必须还处理请求的 BusQueryContainerID 及其子 PDOs。

有关这些标识符 (Id) 的详细信息，请参阅[设备标识字符串](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings)。

**请注意**  函数驱动程序和筛选器驱动程序不处理此 IRP。

 

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md) When Sent
---------

PnP 管理器将发送此 IRP，枚举设备时。 驱动程序可能会发送此 IRP，若要检索其设备之一的实例 ID。

PnP 管理器和驱动程序在 IRQL 被动发送此 IRP\_级别在任意线程上下文中。

## <a name="input-parameters"></a>输入参数


**Parameters.QueryId.IdType**的成员[ **IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)结构指定号请求的类型。 可能值包括 BusQueryDeviceID、 BusQueryHardwareIDs、 BusQueryCompatibleIDs、 BusQueryInstanceID 和 BusQueryContainerID。 保留以下 ID 类型：BusQueryDeviceSerialNumber。

## <a name="output-parameters"></a>输出参数


返回在 I/O 状态块中。

## <a name="io-status-block"></a>I/O 状态块


驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功或相应的错误状态。

如果成功，驱动程序设置**Irp-&gt;IoStatus.Information**为 WCHAR 指针指向所请求的信息。 出现错误时，驱动程序设置**Irp-&gt;IoStatus.Information**为零。

<a name="operation"></a>操作
---------

如果驱动程序对此 IRP 响应中返回号，它会从页面缓冲池以包含将 ID 分配 WCHAR 结构。 当不再需要时，即插即用管理器释放结构。

驱动程序将返回以下值之一：

-   REG\_响应 BusQueryDeviceID，BusQueryInstanceID，SZ 字符串或 BusQueryContainerID 请求。

-   REG\_多\_SZ BusQueryHardwareIDs 或 BusQueryCompatibleIDs 请求响应中的字符串。

如果驱动程序将返回具有非法字符的 ID，系统将 bug 检查。 使用以下值的字符是在此 irp ID 非法的：

-   小于或等于 0x20 ()

-   大于 0x7F

-   等于 0x2C （，）

驱动程序必须符合以下 Id 的长度限制：

-   每个硬件 ID 或兼容的驱动程序将返回在此 IRP 的 ID 必须小于最大\_设备\_ID\_LEN 个字符。 此常量当前具有值为 200，sdk 中定义\\inc\\cfgmgr32.h。

-   驱动程序将返回在此 IRP 的容器 ID 的格式必须为全局唯一标识符 (GUID)，并且必须是最大\_GUID\_字符串\_LEN 字符，其中包括 null 终止符。

-   如果总线驱动程序提供其子设备的全局唯一实例 Id (即，驱动程序设置[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities) **。UniqueID**的设备)，则设备 ID 与实例 ID 的组合必须是小于 (最大\_设备\_ID\_LEN-1) 个字符。 操作系统要求的其他字符的路径分隔符。

-   如果总线驱动程序不提供全局唯一的实例 Id 对于其子设备，则设备 ID 和实例 ID 的组合必须是小于 (最大\_设备\_ID\_LEN-28)。 此公式的值目前 172。

总线驱动程序应做好枚举设备后立即处理此 IRP 子设备。

**指定 BusQueryDeviceID 和 BusQueryInstanceID**

BusQueryDeviceID 和 BusQueryInstanceID 总线驱动程序提供的值允许操作系统以将设备与计算机上的其他设备区分开来。 操作系统使用设备 ID 和中返回的实例 ID **IRP\_MN\_查询\_ID** IRP 和唯一 ID 字段中返回[ **IRP\_MN\_查询\_功能**](irp-mn-query-capabilities.md) IRP，若要查找的设备的注册表信息。

有关**BusQueryDeviceID**，总线驱动程序提供的设备*设备 ID*。 设备 ID 应包含可能的设备，最具体说明合并字符串标识制造商、 设备、 修订、 包装程序和打包的产品提供，在可能的情况的枚举器的名称。 PCI 总线驱动程序，如使用设备 Id 的窗体 PCI 做出响应\\即使\_xxxx & 开发\_xxxx & SUBSYS\_xxxxxxxx & REV\_xx，编码上面提到的项的所有五个。 但是，设备 ID 不应包含足够的信息来区分两个完全相同的设备。 此信息应进行编码实例 id。

对于 BusQueryInstanceID，总线驱动程序应提供一个字符串，包含*实例 ID*设备。 安装程序和总线驱动程序使用的实例 ID，与其他信息，对计算机上的两个相同设备之间进行区分。 实例 ID 是唯一跨整个计算机或设备的父总线上只需唯一。

如果仅在总线上唯一实例 ID，总线驱动程序为 BusQueryInstanceID 指定该字符串，但还指定了**UniqueID**的值**FALSE**响应[ **IRP\_MN\_查询\_功能**](irp-mn-query-capabilities.md)对设备的请求。 如果**UniqueID**是**FALSE**，即插即用管理器，从而增强了实例 ID 添加设备的父有关的信息，从而造成 ID 唯一的计算机上。 在这种情况下总线驱动程序不应采用额外的步骤以使其设备的实例 Id 的全局唯一;只需返回相应的功能信息和操作系统处理它。

当总线驱动程序可以提供的全局唯一 ID 的每个子设备，如的序列号，总线驱动程序为 BusQueryInstanceID 指定这些字符串，并指定**UniqueID**的值**TRUE**中响应[ **IRP\_MN\_查询\_功能**](irp-mn-query-capabilities.md)对每个设备的请求。

**指定 BusQueryHardwareIDs 和 BusQueryCompatibleIDs**

总线驱动程序提供 BusQueryHardwareIDs 值和 BusQueryCompatibleIDs 允许安装程序以找到适合的总线子设备的驱动程序。

总线驱动程序响应每个请求使用 REG\_多\_SZ 描述设备的 Id 列表。 以字符为单位的 Id，包括两个 NULL 字符终止列表中，列表的最大长度是 REGSTR\_VAL\_最大\_HCID\_LEN。

返回多个时*硬件 ID*和/或多个*兼容 ID*，总线驱动程序应列出了按顺序最具体到最常规的 Id，以便选择最佳的驱动程序匹配设备。 硬件 Id 列表中的第一个条目是设备的最具体说明，并在这种情况下，它是通常与相同设备 id。

安装程序会检查针对 INF 文件中列出可能的匹配项的 Id 的 Id。 安装程序首先会扫描硬件 Id 列表，然后兼容 Id 列表。 早期的项将被视为更具体的设备，以及更高版本设备的更多常规 （并因此非最佳） 匹配项的说明。 如果未找到匹配的硬件 Id 列表中，安装程序可能会移动到的兼容 Id 列表之前提示用户提供安装介质。

请参阅[插](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)处理的常规规则[即插即用次要 Irp](plug-and-play-minor-irps.md)。

**指定 BusQueryContainerIDs**

从 Windows 7 开始，总线驱动程序应提供一个字符串，包含 BusQueryContainerID[容器 ID](https://docs.microsoft.com/windows-hardware/drivers/install/container-ids)设备。 容器 ID 允许操作系统进行分组从单个可移动的物理设备的所有功能的设备。 例如，可移动的多功能设备中的所有功能的设备具有相同的容器 id。 有关报告在特殊情况下，如卷设备可能跨多个容器中的多个磁盘，但不属于任何容器，容器 Id 详细信息请参阅[概述的容器 Id](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-container-ids)。

可移动的物理设备指总线驱动程序指定的子设备**可移动**的功能**TRUE**响应[ **IRP\_MN\_查询\_功能**](irp-mn-query-capabilities.md)请求。 有关详细信息**可移动**值，请参阅[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)。

总线驱动程序创建基于设备提供的特定于总线的唯一 ID 的容器 ID。 有关详细信息，请参阅[生成如何容器 Id](https://docs.microsoft.com/windows-hardware/drivers/install/how-container-ids-are-generated)。

该驱动程序必须使该 IRP 请求失败，并将**IoStatus.Status**于状态\_不\_支持如果以下任何条件成立：

-   设备不支持特定于总线的唯一 ID 的总线驱动程序可以使用生成的容器 id。

-   总线驱动程序之前已指定**可移动**的功能**FALSE**响应[ **IRP\_MN\_查询\_功能**](irp-mn-query-capabilities.md)对设备的请求。

**发送此 IRP**

通常情况下，仅 PnP 管理器将发送此 IRP。

若要获取的设备硬件 Id 或兼容 Id，请调用[ **IoGetDeviceProperty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceproperty)而不是发送此 IRP。

驱动程序可能会发送此 IRP，若要检索其设备之一的实例 ID。 例如，考虑其函数执行不会独立运行多功能 ISA 即插即用设备。 PnP 管理器可枚举函数作为单独的设备，但是此类设备的驱动程序可能需要将一个或多个函数相关联。 即插即用 ISA 保证唯一实例 ID，因为这样的多功能设备的驱动程序可以使用实例 Id 来查找驻留在同一设备的函数。 此类设备的驱动程序还必须通过调用获取设备的枚举器名称[ **IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceproperty)来确认该设备是即插即用 ISA 设备。

请参阅[处理 Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)有关发送 Irp 信息。 专门针对此 IRP 可以采用以下步骤：

-   IRP 的下一步 I/O 堆栈位置中设置的值： 设置**MajorFunction**到[ **IRP\_MJ\_PNP**](irp-mj-pnp.md)，将**MinorFunction**到 IRP\_MN\_查询\_ID，并设置**Parameters.QueryId.IdType**到**BusQueryInstanceID**。

-   设置**IoStatus.Status**于状态\_不\_受支持。

除了发送查询 ID IRP，驱动程序必须调用[ **IoGetDeviceProperty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceproperty)若要获取**DevicePropertyEnumeratorName**设备。

IRP 完成，该驱动程序完成了 ID 后，该驱动程序必须释放处理查询 IRP 驱动程序返回的 ID 结构。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h 中 （包括 wdm.h 中、 Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[设备标识字符串](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings)

[**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceproperty)

 

 




