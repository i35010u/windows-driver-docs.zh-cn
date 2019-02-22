---
title: 实现 UI 用于配置 APO 效果
description: 本主题介绍如何实现用户可以配置效果的用户界面 (UI)。
ms.assetid: C8D1CB20-2E77-430A-9933-4BDFFB997158
ms.date: 11/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfac675a3f9b846ca43822e1036e2947b3de20b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541897"
---
# <a name="implementing-a-ui-for-configuring-apo-effects"></a>实现 UI 用于配置 APO 效果


本主题介绍如何实现用户可以配置效果的用户界面 (UI)。 有关 a p o s 的常规信息，请参阅[音频处理对象体系结构](audio-processing-object-architecture.md)。

## <a name="span-idoverviewspanspan-idoverviewspanspan-idoverviewspanoverview"></a><span id="Overview"></span><span id="overview"></span><span id="OVERVIEW"></span>概述


APO 通常提供一个 UI，用户可以配置效果。 例如，此 UI 可以允许用户从多个不同的信号处理算法中进行选择。 Microsoft 为标准的 Windows 不提供配置 UI。 如果自定义 APO 有用户可访问的设置，开发人员必须提供相应的配置 UI。 配置 UI 安装设备驱动程序和关联的 APO 注册过程。

**请注意**  制造商可以使用自定义属性页，旨在支持其不替换此属性页。 制造商也可以选择为不具有任何用户界面，如果其自定义 APO 不具有可访问用户的设置。

 

标准的增强功能选项卡如下所示。

![演讲者属性显示的增强功能选项卡的产品/服务的四个效果，例如低音增强](images/audio-apo-enhancements-properties.png)

有三个选项可用于配置用户界面的增强功能：

1. 指定没有主键\_SYSFX\_UiClsid 根本 – 没有增强功能选项卡将显示。
2. 指定主键\_SYSFX\_UiClsid 等于为标准的内置增强功能属性页 UI-已知的 CLSID 的情况下将显示内置的增强功能选项卡。
3. 使用您自己自定义的 CLSID 创建属性页并设置主键\_SYSFX\_UiClsid 等于您自定义的 CLSID-的情况下将显示自定义选项卡。
此屏幕截图显示了 SYSVAD 交换 APO 示例的自定义属性页。

![演讲者属性显示系统效果示例提供了系统配置的效果的选项卡](images/audio-apo-speaker-properties.png)

此屏幕截图显示在控制面板中的声音小程序。

![声音属性显示耳机虚拟音频设备](images/audio-apo-sound-properties.png)

将新的属性页添加到控制面板中的声音小程序，涉及到系统提供的声音小程序中添加一个新选项卡。 这意味着，当自定义未注册和初始化，其属性页将可用以及系统提供的增强功能页。 很困难，而且复杂而无法在两个不同未的属性页之间实现通信。 就可以增强功能页上的某些默认设置将与新的属性页上的功能设置冲突。

因此此处的最实用方法是用于配置开发要替换系统提供的未自定义未实现单独的 UI。

## <a name="span-idhowtoimplementauiforconfiguringtheeffectsspanspan-idhowtoimplementauiforconfiguringtheeffectsspanspan-idhowtoimplementauiforconfiguringtheeffectsspanhow-to-implement-a-ui-for-configuring-the-effects"></a><span id="How_to_Implement_a_UI_for_Configuring_the_Effects"></span><span id="how_to_implement_a_ui_for_configuring_the_effects"></span><span id="HOW_TO_IMPLEMENT_A_UI_FOR_CONFIGURING_THE_EFFECTS"></span>如何配置效果实现用户界面


音频终结点的属性存储提供了系统效果的 UI APO 的 CLSID。 音频的控制面板项从的音频的终结点的当前上下文中获取此 CLSID。 当音频控制面板项启动相应的自定义系统影响 UI 时，它将其传递的音频的终结点。 用户界面可以访问终结点属性存储读取和调整属性的设置。 属性存储通知也注册 UI 应在其他程序中修改的设置的情况下。

如果您使用自定义 APO 设计**CBaseAudioProcessingObject**基本类和包含系统提供不，您可以替换默认属性页。

Microsoft 提供了控制面板上的声音小程序的增强功能属性页。 这是与系统提供的系统效果 APO 相关联的默认属性页。 供应商可以通过实现和注册自定义属性页提供程序使用自定义页替换此默认属性页。

请参阅[有关属性表](https://go.microsoft.com/fwlink/p/?linkid=106006)有关如何替换增强功能的属性页的信息。

若要设计和实现自定义属性页提供程序时，执行以下步骤。

1.  创建自定义属性页。 请参阅[创建属性表](https://go.microsoft.com/fwlink/p/?linkid=106006)有关详细信息。

2.  打包为 DLL 的属性页。 请参阅[创建和使用 DLL](https://go.microsoft.com/fwlink/p/?linkid=106014)打包为 DLL 自定义页面的详细信息的主题。

3.  修改你[INF 文件](https://msdn.microsoft.com/library/windows/hardware/ff549520)以安装并注册属性页的 DLL。

    下面的 INF 文件片段演示如何修改 INF 文件以注册自定义属性页。

    ```inf
    [SysFx.AddReg]
    ...
    HKR,"FX\\0",%PKEY_SYSFX_UiClsid%,,%SYSFX_UI_CLSID%
    ...
    [Strings]
    PKEY_SYSFX_UiClsid = "{D04E05A6-594B-4FB6-A80D-01AF5EED7D1D},3"
    SYSFX_UI_CLSID     = "{YOUR GUID GOES HERE}"
    ```

    并且由于前面的 INF 文件说明，安装过程修改相应的注册表项，如下所示。

    ```text
    HKLM
     SOFTWARE
      Microsoft
      Windows
       CurrentVersion
      MMDevices
      Audio
       Render
      Endpoint
      FXProperties
       ...
      "{D04E05A6-594B-4FB6-A80D-01Af5EED7D1D},3"=
                         "{YOUR CLSID GOES HERE}"
    ```

    默认属性页的 CLSID 将被替换为自定义属性页的 CLSID。

4.  在全局 AddReg 部分 INF 文件中，com 注册 CLSID

    示例 INF 文件部分，摘自 SYSVAD tabletaudiosample.inf 文件，演示如何执行此操作。 \[SWAPAPO。AddReg\]部分位于全局 AddReg 部分。 \[SWAPAPO。I.Association0.AddReg\] AddReg 部分的一部分为特定 KSCATEGORY\_音频接口。

    ```inf
    [SWAPAPO.AddReg]
    …

    ; Effects UI page COM registration
    HKCR,CLSID\%FX_UI_CLSID%,,,"CplPage Class"
    HKCR,CLSID\%FX_UI_CLSID%\InProcServer32,,,%11%\PropPageExt.dll
    HKCR,CLSID\%FX_UI_CLSID%\InProcServer32,ThreadingModel,,"Apartment"
    …

    [SWAPAPO.I.Association0.AddReg]
    …

    HKR,FX\0,%PKEY_FX_UserInterfaceClsid%,,%FX_UI_CLSID%

    …
    [Strings]
    FX_UI_CLSID     = "{YOUR GUID GOES HERE}"
     
    ```

**使用或包装 windows 效果**

如果要直接使用 Windows 提供效果，或将它们封装，，完成以下步骤：

1.  按照上面的步骤 3，效果属性存储区中注册您的 CLSID。

2.  按照以上步骤 4，以向 COM 注册 CLSID 此外，您将需要调用通过提供的 wdmaudio.inf *Include*并*需要*语句中将 INF 文件如下所示。

    ```cpp
    [YourGlobalSection]
    Include=wdmaudio.inf
    Needs=mssysfx.CopyFilesAndRegister
    ```

## <a name="span-idsysvadswapapouisamplecodespanspan-idsysvadswapapouisamplecodespanspan-idsysvadswapapouisamplecodespansysvad-swapapo-ui-sample-code"></a><span id="SYSVAD_SwapAPO_UI_Sample_Code"></span><span id="sysvad_swapapo_ui_sample_code"></span><span id="SYSVAD_SWAPAPO_UI_SAMPLE_CODE"></span>SYSVAD SwapAPO UI 示例代码


使用 SYVAD 交换 APO 代码示例作为模板可加速自定义 APO 开发过程。 有关交换 APO 示例的常规信息，请参阅[实现音频处理对象](implementing-audio-processing-objects.md)。

**示例代码**

有六个项目 SYSVAD 示例 PropPageExtensions 项目中的包含一个示例 APO 属性页的示例代码。

|                    |                                                            |
|--------------------|------------------------------------------------------------|
| **Project**        | **描述**                                            |
| PropPageExtensions | 例如自定义属性页 UI 扩展插件示例的代码 |

 

下面的代码示例可查看在开发自定义 UI。

|                         |                                                                                                      |
|-------------------------|------------------------------------------------------------------------------------------------------|
| **名称**                | **描述**                                                                                      |
| SwapPropPage.cpp        | CSwapPropPage 类的实现                                                            |
| CplExt.cpp              | 控制面板扩展 DLL 导出的实现                                       |
| UIWidgets.cpp           | CUIWidget 和派生的类的实现                                                      |
| AdvEndpointPropPage.cpp | CAdvEndpointPropPage 的实现                                                               |
| Parts.cpp               | CPart 和派生的类的实现。                                                         |
| TopologyExaminers.cpp   | 用于支持检查音频拓扑中的，例如连接器和终结点的方法的实现。 |

 

属性页扩展示例中使用以下标头文件。

|                       |
|-----------------------|
| **名称**              |
| swapproppage.h        |
| uiwidgets.h           |
| advendpointproppage.h |
| parts.h               |
| topologyexaminers.h   |

 

若要熟悉 PropPageExtensions 示例，可能想要查看标头，然后检查与属性页上定义文本相关的源代码。 如果您的要求是类似于示例代码提供，你可能能够重复使用很多代码创建和更新的自定义 UI 页。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题
[音频处理对象体系结构](audio-processing-object-architecture.md)  
[Windows 音频处理对象](windows-audio-processing-objects.md)  
[实现音频处理对象](implementing-audio-processing-objects.md)  



