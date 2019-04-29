---
title: V4 驱动程序安装的概念
description: V4 打印驱动程序模型使用新的安装程序模型来改善用户体验并降低支持成本。
ms.assetid: C1DF5496-14CF-4BF4-B85C-AF1A691C7AF2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29bd4610f1957bf8fe27ceb848a07a22f4a1f2c2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324845"
---
# <a name="v4-driver-setup-concepts"></a>V4 驱动程序安装的概念


V4 打印驱动程序模型使用新的安装程序模型来改善用户体验并降低支持成本。

V4 打印驱动程序是直接从驱动程序存储区，这消除了文件冲突的可能性并提高安装性能运行。 V4 安装模型仍会继续使用 INF 文件，但还使用了新的清单文件以捕获打印机特定的安装程序指令。

## <a name="device-identifiers"></a>设备标识符


**CompatibleID**。 CompatibleIDs 是打印类驱动程序的一个关键概念，因为它们使驱动程序以支持发布新版本的 Windows，而无需更新的驱动程序之后发布的设备。 这可能是因为 CompatibleIDs 使设备能够比 HardwareID 播发不太具体的打印驱动程序的支持。

如果打印类驱动程序已支持特定 CompatibleID，v4 打印驱动程序不应指定它再次。 如果打印驱动程序的日期晚于打印类驱动程序日期，打印驱动程序将自动下载从 Windows 更新站点。

设备应包括 CompatibleIDs 其 1284ID 字符串中。 如果现有的打印类驱动程序支持设备，然后打印驱动程序应使用，CompatibleID，否则我们建议使用以下格式。

1284\_CID\_&lt;制造商标识符&gt;\_&lt;PDL 标识符&gt;\_设备系列标识符

例如：1284\_CID\_FA\_PCL5e\_Laser

如果已在现有设备中实现 CompatibleIDs，打印驱动程序应继续使用这些 CompatibleIDs。

CompatibleIDs 不使用基于 IP 的打印设备的安装中。 因此，用户将需要确定相应的驱动程序使用的驱动程序的名称。 在打印类驱动程序有，我们建议制造商提供其网站上的兼容性列表的任何设备的打印类驱动程序支持。 有关如何实现 CompatibleIDs 硬件，包括完整的规则和限制，列表中的详细信息请参阅[如何在打印设备中实现兼容 Id](https://msdn.microsoft.com/library/windows/hardware/gg463313.aspx)。

为了支持多个制造商无关 （标准） 打印类驱动程序，Microsoft 才支持几个标准 CompatibleIDs。 下表显示了这些标准 CompatibleIDs 和其关联的 PDL 文件类型。

| PDL 文件类型      | 标准 CompatibleID |
|--------------------|-----------------------|
| XPS                | 1284\_CID\_MS\_XPS    |
| OpenXPS (ECMA 388) | 1284\_CID\_MS\_OXPS   |
| PCL6               | 1284\_CID\_MS\_PCL6   |
| PS                 | 1284\_CID\_MS\_PS     |

 

这些标准打印类驱动程序支持只有一小组功能，因此选择利用这些类驱动程序的制造商应实现增强的驱动程序配置中，使用 Bidi 添加更多特定纸张大小和配置。 下表显示的功能和关联的标准打印类驱动程序支持的选项。

| 功能    | 选项           |
|------------|-------------------|
| 纸张大小 | 字母 A4        |
| 分辨率 | 300 dpi，600 dpi    |
| 媒体类型 | 普通纸       |
| 每张多       | 1, 2, 4, 6, 9, 16 |

 

**PrinterDriverID**。 PrinterDriverID 是一个新的标识符，用于确定打印机共享，以及驱动程序和打印机扩展之间的兼容性的驱动程序之间的兼容性。 例如，如果在服务器上的驱动程序在其清单文件中指定 PrinterDriverID，然后共享该驱动程序连接到此打印机的客户端将搜索本地驱动程序存储区和 Windows 更新的驱动程序，指定在相同的 PrinterDriverID其驱动程序 INF。 如果找到匹配项，则将使用该驱动程序执行的连接。 客户端计算机不筛选使用驱动程序名称的匹配结果。

PrinterDriverID 必须按以下方式指定所有兼容的驱动程序：

-   V4 清单中使用 PrinterDriverID 指令。

-   作为在 v4 驱动程序 INF HardwareID。

对于两个不同的驱动程序共享同一 PrinterDriverID，它们必须是兼容的共享。 若要始终是成功的连接，两个驱动程序必须能够执行以下操作：

-   支持同一 PDL

-   使用相同类型的配置文件 （GPD 或 PPD）

-   要能够呈现任何功能或服务器驱动程序的 GPD、 PPD 和/或约束 JS 文件中指定的选项

-   支持的相同打印机扩展

后台处理程序不会验证这些限制，并且仅依赖 PrinterDriverID 来指示两个驱动程序是否兼容的共享。 制造商必须确保要更改的驱动程序 PrinterDriverID，如果未对任何上述各项进行更改。

打印机扩展还可以与通过 PrinterDriverIDs 驱动程序相关联。 因此，两个共享 PrinterDriverID 的驱动程序必须同时使用相同的打印机扩展。 安装的最后一个打印机扩展将覆盖任何以前的打印机扩展适用于所有设备使用目标的 PrinterDriverIDs，因此必须使用相同的应用程序正常。

**使用 Guid 的最佳实践**。 通过 v4 打印驱动程序模型，最值得注意的是在 PrinterDriverID 和 PrinterExtensionID、 事件 Id 和 ModelID 中广泛使用的 Guid。 这些可以用于唯一地标识不同的项在系统中，或它们标识为为了维护、 共享等相同。

在创建新的 Guid 时，始终使用 GUID 生成器，如包含在 Microsoft Visual Studio 中的一个或 SDK 中包含的一个。 手动编写 Guid 和 Guid 已错误地复制和粘贴的是容易发生冲突。

## <a name="setup-behaviors"></a>安装程序行为


**打印队列名称**。 V3 驱动程序，请打印队列名称已由驱动程序名称，则用户首次规定。 打印类驱动程序的引入，是设备的没有多大用处用户识别的驱动程序名称。 Windows 将重命名会自动安装，如下所示运行 v4 打印驱动程序任何插设备的队列：

1. 最初，打印队列名称设置为驱动程序名称。

2. 如果该驱动程序 v4 打印驱动程序，Windows 将查询使用 Bidi 的设备。

a. 如果\\Printer.DeviceInfo:FriendlyName 指定，它将用作新的队列名称。

b. 否则，将查询 Windows \\Printer.DeviceInfo:Manufacturer， \\Printer.DeviceInfo:ModelName。

i. 如果同时指定两者，Windows 会将它们串联到"制造商 ModelName"。

ii. 如果只有一个这些 Bidi 查询失败，Windows 将使用从其他查询的成功返回作为队列名称。

3. 如果所有 Bidi 查询失败，则 Windows 将使用 IEEE 1284ID 来确定的制造商和型号名称。

a. 如果指定说明或 DES，则它将用作新的队列名称。

b. 否则，Windows 将搜索制造商或制造业和模型或 MDL。

i. 如果同时指定两者，Windows 会将它们串联到"制造商模型"。

ii. 如果只有其中一种失败，Windows 将使用来自另一个密钥的值作为队列名称。

**添加打印机向导**。 驱动程序名称将继续可供用户选择中的驱动程序的唯一标识符**添加打印机向导**。 基于 IP 的设备应实现[端口监视器 MIB (PWG 5107.1 2005年)](http://www.pwg.org/standards.html)以支持 TCP/IP 自动检测。 此外，添加了打印类驱动程序使用的硬件 ID (HWID) 映射到的现有设备可能会使用特定于设备的模型名称。

## <a name="changing-ports-and-dealing-with-printer-devnodes"></a>不断变化的端口和打印机 Devnodes 处理


若要提供 UI 体验的一致性，所有的打印队列提供软件设备节点 (devnode)。 这是如何在 UI 中，发现打印机，它允许虚拟打印机，连接到共享的打印机和网络打印机，以便进行枚举和访问作为插 (PnP) 打印机相同的方式。 物理即插即用打印机软件 devnodes 将从触发创建队列的即插即用 devnode 继承属性。

当两个不同的对象在相关时，UI 将到设备容器分组 devnodes。 此分组中，可以多功能打印机 (MFP) 显示为一个图标**设备和打印机**文件夹。 MFP 中的所有函数的容器 ID 必须是相同顺序对所有函数显示下相同的图标。 这是自动完成的即插即用设备。

更改与队列关联的端口会更改队列的 devnode 与关联的容器 ID。 这会导致队列要与物理设备的即插即用对象的其余部分相同的设备容器下不再进行分组。 没有足够的信息来正确地清理变得分隔队列和即插即用对象的情况下在操作系统中。 在某些情况下，这是用户的实际意图。 只有用户或更改端口名称的应用程序知道预期的结果是什么，并且用户/应用程序负责清理任何令人困惑的状态更改队列的端口后留在原地。 以下是两个示例情况下，显示了如何进行相应的清理的说明。

1. IT 管理员设置打印机 – 的 IT 管理员使用 WS 发现来查找网络上的打印机和更改为 TCP/IP 端口，因为他们喜欢其 TCP/IP 管理过程。

a. 假定条件下-此处是在设备和打印机文件夹中只有一个"设备"。

b. 解决方案，IT 管理员从设备和打印机文件夹中删除 WSD 即插即用 devnode。

2. IHV 安装软件-IHV 安装的驱动程序以及自定义端口监视器 （自定义端口监视器不允许在 v4 中，但相同的 devnode 处理适用于 v3 驱动程序）。 IHV 更改为设备制造商创建一个端口的打印队列的 USB 端口。

a. 假定条件下-此处是在设备和打印机文件夹中只有一个"设备"。

b. 解决方案\#1 – 即插即用 devnode 仍需要：安装程序更改队列 devnode 容器的 ID，用于匹配的即插即用的对象。

c. 解决方案\#2 – 即插即用 devnode 是无关：安装程序将删除原始的即插即用设备。

**驱动程序分级**。 引入的 v4 打印驱动程序不会修改插排名行为。 当在插入设备时，将选定得分最高可用的驱动程序。 如果所选驱动程序是打印类驱动程序，并且没有更好地排名，匹配的驱动程序在 Windows Update 站点上，则所选驱动程序将自动替换的下次用户下载的 Windows 更新。

有关驱动程序分级的详细信息，请参阅[如何 Windows Ranks Drivers](https://msdn.microsoft.com/library/windows/hardware/ff546225.aspx)。

## <a name="driver-setup-best-practices"></a>驱动程序安装程序的最佳实践


**打包**。 V4 打印驱动程序不使用**需要**并**包括**INF 文件指令，或若要处理共享的文件的核心驱动程序技术。 因此，v4 打印驱动程序必须是独立的但仅有少数例外。

V4 打印驱动程序可能会继续接收依赖项上常见的文件的 Windows 提供。 这些在 NTPrint.INF 或 NTPrint4.INF 中包括的文件。 驱动程序可能会包括这些文件通过指定**下，RequiredFiles**指令 v4 清单文件中。

如果存在现有打印类驱动程序为你的设备或你 PDL 提供基本的渲染功能，则还存在一种机制来创建一个依赖项的类驱动程序通过使用**RequiredClass**指令。 此指令会导致 Windows 构建使用从 v4 打印驱动程序和所需的打印类驱动程序文件的驱动程序。 与优先于更具体的文件的最特定文件合并 GPD 和 PPD 文件。 下图说明了用于合并 GPD/PPD 文件的逻辑，还包括从 Bidi 获得增强的驱动程序配置文件。 其他驱动程序文件，如 JavaScript 约束，不会合并驱动程序包中。

![gpd/ppd 文件合并逻辑](images/gpd-ppdmergelogic.png)

**打印机型号系列**。 插维护模型线上的所有 HardwareIDs 和 CompatibleIDs 隐式排名。 因此，Microsoft 建议合作伙伴应使用以下最佳实践以避免不可预知行为方面排名。

V4 打印驱动程序

1. V4 打印驱动程序 Inf 必须定义两种不同的型号系列：

a. HardwareID 代码行："驱动程序名称"= INSTALL\_部分中，busenumerator\\硬件 Id

b. PrinterDriverID 代码行："Driver name" = INSTALL\_SECTION,{GUID}

2. V4 打印驱动程序 Inf 必须在单独的行上定义特定于总线的 HardwareIDs:

a. "驱动程序名称"= INSTALL\_部分，WSDPRINT\\硬件 Id

b. " Driver name" = INSTALL\_SECTION,USBPRINT\\HardwareID

c. "驱动程序名称"= INSTALL\_部分，LPTENUM\\硬件 Id

打印类驱动程序

1. 打印类驱动程序 Inf 必须定义三种不同的型号系列：

a. HardwareID 代码行："Driver name" = INSTALL\_SECTION,HardwareID

b. PrinterDriverID 代码行："Driver name" = INSTALL\_SECTION,{GUID}

c. CompatibleID 代码行："打印类驱动程序名称"= INSTALL\_部分、 1284年\_CID\_CompatID

2. 打印类驱动程序 Inf，无需定义任何总线枚举器 (例如，WSDPRINT\)

## <a name="related-topics"></a>相关主题
[如何在打印设备中实现兼容 Id](https://msdn.microsoft.com/library/windows/hardware/gg463313.aspx)  
[Windows 驱动程序的级别](https://msdn.microsoft.com/library/windows/hardware/ff546225.aspx)  
[端口监视器 MIB (PWG 5107.1 2005年)](http://www.pwg.org/standards.html)  



