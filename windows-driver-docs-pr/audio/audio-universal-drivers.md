---
title: 音频的通用 Windows 驱动程序
description: Windows 10 中，您可以编写一个通用的音频驱动程序，即可适用于许多类型的硬件。
ms.assetid: F4B56B3F-792F-4887-AF0F-FFC1F000CB8F
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 795050c4d65f5be9d98dfc14572bd782bcb5d751
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333943"
---
# <a name="universal-windows-drivers-for-audio"></a>音频的通用 Windows 驱动程序

Windows 10 中，您可以编写一个通用的音频驱动程序，即可适用于许多类型的硬件。 本主题讨论了这种方法，以及不同平台之间的差异的好处。 除了音频的通用 Windows 驱动程序，Windows 将继续支持以前的音频驱动程序技术，例如 WDM。

## <a name="getting-started-with-universal-windows-drivers-for-audio"></a>开始使用通用 Windows 驱动程序音频

Ihv 可以开发适用于所有设备 （台式计算机、 便携式计算机、 平板电脑、 手机） 的通用 Windows 驱动程序。 这可能会减少开发时间和进行初始开发和更高版本的代码维护的成本。

这些工具可以用来开发通用 Windows 驱动程序支持：

- Visual Studio 2015 的支持：没有要将"目标平台"设置为等于"世界"的驱动程序设置。 有关设置驱动程序开发环境的详细信息，请参阅[通用 Windows 驱动程序入门](https://msdn.microsoft.com/windows-drivers/develop/getting_started_with_universal_drivers)。

- APIValidator 工具：你可以使用 ApiValidator.exe 工具验证你的驱动程序调用的 API 是否对通用 Windows 驱动程序有效。 此工具是一部分适用于 Windows 10 的 Windows Driver Kit (WDK)，如果您使用的 Visual Studio 2015 将自动运行。 有关详细信息，请参阅[验证通用 Windows 驱动程序](https://msdn.microsoft.com/windows-drivers/develop/validating_universal_drivers)。

- 更新的 DDI 参考文档：正在更新 DDI 参考文档，以指示哪些 DDIs 支持通用 Windows 驱动程序。 有关详细信息，请参阅[音频设备引用](https://msdn.microsoft.com/library/windows/hardware/ff536192)。

## <a name="create-a-universal-audio-driver"></a>创建通用的音频驱动程序

有关分步指南，请参阅[通用 Windows 驱动程序入门](https://msdn.microsoft.com/windows-drivers/develop/getting_started_with_universal_drivers)。 下面是这些步骤的摘要：

1. 加载通用音频 sysvad 示例使用作为起始点的通用音频驱动程序。 或者，空 WDM 驱动程序模板开始，并根据需要为音频驱动程序代码中添加通用 sysvad 示例。

2. 在项目属性中，设置为"通用"的目标平台。

3. 创建安装包：如果你的目标是运行 Windows 10 桌面版 （主页、 专业版、 企业版和教育版），使用可配置的 INF 文件的设备。 如果你的目标是运行 Windows 10 移动版的设备，使用 PkgGen 生成.spkg 文件。

4. 构建、 安装、 部署和调试驱动程序适用于 Windows 10 桌面版或 Windows 10 移动版。

## <a name="sample-code"></a>示例代码

Sysvad 和 SwapAPO 都已转换为通用 Windows 驱动程序示例。 有关详细信息，请参阅[示例音频驱动程序](sample-audio-drivers.md)。

## <a name="available-programming-interfaces-for-universal-windows-drivers-for-audio"></a>音频的通用 Windows 驱动程序可用编程接口

从 Windows 10 开始，驱动程序的编程接口是基于 OneCoreUAP 的 Windows 版本的一部分。 通过使用该通用组，可以编写通用 Windows 驱动程序。 这些驱动程序将运行在同时面向桌面版本的 Windows 10 和 Windows 10 移动版和其他 Windows 10 版本。

使用通用的音频驱动程序时，为以下 DDIs 都是可用。

- [音频驱动程序的事件集](https://msdn.microsoft.com/library/windows/hardware/ff536195)

- [音频驱动程序接口](https://msdn.microsoft.com/library/windows/hardware/ff536196)

- [音频驱动程序的属性集](https://msdn.microsoft.com/library/windows/hardware/ff536197)

- [音频驱动程序结构](https://msdn.microsoft.com/library/windows/hardware/ff536198)

- [音频拓扑节点](https://msdn.microsoft.com/library/windows/hardware/ff536219)

- [高清晰度音频 DDI 引用](https://msdn.microsoft.com/library/windows/hardware/ff536445)

- [端口类音频驱动程序参考](https://msdn.microsoft.com/library/windows/hardware/ff537764)

## <a name="convert-an-existing-audio-driver-to-a-universal-windows-driver"></a>将现有的音频驱动程序转换为通用 Windows 驱动程序

请按照此过程将现有的音频驱动程序转换为通用 Windows 驱动程序。

1. 确定是否将在 OneCoreUAP Windows 上运行现有的驱动程序调用。 检查引用页的要求部分。 有关详细信息请参阅[音频设备引用](https://msdn.microsoft.com/library/windows/hardware/ff536192)。

2. 作为通用 Windows 驱动程序，重新编译您的驱动程序。 在项目属性中，设置为"通用"的目标平台。

3. 使用 ApiValidator.exe 工具验证 DDIs 驱动程序调用适用于通用 Windows 驱动程序。 此工具是一部分适用于 Windows 10 的 Windows Driver Kit (WDK)，如果您使用的 Visual Studio 2015 将自动运行。 有关详细信息，请参阅[验证通用 Windows 驱动程序](https://msdn.microsoft.com/windows-drivers/develop/validating_universal_drivers)。

4. 如果该驱动程序调用不属于 OneCoreUAP 的接口，则编译器将显示错误。

5. 这些调用替换为备用的调用，或创建代码解决此问题，或编写新的驱动程序。

## <a name="creating-a-componentized-audio-driver-installation"></a>创建组件化的音频驱动程序安装

### <a name="overview"></a>概述

若要创建更流畅、 更可靠的安装体验并更好地支持组件服务，将驱动程序安装过程分为以下组件。

- DSP （如果存在） 和编解码器
- APO
- OEM 自定义

（可选） 单独的 INF 文件可以用于 DSP 和编解码器。

此关系图概述了组件化音频安装。

![组件化音频堆栈显示 DSP 驱动程序编解码器和 a p o s](images/audio-componentized-stack-diagram.png)

单独的扩展 INF 文件用于自定义特定系统每个基础驱动程序组件。 自定义项包括优化参数和其他特定于系统的设置。 有关详细信息，请参阅[使用扩展 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/using-an-extension-inf-file)。

扩展 INF 文件必须是通用的 INF 文件。 有关详细信息，请参阅[使用通用 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-universal-inf-file)。

有关添加使用 INF 文件的软件的信息，请参阅[使用组件 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-component-inf-file)。

### <a name="submitting-componentized-inf-files"></a>提交组件化的 INF 文件

APO INF 包，必须提交到合作伙伴中心单独从基础驱动程序包。 有关创建包的详细信息，请参阅[Windows HLK Getting Started](https://docs.microsoft.com/windows-hardware/test/hlk/getstarted/windows-hlk-getting-started)。

### <a name="sysvad--componentized-inf-files"></a>SYSVAD 组件化 INF 文件

若要查看检查的组件化 INF 文件示例[sysvad/TabletAudioSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad/TabletAudioSample)，Github 上。

| 文件名                              | 描述                                                                    |
|----------------------------------------|--------------------------------------------------------------------------------|
| ComponentizedAudioSample.inf           | 基本组件化的示例音频 INF 文件中。                                  |
| ComponentizedAudioSampleExtension.inf  | 与其他 OEM 自定义基 sysvad 扩展驱动程序。   |
| ComponentizedApoSample.inf             | APO 的示例扩展 INF 文件。                                              |

传统的 INF 文件继续 SYSVAD 示例中提供。

| 文件名                      | 描述                                                                    |
|--------------------------------|--------------------------------------------------------------------------------|
| tabletaudiosample.inf          | 桌面 monolitic INF 文件，其中包含所有所需安装驱动程序的信息。 |
| phoneaudiosample.inf           | 包含所有所需安装驱动程序的信息是 phone monolitic INF 文件。   |

### <a name="apo-vendor-specific-tuning-parameters-and-feature-configuration"></a>APO 供应商特定优化参数和功能配置

通过扩展 INF 包，必须安装所有 APO 供应商系统的特定设置、 参数和优化值。 在许多情况下，这可以执行与使用简单的方式[INF AddReg 指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)。 在更复杂的情况下，可以使用的优化的文件。  

基本驱动程序包必须不依赖于这些自定义才能正常 （但当然功能可能会降低）。  

### <a name="programmatically-launching-uwp-hardware-support-apps"></a>以编程方式启动 UWP 硬件支持应用程序

若要以编程方式启动 UWP 硬件支持应用程序中，基于驱动程序事件 （例如，在新的音频设备连接时），请使用 Windows Shell Api。 Windows 10 Shell Api 支持一种方法启动 UWP 用户界面基于资源激活或通过直接[IApplicationActivationManager](https://msdn.microsoft.com/library/windows/desktop/hh706903.aspx)。 您可以找到更多详细信息中的 UWP 应用程序自动启动[自动启动的 Windows 10 UWP 应用](https://docs.microsoft.com/windows/uwp/xbox-apps/automate-launching-uwp-apps#launch-activation)。  

### <a name="apo-and-device-driver-vendor-use-of-the-audiomodules-api"></a>APO、 设备驱动程序供应商使用 AudioModules API

音频模块 API/DDI 旨在标准化 UWP 应用程序或对内核驱动程序模块或 DSP 处理块的用户模式服务之间的通信传输 （但不是协议） 传递的命令。 音频模块要求使用实现正确的 DDI 以支持模块枚举和通信的驱动程序。 命令将以二进制形式传递，解释/定义应由创建者。  

音频模块当前不用于促进 UWP 应用，并在音频引擎中运行 SW APO 之间直接进行通信。

有关音频模块的详细信息，请参阅[实现音频模块通信](https://docs.microsoft.com/windows-hardware/drivers/audio/implementing-audio-module-communication)并[配置和查询音频设备模块](https://docs.microsoft.com/windows-hardware/drivers/audio/configure-and-query-audiodevicemodules)。

### <a name="apo-hwid-strings-construction"></a>APO HWID 字符串构造  

APO 硬件 Id 合并标准信息和供应商定义的字符串。

按如下所示构造：

```syntax
APO\VEN_v(4)&AID_a(4)&SUBSYS_ n(4)s(4) &REV_r(4)
APO\VEN_v(4)&AID_a(4)&SUBSYS_ n(4)s(4)
APO\VEN_v(4)&AID_a(4)
```

其中：

- v(4) 是 APO 设备供应商的 4 个字符标识符。 这将由 Microsoft 管理。  
- a(4) 是针对 APO，由 APO 供应商定义的 4 个字符标识符。  
- n(4) 是父设备子系统的供应商的 4 个字符 PCI SIG 分配标识符。 这通常是 OEM 标识符。
- s(4) 是父设备的 4 个字符供应商定义的子系统标识符。 这通常是 OEM 产品标识符。

### <a name="plug-and-play-inf-version-and-date-evaluation-for-driver-update"></a>有关驱动程序更新的即插即用和播放 INF 版本和日期计算

Windows 即插即用和播放系统会评估日期和驱动程序版本以确定哪一个驱动器时存在多个驱动程序安装。  有关详细信息，请参阅[如何 Windows Ranks Drivers](https://docs.microsoft.com/windows-hardware/drivers/install/how-setup-ranks-drivers--windows-vista-and-later-)。

若要允许的最新的驱动程序使用，请确保并更新的日期和版本，每个新版本的驱动程序。

### <a name="apo-driver-registry-key"></a>APO 驱动程序注册表项

对于第三方定义音频驱动程序/APO 注册表项，请使用 HKR HKLM\System\CurrentControlSet 除外。

### <a name="use-a-windows-service-to-facilitate-uwp---apo-communication"></a>使用 Windows 服务来帮助进行 UWP <>-APO 通信

Windows 服务不是为管理用户模式组件，如不是绝对必需，但是，如果您的设计包括 RPC 服务器以便 UWP <>-APO 通信，我们建议实现的功能在 Windows 服务，然后控制 APO 的音频引擎中运行。  

## <a name="building-the-sysvad-universal-audio-sample-for-windows10-desktop"></a>Windows 10 桌面版为构建 Sysvad 世界音频示例

完成以下步骤生成 sysvad 示例对 Windows 10 桌面版。

1. 找到的桌面的 inf 文件 (tabletaudiosample.inf) 并将制造商名称设置为一个值，例如"Contoso"

2. 在解决方案资源管理器，右键单击解决方案 sysvad，并选择 Configuration Manager。 如果要部署到 64 位版本的 Windows，则将目标平台设置为 x64。 请确保配置和平台设置是相同的所有项目。

3. 生成所有 sysvad 解决方案中的项目。

4. 找到生成中生成的输出目录。 例如它可能位于如下目录中：

   ```cmd
   C:\Program Files (x86)\Windows Kits\10\src\audio\sysvad\x64\Debug\package
   ```

5. 导航到 WDK 安装中的工具文件夹并找到 PnpUtil 工具。 例如，在以下文件夹中查看：C:\\程序文件 (x86)\\Windows 工具包\\10\\工具\\x64\\PnpUtil.exe。

6. 将以下文件复制到你想要安装 sysvad 驱动程序的系统：

|                            |                                                                                   |
|----------------------------|-----------------------------------------------------------------------------------|
| TabletAudioSample.sys      | 驱动程序文件中。                                                                  |
| tabletaudiosample.inf      | 一个包含安装驱动程序所需信息的信息 (INF) 文件。 |
| sysvad.cat                 | 目录文件。                                                                 |
| SwapAPO.dll                | UI 来管理未一个示例驱动程序扩展。                                |
| PropPageExt.dll            | 属性页上一个示例驱动程序扩展。                                    |
| KeywordDetectorAdapter.dll | 示例关键字检测程序。                                                        |

## <a name="install-and-test-the-driver"></a>安装和测试驱动程序

请按照这些步骤安装在目标系统上使用 PnpUtil 的驱动程序。

1. 打开管理员命令提示符和复制到驱动程序文件的目录中的以下类型。

    **pnputil -i -a tabletaudiosample.inf**

2. 应完成 sysvad 驱动程序安装。 如果有任何错误，您可以检查此文件以获取其他信息： `%windir%\inf\setupapi.dev.log`

3. 在设备管理器中，在视图菜单上选择按类型列出的设备。 在设备树中，找到 Microsoft 虚拟音频设备 (WDM)-Sysvad 示例。 这通常是在声音、 视频和游戏控制器节点下。

4. 在目标计算机上，打开控制面板，并导航到**硬件和声音** &gt; **管理音频设备**。 声音对话框中选择标记为作为 Microsoft 虚拟音频设备 (WDM)-Sysvad 示例的扬声器图标，然后单击设为默认值，但不是单击确定。 这将保持声音对话框打开。

5. 查找 MP3 或目标计算机上的其他音频文件，然后双击以播放它。 然后在声音对话框，验证关联的 Microsoft 虚拟音频设备 (WDM)-Sysvad 示例驱动程序在卷级别指示器中没有活动。

## <a name="building-the-sysvad-universal-audio-sample-for-windows10-mobile"></a>生成 Windows 10 移动版 Sysvad 世界音频示例

完成以下步骤适用于 Windows 10 移动设备生成 sysvad 示例。

1. 找到移动 inf 文件 (phoneaudiosample.inf)，将设置一个值，例如"Contoso"的制造商名称

2. 生成 sysvad 解决方案中的以下项目：

   - EndPointsCommon

   - PhoneAudioSample

3. 找到从生成的输出目录。 例如，默认值的 Visual Studio 中的位置可以位于如下目录中：

   ```cmd
   C:\Program Files (x86)\Windows Kits\10\src\audio\sysvad\x64\Debug\package`
   ```

4. 遵循中的指导[创建包](https://msdn.microsoft.com/library/dn756642)创建包含移动映像的驱动程序文件的包。

5. 若要安装移动驱动程序包 （.spkg 文件），您需要将程序包合并到一个移动的 OS 映像。 使用 ImgGen.spkg 驱动程序包添加到可以然后刷新为移动设备的完整闪存更新 (FFU) 映像。 可能需要删除移动的映像，以允许进行测试的 sysvad 虚拟音频驱动程序中存在其他音频驱动程序。

6. 运行后的 OS 映像包含驱动程序包、 播放的声音剪辑和验证 sysvad phone 音频示例正常工作。 您可以建立监视移动设备上的 sysvad 虚拟驱动程序的内核调试程序连接。