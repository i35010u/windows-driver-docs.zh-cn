---
title: INF 节摘要
description: INF 节摘要
ms.assetid: a9d4691b-4429-456b-a5d2-482ccd0a2845
keywords:
- INF 文件 WDK 设备安装，部分
- 部分 WDK INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d35ac8e784246ff5e3ed596d9ff6c664f83dfd6
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89094829"
---
# <a name="summary-of-inf-sections"></a>INF 节摘要





下面汇总了可在 INF 文件中使用的系统定义的部分。 系统定义的部分名称不区分大小写。 例如， **版本**、 **版本**和 **版本** 在 INF 文件中的名称相同。

本部分介绍 INF 文件的各个部分，其顺序与它们在大多数设备 INF 文件中的显示顺序相同。 但是，可以按任意顺序指定这些部分。 Windows 按节名称（而不是按顺序）查找每个 INF 文件中的所有节，无论是由系统定义的还是由 INF 编写的。

<a href="" id="version-section"></a>[**版本部分**](inf-version-section.md)  
这是每个 INF 文件的必需部分。 若要在 Windows 2000 和更高版本的 Windows 上安装，此部分必须具有有效的 **签名** 条目。

<a href="" id="signatureattributes-section"></a>[**SignatureAttributes 部分**](inf-signatureattributes-section.md)  
INF 的此部分定义一组要在硬件认证中嵌入签名的文件。 具有某些特殊需求的设备需要其他签名。 例如，受保护的环境 media 播放、初期启动反恶意软件和第三方 HAL 扩展。

<a href="" id="sourcedisksnames-section"></a>[**SourceDisksNames 部分**](inf-sourcedisksnames-section.md)  
如果 INF 文件具有相应的 **SourceDisksFiles** 部分，则需要此部分。 此部分是从打包产品附带的分发媒体中安装 IHV/OEM 提供的设备及其驱动程序所必需的。 此类 INF 文件中也需要安装以下各项之一：

- 用于补充系统提供的设备类安装程序或共同安装程序的操作的共同安装程序 DLL (另请参阅 <em>DDInstall</em>**。** 此列表后面的 CoInstallers) 

- 用于补充操作系统设备安装程序操作的新的类安装程序 DLL (参阅 **ClassInstall32**) 

本部分标识用于安装的单个源分发磁盘或 cd-rom 光盘。 与此相反，系统提供的 INF 文件分别在其**版本**部分中指定了**LayoutFile**条目，并提供了至少一个 INF 文件，其中详细介绍了要安装的所有软件组件的源分发内容和布局。

<a href="" id="sourcedisksfiles-section"></a>[**SourceDisksFiles 部分**](inf-sourcedisksfiles-section.md)  
此部分确定要从分发媒体安装到目标计算机上目标的文件的位置。 具有此部分的 INF 文件还必须具有 **SourceDisksNames** 部分。

<a href="" id="destinationdirs-section"></a>[**DestinationDirs 部分**](inf-destinationdirs-section.md)  
设备/驱动程序 INF 文件具有 **DestinationDirs** 部分，可为 inf 指定的文件副本指定分发媒体上提供的文件副本，或在 inf 布局文件中列出。 此部分是必需的，除非 INF 文件安装的设备（例如调制解调器或显示器监视器）除其 INF 以外的其他任何文件一起安装。

<a href="" id="controlflags-section"></a>[**ControlFlags 部分**](inf-controlflags-section.md)  
本部分控制是否仅使用 INF 文件从分发媒体传输文件。

通常，适用于设备驱动程序和系统类安装程序的大多数 INF 文件都包含此部分，因此，他们可以从可供最终用户显示的可手动安装设备的列表中排除至少一部分 *模型* 条目。 仅安装 PnP 设备的 INF 文件会禁止显示所有特定于模型的信息。

<a href="" id="manufacturer-section"></a>[**制造商部分**](inf-manufacturer-section.md)  
在设备及其驱动程序的 INF 文件中需要此部分。

系统设备类 INF 的 " **制造商** " 部分有时称为 "目录"，因为它的每个条目都引用了一个 inf 写入器定义的 *模型* 部分，而后者又引用了其他由 inf 编写器定义的部分，例如，每个模型条目的 *DDInstall* 部分、 <em>DDInstall</em>**。服务** 部分等。

<a href="" id="models-section--per-manufacturer-entry--"></a>每个**制造商**条目 ([**模型部分**](inf-models-section.md))    
此部分需要标识 INF 文件为其安装驱动程序的设备。 它在 INF 文件中的其他位置（其中包含设备的安装说明），指定一组通用名称与设备 (string) 之间的映射、设备 ID 和 *DDInstall* 部分的名称。

为单个提供程序安装一个或多个设备和驱动程序的 INF 文件只能有一个 *模型* ，但设备类的系统 INF 文件可以有许多由 INF 编写器定义的 *模型* 部分。

<a href="" id="ddinstall-section--per-models-entry--"></a>[***DDInstall***](inf-ddinstall-section.md)每个*模型*条目 (节)    
此部分是实际安装 INF 文件中的 " *模型* " 部分中列出的任何设备以及每个此类设备的驱动程序所必需的。 一个 *DDInstall* 部分可由多个 *模型* 部分共享。

<a href="" id="ddinstall-services-section"></a>[***DDInstall*.服务部分**](inf-ddinstall-services-section.md)  
从 Microsoft Windows 2000 开始，此部分是扩展大多数内核模式设备驱动程序的 *DDInstall* 部分所必需的。 这包括任何 WDM 驱动程序 (例外情况是调制解调器的 INF 文件和显示器) 的监视器。 它控制启动特定驱动程序的服务的方式和时间，其依赖项 (如果任何) 在基础上，等等。 如果设备驱动程序支持事件日志记录，此部分还会通过设备驱动程序设置事件日志记录服务。

<a href="" id="ddinstall-hw-section"></a>[***DDInstall*.HW 部分**](inf-ddinstall-hw-section.md)  
此可选部分会向注册表中添加特定于驱动程序的 (和通常与驱动程序无关的) 信息，或者删除注册表中的此类信息，可能适用于多功能设备或安装一个或多个 PnP 筛选器驱动程序。

<a href="" id="ddinstall-coinstallers-section"></a>[***DDInstall*.CoInstallers 部分**](inf-ddinstall-coinstallers-section.md)  
**注意**   如果要构建通用或移动驱动程序包，此部分无效。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

此可选部分注册在分发媒体上提供的一个或多个特定于设备的共同安装程序，以补充系统设备安装程序或现有设备类安装程序的操作。

共同安装程序是一种由 IHV/OEM 提供的 Win32 DLL，通常会将额外的配置信息写入注册表，或者执行需要动态生成的计算机特定信息（在创建设备的 INF 文件时不可用）的其他安装任务。 有关详细信息，请参阅 [编写共同安装程序](writing-a-co-installer.md)。

<a href="" id="ddinstall-factdef-section"></a>[***DDInstall*.FactDef 部分**](inf-ddinstall-factdef-section.md)  
**注意**   如果要构建通用或移动驱动程序包，此部分无效。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

此部分应包含在任何手动安装的非 PnP 设备的 INF 文件中。 它指定厂家默认硬件配置设置，例如，与总线相关的 i/o 端口、IRQ (（如果有任何) ，等等）。

<a href="" id="ddinstall-logconfigoverride-section"></a>[***DDInstall*.LogConfigOverride 部分**](inf-ddinstall-logconfigoverride-section.md)  
**注意**   如果要构建通用或移动驱动程序包，此部分无效。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

此部分用于创建 [替代配置](../kernel/hardware-resources.md#logical-configuration-types-for-resource-requirements-lists)，该配置将覆盖即插即用设备的总线驱动程序报告的硬件资源要求。

<a href="" id="ddinstall-interfaces-section"></a>[***DDInstall*.接口部分**](inf-ddinstall-interfaces-section.md)  
如果驱动程序导出设备接口类的功能，从而创建接口类的新实例（如内核流式处理静止映像捕获或数据解压缩），则其 INF 文件可包含此部分。

<a href="" id="interfaceinstall32-section"></a>[**InterfaceInstall32 部分**](inf-interfaceinstall32-section.md)  
如果要安装的组件（如新的类驱动程序）将一个或多个新的 [设备接口类](./overview-of-device-interface-classes.md) 提供给更高级别的组件，则其 INF 文件将包含此部分。 实际上，此部分通过设置使用接口类提供的功能所需的任何内容，为新类引导一组设备接口。

<a href="" id="defaultinstall-section"></a>[**DefaultInstall 部分**](inf-defaultinstall-section.md)  
如果在选择并按住 (或右键单击 INF 文件名) 后，用户选择 "安装" 菜单项，则将访问 INF 文件的 **DefaultInstall** 节。

<a href="" id="defaultinstall-services-section"></a>[**DefaultInstall 部分**](inf-defaultinstall-services-section.md)  
本部分与 [**Inf DDInstall 部分**](inf-ddinstall-services-section.md)相同，并用于与 [**inf DefaultInstall 部分**](inf-defaultinstall-section.md)关联。

<a href="" id="strings-section"></a>[**字符串部分**](inf-strings-section.md)  
每个 INF 文件中都需要此部分来定义 **%** <em>strkey</em> **%** 在 inf 中指定的每个 strkey 令牌。 按照约定，如果 INF 提供一组特定于区域设置的**字符串**) 部分，则这些**字符串**部分 (或部分，以便于维护和本地化。

此处列出的某些部分（特别是在其名称中 *安装* 的部分）可以包含引用其他由 INF 编写器定义的部分的指令。 每个指令会导致在安装过程中，在相应类型的 INF 写入器定义的部分下列出的项上执行特定操作。

前面列表中任何特定部分的有效条目集和指令集都是特定于部分的，并显示在这些部分的参考的正式语法中。 此外，请参阅 [INF 指令摘要](summary-of-inf-directives.md) ，了解最常用指令的摘要。

每个此类节中的可选条目和指令显示在 unbolded 括号中，例如：

** \[ 版本 \] ** ... \[**Provider =%**<em>INF-creator</em> **%** \] .。。** \[ 版本 \] **部分中的**提供程序**条目是可选的，因为它不是每个 INF 文件中的必需条目。

 

