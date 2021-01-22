---
title: 音频的通用 Windows 驱动程序
description: 在 Windows 10 中，你可以编写一个通用音频驱动程序，该驱动程序将跨多种硬件类型工作。
ms.date: 10/18/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4779e059c36d4f31b8b92f45a0ebb48040e029b2
ms.sourcegitcommit: 5ee1712829b7e9bc5614863b2e3af30222241ffd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2021
ms.locfileid: "98687708"
---
# <a name="universal-windows-drivers-for-audio"></a>音频的通用 Windows 驱动程序

在 Windows 10 中，你可以编写一个通用音频驱动程序，该驱动程序将跨多种硬件类型工作。 本主题讨论此方法的优点以及不同平台之间的差异。 除了适用于音频的通用 Windows 驱动程序外，Windows 还会继续支持以前的音频驱动程序技术，如 WDM。

## <a name="getting-started-with-universal-windows-drivers-for-audio"></a>适用于音频的通用 Windows 驱动程序的入门

Ihv 可以开发一个通用 Windows 驱动程序，该驱动程序可在所有设备上工作， (台式机、笔记本电脑、平板电脑、手机) 。 这可以缩短初始开发和更高版本代码维护的开发时间和成本。

这些工具可用于开发通用 Windows 驱动程序支持：

- Visual Studio 2015 支持：存在将 "目标平台" 设置为 "通用" 的驱动程序设置。 有关设置驱动程序开发环境的详细信息，请参阅 [具有通用 Windows 驱动程序的入门](/windows-hardware/drivers)。

- APIValidator 工具：可以使用 ApiValidator.exe 工具验证驱动程序调用的 Api 对通用 Windows 驱动程序是否有效。 此工具是适用于 Windows 10 的 Windows 驱动程序工具包 (WDK) 的一部分，如果使用的是 Visual Studio 2015，则会自动运行。 有关详细信息，请参阅 [验证通用 Windows 驱动程序](/windows-hardware/drivers)。

- 更新了 DDI 参考文档：正在更新 DDI 引用文档以指示通用 Windows 驱动程序支持哪些 DDIs。 有关详细信息，请参阅 [音频设备参考](/previous-versions/ff536192(v=vs.85))。

## <a name="create-a-universal-audio-driver"></a>创建通用音频驱动程序

有关分步指南，请参阅 [使用通用 Windows 驱动程序入门](/windows-hardware/drivers)。 下面是这些步骤的摘要：

1. 加载通用音频 sysvad 示例，以用作通用音频驱动程序的起点。 或者，从空的 WDM 驱动程序模板开始，并根据音频驱动程序的需要从通用 sysvad 示例中添加代码。

2. 在项目属性中，将 "目标平台" 设置为 "通用"。

3. 创建安装包：如果你的目标是运行 Windows 10 for desktop edition (Home、Pro、Enterprise 和教育) 的设备，请使用可配置的 INF 文件。 如果目标是运行 Windows 10 移动版的设备，请使用 PkgGen 生成 spkg 文件。

4. 构建、安装、部署和调试适用于 Windows 10 的驱动程序以用于桌面版或 Windows 10 移动版。

## <a name="sample-code"></a>代码示例

Sysvad 和 SwapAPO 已转换为通用 Windows 驱动程序示例。 有关详细信息，请参阅 [示例音频驱动程序](sample-audio-drivers.md)。

## <a name="available-programming-interfaces-for-universal-windows-drivers-for-audio"></a>适用于音频的通用 Windows 驱动程序的可用编程接口

从 Windows 10 开始，驱动程序编程接口是 OneCoreUAP 的 Windows 版本的一部分。 通过使用该公用集，可以编写通用 Windows 驱动程序。 对于桌面版和 Windows 10 移动版以及其他 Windows 10 版本，这些驱动程序将在 Windows 10 上运行。

使用通用音频驱动程序时，可以使用以下 DDIs。

- [音频驱动程序事件集](./audio-drivers-event-sets.md)

- [音频驱动程序接口](./audio-drivers-interfaces.md)

- [音频驱动程序属性集](./audio-drivers-property-sets.md)

- [音频驱动程序结构](./audio-drivers-structures.md)

- [音频拓扑节点](./audio-topology-nodes.md)

- [高清音频 DDI 参考](./high-definition-audio-ddi-reference.md)

- [端口类音频驱动程序参考](./port-class-audio-driver-reference.md)

## <a name="convert-an-existing-audio-driver-to-a-universal-windows-driver"></a>将现有音频驱动程序转换为通用 Windows 驱动程序

按照此过程将现有音频驱动程序转换为通用 Windows 驱动程序。

1. 确定现有的驱动程序调用是否将在 OneCoreUAP Windows 上运行。 查看引用页的 "要求" 部分。 有关详细信息，请参阅 [音频设备参考](/previous-versions/ff536192(v=vs.85))。

2. 将驱动程序重新编译为通用 Windows 驱动程序。 在项目属性中，将 "目标平台" 设置为 "通用"。

3. 使用 ApiValidator.exe 工具验证驱动程序调用的 DDIs 对通用 Windows 驱动程序是否有效。 此工具是适用于 Windows 10 的 Windows 驱动程序工具包 (WDK) 的一部分，如果使用的是 Visual Studio 2015，则会自动运行。 有关详细信息，请参阅 [验证通用 Windows 驱动程序](/windows-hardware/drivers)。

4. 如果驱动程序调用的接口不是 OneCoreUAP 的一部分，编译器会显示错误。

5. 将这些调用替换为备用调用，或创建代码解决方法或编写新的驱动程序。

## <a name="creating-a-componentized-audio-driver-installation"></a>创建组件化音频驱动程序安装

### <a name="overview"></a>概述

若要创建更流畅、更可靠的安装体验并更好地支持组件服务，请将驱动程序安装过程划分为以下组件。

- 如果存在) 和编解码器，则 DSP (
- APO
- OEM 自定义

（可选）可以将单独的 INF 文件用于 DSP 和编解码器。

此图汇总了组件化音频安装。

![显示 DSP 驱动程序编解码器的组件化音频堆栈](images/audio-componentized-stack-diagram.png)

单独的扩展 INF 文件用于为特定系统自定义每个基本驱动程序组件。 自定义包括优化参数和其他特定于系统的设置。 有关详细信息，请参阅 [使用扩展 INF 文件](../install/using-an-extension-inf-file.md)。

扩展 INF 文件必须是通用 INF 文件。 有关详细信息，请参阅[使用通用 INF 文件](../install/using-a-universal-inf-file.md)。

有关使用 INF 文件添加软件的信息，请参阅 [使用组件 INF 文件](../install/using-a-component-inf-file.md)。

### <a name="submitting-componentized-inf-files"></a>正在提交组件化 INF 文件

APO INF 包必须单独从基础驱动程序包提交到合作伙伴中心。 有关创建包的详细信息，请参阅 [WINDOWS HLK 入门](/windows-hardware/test/hlk/getstarted/windows-hlk-getting-started)。

### <a name="sysvad--componentized-inf-files"></a>SYSVAD 组件化 INF 文件

若要查看组件化 INF 文件的示例，请查看 Github 上的 [sysvad/TabletAudioSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad/TabletAudioSample)。

| 文件名                              | 说明                                                                    |
|----------------------------------------|--------------------------------------------------------------------------------|
| ComponentizedAudioSample .inf           | 基本组件化示例音频 INF 文件。                                  |
| ComponentizedAudioSampleExtension .inf  | 具有其他 OEM 自定义的 sysvad 基础的扩展驱动程序。   |
| ComponentizedApoSample .inf             | APO 示例扩展 INF 文件。                                              |

SYSVAD 示例中仍提供了传统的 INF 文件。

| 文件名                      | 说明                                                                    |
|--------------------------------|--------------------------------------------------------------------------------|
| tabletaudiosample .inf          | 一个 desktop monolitic INF 文件，其中包含安装驱动程序所需的所有信息。 |

### <a name="apo-vendor-specific-tuning-parameters-and-feature-configuration"></a>APO 供应商特定优化参数和功能配置

必须通过扩展 INF 包安装所有 APO 的供应商系统特定的设置、参数和优化值。 在许多情况下，可以使用 [INF AddReg 指令](../install/inf-addreg-directive.md)简单地执行此方法。 在更复杂的情况下，可以使用优化文件。  

基本驱动程序包不能依赖于这些自定义，因此 (功能，尽管当然，) 的功能可能会降低。  

### <a name="uwp-audio-settings-apps"></a>UWP 音频设置应用

若要实现最终用户 UI，请使用硬件支持应用 (适用于 Windows 通用音频驱动程序的 HSA) 。  有关详细信息，请参阅 [硬件支持应用 (HSA) ：驱动程序开发人员的步骤](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md)。

### <a name="programmatically-launching-uwp-hardware-support-apps"></a>以编程方式启动 UWP 硬件支持应用

若要以编程方式启动 UWP 硬件支持应用（基于驱动程序事件） (例如，在将新的音频设备连接到) 时，请使用 Windows Shell Api。 Windows 10 Shell Api 支持基于资源激活或直接通过 [IApplicationActivationManager](/windows/win32/api/shobjidl_core/nf-shobjidl_core-iapplicationactivationmanager-activateapplication)启动 UWP UI 的方法。 可在 [自动启动 Windows 10 UWP 应用](/windows/uwp/xbox-apps/automate-launching-uwp-apps#launch-activation)中找到有关自动启动 uwp 应用程序的更多详细信息。  

### <a name="apo-and-device-driver-vendor-use-of-the-audiomodules-api"></a>APO 和设备驱动程序供应商使用 AudioModules API

音频模块 API/DDI 设计用于标准化通信传输 (而不是协议) ，用于在 UWP 应用程序或用户模式服务之间传递到内核驱动程序模块或 DSP 处理块的命令。 音频模块需要驱动程序，该驱动程序实现正确的 DDI 以支持模块枚举和通信。 命令作为二进制传递，解释/定义留给创建者。  

音频模块目前并未设计用于方便在音频引擎中运行的 UWP 应用和 SW APO 之间进行直接通信。

有关音频模块的详细信息，请参阅 [实现音频模块通信](./implementing-audio-module-communication.md) 和 [配置和查询音频设备模块](./configure-and-query-audiodevicemodules.md)。

### <a name="apo-hwid-strings-construction"></a>APO HWID 字符串构造  

APO 硬件 Id 结合了标准信息和供应商定义的字符串。

它们按如下方式构造：

```syntax
SWC\VEN_v(4)&AID_a(4)&SUBSYS_ n(4)s(4) &REV_r(4)
SWC\VEN_v(4)&AID_a(4)&SUBSYS_ n(4)s(4)
SWC\VEN_v(4)&AID_a(4)
```

其中：

-  (4) 为 APO 设备供应商提供4个字符的标识符。 这将由 Microsoft 管理。  
-  (4) 是 APO 供应商定义的 APO 的4个字符的标识符。  
- n (4) 是由四个字符组成的 PCI SIG 为父设备的子系统供应商指定的标识符。 这通常是 OEM 标识符。
- s (4) 是父设备的由4个字符供应商定义的子系统标识符。 这通常是 OEM 产品标识符。

### <a name="plug-and-play-inf-version-and-date-evaluation-for-driver-update"></a>用于驱动程序更新的即插即用 INF 版本和日期评估

Windows 即插即用系统评估日期和驱动程序版本，以确定存在多个驱动程序时要安装的驱动器。  有关详细信息，请参阅 [Windows 如何对驱动程序进行排名](../install/how-setup-ranks-drivers--windows-vista-and-later-.md)。

若要允许使用最新的驱动程序，请确保并更新每个新版本的驱动程序的日期和版本。

### <a name="apo-driver-registry-key"></a>APO 驱动程序注册表项

对于第三方定义的音频驱动程序/APO 注册表项，请使用 HKR （HKLM\System\CurrentControlSet. 除外）

### <a name="use-a-windows-service-to-facilitate-uwp---apo-communication"></a>使用 Windows 服务来促进 UWP < > APO 通信

管理用户模式组件（例如，如果你的设计包含 RPC 服务器来帮助 UWP < > APO 通信），则不一定需要 Windows 服务，我们建议在 Windows 服务中实现该功能，然后控制在音频引擎中运行的 APO。  

## <a name="building-the-sysvad-universal-audio-sample-for-windows-10-desktop"></a>构建适用于 Windows 10 桌面版的 Sysvad 通用音频示例

完成以下步骤以生成适用于 Windows 10 桌面的 sysvad 示例。

1. 找到桌面 inf 文件 ("tabletaudiosample") 并将制造商名称设置为一个值，例如 "Contoso"

2. 在解决方案资源管理器中，选择并按住 (或右键单击) 解决方案 "sysvad"，然后选择 "Configuration Manager"。 如果要部署到64位版本的 Windows，请将目标平台设置为 x64。 请确保所有项目的配置和平台设置都相同。

3. 生成 sysvad 解决方案中的所有项目。

4. 从生成中查找生成的输出目录。 例如，它可能位于如下目录中：

   ```cmd
   C:\Program Files (x86)\Windows Kits\10\src\audio\sysvad\x64\Debug\package
   ```

5. 导航到 WDK 安装中的 "工具" 文件夹，并找到 PnpUtil 工具。 例如，在以下文件夹中查找： C： \\ Program Files (x86) \\ Windows 工具包 \\ 10 \\ 工具 \\ x64 \\PnpUtil.exe。

6. 将以下文件复制到要安装 sysvad 驱动程序的系统：

|文件|说明|
|----|----|
| TabletAudioSample.sys      | 驱动程序文件。                                                                  |
| tabletaudiosample .inf      |  (INF) 包含安装驱动程序所需的信息的信息。 |
| sysvad.cat                 | 目录文件。                                                                 |
| SwapAPO.dll                | 用于管理的 UI 的示例驱动程序扩展插件。                                |
| PropPageExt.dll            | 属性页的驱动程序扩展示例。                                    |
| KeywordDetectorAdapter.dll | 示例关键字检测器。                                                        |

## <a name="install-and-test-the-driver"></a>安装并测试驱动程序

按照以下步骤使用目标系统上的 PnpUtil 安装驱动程序。

1. 打开管理员命令提示符，并在复制驱动程序文件的目录中键入以下命令。

    **pnputil-i-a tabletaudiosample**

2. Sysvad 驱动程序安装应已完成。 如果有任何错误，可以检查此文件以了解其他信息： `%windir%\inf\setupapi.dev.log`

3. 在 Device Manager 的 "视图" 菜单上，选择 "设备（按类型）"。 在设备树中，找到 "Microsoft 虚拟音频设备 (WDM) -Sysvad 示例。 这通常位于 "声音、视频和游戏控制器" 节点下。

4. 在目标计算机上，打开 "控制面板"，并导航到 " **硬件和声音** &gt; **管理音频设备**"。 在 "声音" 对话框中，选择标记为 Microsoft 虚拟音频设备 (WDM) -Sysvad 示例的扬声器图标，然后选择 "设置默认值"，但不要选择 "确定"。 这会使 "声音" 对话框处于打开状态。

5. 在目标计算机上找到 MP3 或其他音频文件，然后双击以播放该文件。 然后在 "声音" 对话框中，验证与 Microsoft 虚拟音频设备 (WDM) -Sysvad 示例驱动程序关联的卷级别指示器中是否存在活动。

