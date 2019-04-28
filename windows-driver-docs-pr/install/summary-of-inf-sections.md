---
title: INF 节摘要
description: INF 节摘要
ms.assetid: a9d4691b-4429-456b-a5d2-482ccd0a2845
keywords:
- INF 文件 WDK 设备安装，部分
- 部分 WDK INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32335accd55ea8f78b088d11a1322773069458db
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339667"
---
# <a name="summary-of-inf-sections"></a>INF 节摘要





下表汇总了可以 INF 文件中使用的系统定义的部分。 系统定义的节名称不区分大小写。 例如，**版本**，**版本**，并**版本**都是 INF 文件中的有效部分名称。

本部分介绍它们通常在大多数设备 INF 文件中显示的相同顺序中的 INF 文件部分。 但是，这些部分实际上可以指定任何任意顺序。 Windows 将查找每个 INF 文件中的所有部分按节名不是按顺序排列，是否系统定义的或 INF 编写器定义。

<a href="" id="version-section"></a>[**版本部分**](inf-version-section.md)  
这是为每个 INF 文件所需的节。 对于 Windows 2000 和更高版本的 Windows 上的安装，此部分必须具有有效**签名**条目。

<a href="" id="signatureattributes-section"></a>[**SignatureAttributes 部分**](inf-signatureattributes-section.md)  
INF 此节定义一组文件要嵌入的签名作为硬件认证的一部分。 这些附加签名所需的设备具有某些特殊的需求。 示例包括受保护的环境媒体的播放、 早期启动反恶意软件和第三方 HAL 扩展。

<a href="" id="sourcedisksnames-section"></a>[**SourceDisksNames 部分**](inf-sourcedisksnames-section.md)  
本部分是必需的如果 INF 文件具有相应**SourceDisksFiles**部分。 本部分需从分发媒体包含在打包产品中安装 IHV/OEM-提供设备及其驱动程序。 它还需要安装以下任一此类的 INF 文件：

- 辅助安装程序 DLL 以补充系统提供的设备类安装程序或共同安装程序的操作 (另请参阅<em>DDInstall</em>**。共同安装程序**此列表中更高版本)

- 新的类安装程序 DLL 来补充 OS 的设备安装程序的操作 (另请参阅**ClassInstall32**)

本部分介绍的各个源分发磁盘或 CD-ROM 光盘进行安装。 与此相反，系统提供 INF 文件每个指定**LayoutFile**中的条目及其**版本**部分，并提供详细说明的源分发内容和布局的至少一个其他 INF 文件若要安装的所有软件组件。

<a href="" id="sourcedisksfiles-section"></a>[**SourceDisksFiles 部分**](inf-sourcedisksfiles-section.md)  
此部分标识要从分发介质安装到目标计算机上的目标的文件的位置。 具有本部分的 INF 文件还必须具有**SourceDisksNames**部分。

<a href="" id="destinationdirs-section"></a>[**DestinationDirs 部分**](inf-destinationdirs-section.md)  
设备/驱动程序 INF 文件具有**DestinationDirs**部分以指定默认目标目录为 INF 指定的文件副本分发媒体上提供了或 INF 布局文件中列出。 本部分是必需的除非该 INF 文件将安装的设备，如调制解调器或显示器，具有除其 INF 安装该程序的任何文件。

<a href="" id="controlflags-section"></a>[**ControlFlags 部分**](inf-controlflags-section.md)  
此部分控制是否使用 INF 文件只是为了从分发介质传输文件。

通常情况下，大多数设备驱动程序和系统类安装程序的 INF 文件具有本部分中，因此它们可以排除的至少一个子集*模型*可手动安装的设备，若要向最终用户显示的列表中的项。 仅安装即插即用设备的 INF 文件禁止显示所显示的所有特定于模型的信息。

<a href="" id="manufacturer-section"></a>[**制造商部分**](inf-manufacturer-section.md)  
设备和其驱动程序的 INF 文件中需要此部分。

**制造商**因为其项的每个引用 INF-编写器定义的系统设备类 INF 部分有时称为"表的内容，"*模型*部分，其中，反过来，引用其他 INF 编写器定义部分中，如每个模型的输入*DDInstall*部分中， <em>DDInstall</em>**。服务**部分中，等等。

<a href="" id="models-section--per-manufacturer-entry--"></a>[**模型部分**](inf-models-section.md) (每个**制造商**条目)   
本部分需确定为其 INF 文件将安装驱动程序的设备。 它指定一组设备、 设备 ID 和名称的通用名称 （字符串） 之间的映射*DDInstall*部分中，包含该设备的安装说明的 INF 文件中的其他位置。

为单个提供程序安装一个或多个设备和驱动程序的 INF 文件必须只有一个*模型*部分中，但系统 INF 文件，查找设备类都可以具有许多 INF 编写器定义*模型*部分。

<a href="" id="ddinstall-section--per-models-entry--"></a>[***DDInstall*一节**](inf-ddinstall-section.md) (每个*模型*条目)   
实际安装任何设备中列出的所需的此部分*模型*INF 文件，以及每个此类设备的驱动程序中的部分。 一个*DDInstall*可由多个共享部分*模型*部分。

<a href="" id="ddinstall-services-section"></a>[***DDInstall *。服务部分**](inf-ddinstall-services-section.md)  
从 Microsoft Windows 2000 开始，此部分是必需的因为的扩展*DDInstall*大多数内核模式设备驱动程序的部分。 这包括 （例外情况是调制解调器和显示监视器的 INF 文件） 的任何 WDM 驱动程序。 它控制如何以及何时启动的特定驱动程序的服务，其依赖项 （如果有） 基础旧，等等。 本部分还设置了事件日志记录服务的设备驱动程序如果它支持事件日志记录。

<a href="" id="ddinstall-hw-section"></a>[***DDInstall *。硬件部分**](inf-ddinstall-hw-section.md)  
此可选部分添加特定于设备的 (并且通常情况下，独立于驱动程序的) 信息写入注册表或从注册表中，可能是多功能设备或安装一个或多个即插即用的筛选器驱动程序中删除此类信息。

<a href="" id="ddinstall-coinstallers-section"></a>[***DDInstall *。共同安装程序部分**](inf-ddinstall-coinstallers-section.md)  
**请注意**  如果要构建一个通用或移动设备的驱动程序包，此部分无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

此可选部分注册一个或多个特定于设备的共同安装程序分发媒体上提供了用于补充或将现有的设备类安装的系统的设备安装程序的操作。

辅助安装程序是一个 IHV/OEM 提供的 Win32 DLL，它通常将写入注册表的其他配置信息或执行其他安装任务的需要时不可用的动态生成的特定于计算机的信息创建设备的 INF 文件。 有关详细信息，请参阅[编写共同安装程序](writing-a-co-installer.md)。

<a href="" id="ddinstall-factdef-section"></a>[***DDInstall *。FactDef 部分**](inf-ddinstall-factdef-section.md)  
**请注意**  如果要构建一个通用或移动设备的驱动程序包，此部分无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

本部分应包含在任何手动安装的非 PnP 设备 INF 文件。 它指定出厂默认硬件配置设置，如总线相对 I/O 端口、 IRQ （如果有） 和等的卡。

<a href="" id="ddinstall-logconfigoverride-section"></a>[***DDInstall *。LogConfigOverride 部分**](inf-ddinstall-logconfigoverride-section.md)  
**请注意**  如果要构建一个通用或移动设备的驱动程序包，此部分无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

本部分用于创建[重写配置](https://msdn.microsoft.com/library/windows/hardware/ff547012#logical-configuration-types-for-resource-requirements-lists)，这会重写插设备的总线驱动程序报告的硬件资源要求。

<a href="" id="ddinstall-interfaces-section"></a>[***DDInstall *。接口部分**](inf-ddinstall-interfaces-section.md)  
如果驱动程序将导出的设备接口类，因此创建的接口类，如内核流式处理静止图像捕获或数据解压缩，新实例的功能其 INF 文件可以有本部分中。

<a href="" id="interfaceinstall32-section"></a>[**InterfaceInstall32 部分**](inf-interfaceinstall32-section.md)  
如果要安装的组件，如新的类驱动程序，提供了一个或多个新[设备接口类](device-interface-classes.md)到更高级的组件，其 INF 文件具有此部分。 实际上，本部分会引导通过设置所需使用接口类提供的功能的一组设备接口的新类。

<a href="" id="defaultinstall-section"></a>[**DefaultInstall 部分**](inf-defaultinstall-section.md)  
INF 文件的**DefaultInstall**将访问部分，如果用户的 INF 文件的名称上右键单击后选择"安装"菜单项。

<a href="" id="defaultinstall-services-section"></a>[**DefaultInstall.Services 部分**](inf-defaultinstall-services-section.md)  
本部分等同于[ **INF DDInstall.Services 部分**](inf-ddinstall-services-section.md)，并使用与建立关联[ **INF DefaultInstall 部分**](inf-defaultinstall-section.md).

<a href="" id="strings-section"></a>[**字符串部分**](inf-strings-section.md)  
本部分中的每个 INF 文件需要定义每个**%** <em>strkey</em> **%** INF 中指定的令牌。 按照约定，**字符串**部分 (或如果 INF 提供了一组特定于区域设置的部分**字符串**部分) 显示在以便于维护和本地化的所有系统提供 INF 文件中最后一个。

某些部分在此处列出，尤其是具有*安装*在其名称中可以包含引用 INF 编写器定义的其他部分的指令。 每个指令会导致在安装过程中的相应类型 INF 编写器定义部分的下方列出的项上执行特定操作。

有效的条目和以前列表中任何特定部分的指令集是部分特定于和为每个这些部分引用的正式语法中所示。 此外，请参阅[摘要的 INF 指令](summary-of-inf-directives.md)摘要最常用的指令。

括在 unbolded 方括号，例如显示可选条目和每个此类部分中的指令：

**\[版本\]** ...\[**提供程序 = %**<em>INF 创建者</em>**%** \] ...**提供程序**中的条目**\[版本\]** 部分是可选的意义上说，它不是每个 INF 文件中的必需项。

 

 





