---
title: V4 驱动程序安装的概念
description: V4 打印驱动程序模型使用新的设置模型来改善用户体验并降低支持成本。
ms.assetid: C1DF5496-14CF-4BF4-B85C-AF1A691C7AF2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c550830ab211b64b876bcf9ad4bba835d0607005
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652858"
---
# <a name="v4-driver-setup-concepts"></a>V4 驱动程序安装的概念


V4 打印驱动程序模型使用新的设置模型来改善用户体验并降低支持成本。

V4 打印驱动程序直接从驱动程序存储区运行，这消除了文件冲突的可能性，并提高了安装性能。 V4 设置模型继续使用 INF 文件，但也使用新的清单文件来捕获打印机特定的安装指令。

## <a name="device-identifiers"></a>设备标识符


**CompatibleID**。 CompatibleIDs 是打印类驱动程序的重要概念，因为它们允许驱动程序支持在发布新版 Windows 后发布的设备，而无需更新驱动程序。 这是可能的，因为 CompatibleIDs 允许设备播发对特定于 HardwareID 的打印驱动程序的支持。

如果某个特定的 CompatibleID 已被打印类驱动程序支持，v4 打印驱动程序不应再次指定它。 如果打印驱动程序的日期比打印类驱动程序的日期新，则将从 Windows 更新站点自动下载打印驱动程序。

设备应在其1284ID 字符串中包含 CompatibleIDs。 如果现有的打印类驱动程序支持设备，则打印驱动程序应使用该 CompatibleID，否则我们建议使用以下格式。

1284\_CID\_&lt;制造商标识符&gt;\_&lt;PDL 标识符&gt;设备家族标识符

例如： 1284\_CID\_FA\_PCL5e\_激光器

如果已在现有设备中实现 CompatibleIDs，则打印驱动程序应继续使用这些 CompatibleIDs。

在基于 TCP/IP 的打印设备的安装中不使用 CompatibleIDs。 因此，用户将需要仅使用驱动程序的名称来标识适当的驱动程序。 如果使用打印类驱动程序，我们建议制造商在其网站上提供打印类驱动程序所支持的任何设备的兼容性列表。 有关如何在硬件中实现 CompatibleIDs 的详细信息，包括规则和限制的完整列表，请参阅[如何在打印设备中实现兼容 id](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn613942(v=vs.85))。

Microsoft 支持一些标准 CompatibleIDs，以便支持多个特定于制造商的（标准）打印类驱动程序。 下表显示了这些标准 CompatibleIDs 及其关联的 PDL 文件类型。

| PDL 文件类型      | 标准 CompatibleID |
|--------------------|-----------------------|
| XPS                | 1284\_CID\_MS\_XPS    |
| OpenXPS （ECMA-388） | 1284\_CID\_MS\_.OXPS   |
| PCL6               | 1284\_CID\_MS\_PCL6   |
| PS                 | 1284\_CID\_MS\_PS     |

 

这些标准打印类驱动程序仅支持一小部分功能，因此选择使用这些类驱动程序的制造商应该使用双向来添加更具体的纸张大小和配置。 下表显示了标准打印类驱动程序支持的功能和关联选项。

| 功能    | “选项”           |
|------------|-------------------|
| 纸张大小 | Letter、A4        |
| 分辨率 | 300dpi, 600dpi    |
| 介质类型 | 普通纸       |
| N 个向上       | 1，2，4，6，9，16 |

 

**PrinterDriverID**。 PrinterDriverID 是一个新的标识符，用于确定驱动程序之间的兼容性，以及驱动程序与打印机扩展之间的兼容性。 例如，如果服务器上的驱动程序在其清单文件中指定了 PrinterDriverID 并共享了驱动程序，则连接到此打印机的客户端将搜索本地驱动程序存储区，并为指定同一 PrinterDriverID 的驱动程序 Windows 更新其驱动程序 INF。 如果找到匹配项，将使用该驱动程序建立连接。 客户端计算机不使用驱动程序名称筛选匹配结果。

对于所有兼容的驱动程序，必须按以下方式指定 PrinterDriverID：

-   使用 v4 清单中的 PrinterDriverID 指令。

-   作为 v4 驱动程序 INF 中的 HardwareID。

对于共享相同 PrinterDriverID 的两个不同的驱动程序，它们必须兼容以便于共享。 为了使连接始终成功，两个驱动程序必须能够执行以下操作：

-   支持相同的 PDL

-   使用相同类型的配置文件（GPD 或 PPD）

-   能够呈现在服务器驱动程序的 GPD、PPD 和/或约束 JS 文件中指定的任何功能或选项

-   支持相同的打印机扩展

后台处理程序不会验证这些限制，而只依赖于 PrinterDriverID 来指示两个驱动程序是否与共享兼容。 如果对上述任何项进行了更改，则必须确保为驱动程序更改 PrinterDriverID。

打印机扩展还可以通过 PrinterDriverIDs 与驱动程序相关联。 因此，共享 PrinterDriverID 的两个驱动程序都必须使用相同的打印机扩展。 安装的最后一个打印机扩展将使用目标 PrinterDriverIDs 覆盖所有设备以前的所有打印机扩展，因此必须使用相同的应用程序才能正常工作。

**使用 guid 的最佳实践**。 Guid 是通过 v4 打印驱动程序模型广泛使用的，最值得注意的是，在 PrinterDriverID 中，也可以在 PrinterExtensionID、EventID 和 ModelID 中使用。 这些项可用于唯一标识系统中的不同项，或将其标识为与服务、共享等相同。

创建新的 Guid 时，请始终使用 GUID 生成器，如 Microsoft Visual Studio 中包含的 GUID 或 SDK 中包含的 GUID。 手动创建了错误复制和粘贴的 Guid 和 Guid 很容易发生冲突。

## <a name="setup-behaviors"></a>设置行为


**打印队列名称**。 对于 v3 驱动程序，首先按驱动程序名称指示打印队列名称，然后由用户指示。 随着打印类驱动程序的引入，驱动程序名称在用户识别设备时要少得多。 对于安装的任何即插即用设备，Windows 将自动重命名队列，如下所示：

1. 最初，打印队列名称设置为驱动程序名称。

2. 如果该驱动程序是 v4 打印驱动程序，Windows 将使用双向查询该设备。

a. 如果指定 \\DeviceInfo： FriendlyName，则将其用作新的队列名称。

b. 否则，Windows 将查询 \\DeviceInfo：制造商 \\： ModelName。

i. 如果同时指定两者，则 Windows 会将它们连接到 "Manufacturer ModelName"。

ii. 如果其中只有一个双向查询失败，则 Windows 将使用从另一个查询返回的成功返回作为队列名称。

3. 如果所有双向查询都失败，则 Windows 将使用 IEEE 1284ID 来确定制造商和型号名称。

a. 如果指定了 DESCRIPTION 或 DES，则将其用作新的队列名称。

b. 否则，Windows 将搜索制造商、制造和型号或 MDL。

i. 如果同时指定两者，则 Windows 会将它们连接到 "制造商型号"。

ii. 如果其中只有一个失败，则 Windows 将使用另一个键的值作为队列名称。

**"添加打印机向导"** 。 驱动程序名称将继续是用户在 "**添加打印机向导**" 中选择驱动程序的唯一标识符。 基于 TCP/IP 的设备应实现[端口监视器 MIB （PWG 5107.1-2005）](https://www.pwg.org/standards.html)以支持 tcp/ip 自动检测。 使用硬件 ID （HWID）映射添加到打印类驱动程序的现有设备可能还会使用特定于设备的模型名称。

## <a name="changing-ports-and-dealing-with-printer-devnodes"></a>更改端口和处理 Printer Devnodes


为了提供一致的 UI 体验，所有打印队列均提供了一个软件设备节点（devnode）。 这是在 UI 中发现打印机的方式，它允许以与即插即用（PnP）打印机相同的方式枚举和访问虚拟打印机、与共享打印机的连接以及网络打印机。 适用于物理 PnP 打印机的软件 devnodes 将从已触发队列创建的 PnP devnode 继承属性。

当两个不同的对象相关时，UI 会将 devnodes 分组为设备容器。 这种分组允许多功能打印机（MFP）在 "**设备和打印机**" 文件夹中显示为一个图标。 MFP 中所有函数的容器 ID 必须相同，才能使函数全部显示在相同图标下。 这是为 PnP 设备自动完成的。

更改与队列关联的端口将更改与队列的 devnode 关联的容器 ID。 这将导致队列不再与物理设备的其余 PnP 对象在同一设备容器下进行分组。 操作系统中的信息不足，无法正确清理队列和 PnP 对象之间的分离情况。 在某些情况下，这是用户的实际意图。 只有更改端口名称的用户或应用程序才会知道预期的结果，而是由用户/应用程序清理在更改队列端口后留下的任何混乱的状态。 下面是两个示例情况，其中说明了如何正确清理。

1. IT 管理员设置打印机– IT 管理员使用 WS 发现查找网络上的打印机，并将端口更改为 TCP/IP，因为它们喜欢其 TCP/IP 管理进程。

a. 预期– "设备和打印机" 文件夹中只有一个 "设备"。

b. 解决方案-IT 管理员从 "设备和打印机" 文件夹中删除 WSD PnP devnode。

2. IHV 设置软件– IHV 安装驱动程序和自定义端口监视器（在 v4 中不允许使用自定义端口监视器，但相同的 devnode 处理适用于 v3 驱动程序）。 IHV 将打印队列的 USB 端口更改为设备制造商创建的端口。

a. 预期– "设备和打印机" 文件夹中只有一个 "设备"。

b. 解决方案 \#1-仍需 PnP devnode：安装程序将更改队列 devnode 的容器 ID，使其与 PnP 对象匹配。

c. 解决方案 \#2 – PnP devnode 是无关的：安装程序删除原始 PnP 设备。

**驱动程序排名**。 V4 打印驱动程序的引入不会修改即插即用排名行为。 设备接通电源时，将选择具有最高分数的可用驱动程序。 如果所选的驱动程序是打印类驱动程序，并且在 Windows 更新站点上有更好的排名和匹配的驱动程序，则在用户下一次下载 Windows 更新时，将自动替换所选的驱动程序。

有关驱动程序排名的详细信息，请参阅[Windows 如何对驱动程序](https://docs.microsoft.com/windows-hardware/drivers/install/how-setup-ranks-drivers--windows-vista-and-later-)进行排名。

## <a name="driver-setup-best-practices"></a>驱动程序设置最佳方案


**打包**。 V4 打印驱动程序不使用这些**要求**，并**包括**INF 文件指令或核心驱动程序技术来处理共享文件。 因此，v4 打印驱动程序必须是独立的，只有几个例外。

V4 打印驱动程序可能会继续依赖于 Windows 提供的常见文件。 其中包括 Ntprint.inf 或 NTPrint4 中的文件。 驱动程序可以通过在 v4 清单文件中指定**RequiredFiles**指令来包含这些文件。

如果存在为你的设备或 PDL 提供基本呈现功能的现有打印类驱动程序，则还存在一种机制，用于通过使用**RequiredClass**指令来依赖类驱动程序。 此指令会使 Windows 使用 v4 打印驱动程序和所需的打印类驱动程序中的文件构建驱动程序。 合并了 GPD 和 PPD 文件，其中最具体的文件优先于不太具体的文件。 下图说明了用于合并 GPD/PPD 文件的逻辑，还包括从双向获取的增强驱动程序配置文件。 其他驱动程序文件（如 JavaScript 约束）不会合并到驱动程序包中。

![gpd/ppd 文件合并逻辑](images/gpd-ppdmergelogic.png)

**打印机型号线条**。 即插即用维护模型行中所有 HardwareIDs 和 CompatibleIDs 的隐式排名。 因此，Microsoft 建议合作伙伴应使用以下最佳做法，以避免在排名方面出现不可预知的行为。

V4 打印驱动程序

1. V4 打印驱动程序 Inf 必须定义两种不同类型的模型行：

a. HardwareID 行： "Driver name" = INSTALL\_节，busenumerator\\HardwareID

b. PrinterDriverID 行： "Driver name" = INSTALL\_节，{GUID}

2. V4 打印驱动程序 Inf 必须在单独的行上定义特定于总线的 HardwareIDs：

a. "Driver name" = INSTALL\_部分，WSDPRINT\\HardwareID

b. "Driver name" = INSTALL\_部分，USBPRINT\\HardwareID

c. "Driver name" = INSTALL\_部分，LPTENUM\\HardwareID

打印类驱动程序

1. 打印类驱动程序 Inf 必须定义三种不同类型的模型行：

a. HardwareID 行： "Driver name" = INSTALL\_节，HardwareID

b. PrinterDriverID 行： "Driver name" = INSTALL\_节，{GUID}

c. CompatibleID 行： "打印类驱动程序名称" = 安装\_部分，，1284\_CID\_CompatID

2. 打印类驱动程序 Inf 不得定义任何总线枚举器（例如，WSDPRINT\)

## <a name="related-topics"></a>相关主题
[如何在打印设备中实现兼容 Id](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn613942(v=vs.85))  
[Windows 排名驱动程序的方式](https://docs.microsoft.com/windows-hardware/drivers/install/how-setup-ranks-drivers--windows-vista-and-later-)  
[端口监视器 MIB （PWG 5107.1-2005）](https://www.pwg.org/standards.html)  



