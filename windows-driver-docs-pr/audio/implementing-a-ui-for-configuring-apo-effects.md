---
title: 实现用于配置 APO 效果的 UI
description: 本主题介绍如何实现允许用户配置效果的用户界面（UI）。
ms.assetid: C8D1CB20-2E77-430A-9933-4BDFFB997158
ms.date: 10/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: d5fef103f27a884bb808e99878e8a511b3b17617
ms.sourcegitcommit: bff7fdcac628f8b62bd9df2658ca56301d1f8b07
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2019
ms.locfileid: "72030804"
---
# <a name="implementing-a-ui-for-configuring-apo-effects"></a>实现用于配置 APO 效果的 UI

本主题介绍如何实现允许用户配置效果的用户界面（UI）。 有关的一般信息，请参阅[音频处理对象体系结构](audio-processing-object-architecture.md)。

## <a name="span-idoverviewspanspan-idoverviewspanspan-idoverviewspanoverview"></a><span id="Overview"></span><span id="overview"></span><span id="OVERVIEW"></span>概述

> [!NOTE]
> Windows 10 版本1809和 PropPageExtensions 项目不再出现在 Sysvad 示例中后，不再支持此自定义项。 对于更高版本的 Windows，推荐的方法是创建硬件支持应用。 有关详细信息，请参阅[硬件支持应用 (HSA)：适用于驱动程序开发人员的步骤](https://docs.microsoft.com/windows-hardware/drivers/devapps/hardware-support-app--hsa--steps-for-driver-developers)。
>

APO 通常提供允许用户配置效果的 UI。 例如，可以通过此 UI 从几个不同的信号处理算法中进行选择。 Microsoft 为标准 Windows 用户提供了一个配置 UI。 如果自定义 APO 具有用户可访问的设置，则开发人员必须提供相应的配置 UI。 配置 UI 与设备驱动程序一起安装，并由注册过程与 APO 关联。

**请注意**   制造商可以将此属性页替换为设计用于支持其所在用户的自定义属性页。 如果自定义 APO 没有用户可访问的设置，则制造商也可以选择不包含任何 UI。

"标准增强功能" 选项卡如下所示。

![显示四个效果（如低音增强）的 "扬声器属性" 显示 "增强" 选项卡](images/audio-apo-enhancements-properties.png)

有三个选项可用于配置增强 UI：

1. 指定 no PKEY @ no__t-0SYSFX @ no__t-1UiClsid all –不会显示任何增强选项卡。
2. 指定 PKEY @ no__t-0SYSFX @ no__t-1UiClsid 等于标准内置增强属性页 UI 的已知 CLSID-将显示内置的增强功能选项卡。
3. 创建自己的属性页，并将其设置为自定义 CLSID，并将 PKEY @ no__t-0SYSFX @ no__t-1UiClsid 设置为等于自定义 CLSID-将显示自定义选项卡。
此屏幕截图显示了 SYSVAD Swap APO 示例的自定义属性页。

![显示系统效果的扬声器属性示例选项卡提供系统效果配置](images/audio-apo-speaker-properties.png)

此屏幕截图显示控制面板中的 "声音" 小程序。

![显示耳机虚拟音频设备的声音属性](images/audio-apo-sound-properties.png)

将新属性页添加到控制面板中的 "声音" 小程序，这涉及到向系统提供的声音小程序添加新的选项卡。 这意味着，当注册并初始化自定义的时，它们的属性页将与系统提供的增强功能页面一起使用。 跨两个不同的属性页实现通信是非常困难且复杂的。 "增强" 页上的某些默认设置可能会与新属性页上的功能设置发生冲突。

因此，最实用的方法是实现单独的 UI，用于配置为替换系统提供的中所开发的自定义。

## <a name="span-idhow_to_implement_a_ui_for_configuring_the_effectsspanspan-idhow_to_implement_a_ui_for_configuring_the_effectsspanspan-idhow_to_implement_a_ui_for_configuring_the_effectsspanhow-to-implement-a-ui-for-configuring-the-effects"></a><span id="How_to_Implement_a_UI_for_Configuring_the_Effects"></span><span id="how_to_implement_a_ui_for_configuring_the_effects"></span><span id="HOW_TO_IMPLEMENT_A_UI_FOR_CONFIGURING_THE_EFFECTS"></span>如何实现用于配置效果的 UI


系统效果的 UI APO 的 CLSID 可从音频终结点的属性存储中获取。 "音频控制面板" 项从当前位于上下文的音频终结点获取此 CLSID。 当 "音频控制面板" 项启动适当的自定义系统效果 UI 时，它会将它传递给音频终结点。 然后，UI 可以访问终结点属性存储区来读取和调整属性设置。 UI 还应注册属性存储通知，以防其他某个程序修改设置。

如果使用**CBaseAudioProcessingObject**基类设计自定义 APO 并包装系统提供的 "中"，则可以替换默认属性页。

Microsoft 为控制面板上的 "声音" 小程序提供了增强属性页。 这是与系统提供的系统效果 APO 关联的默认属性页。 供应商可以通过实现和注册自定义属性页提供程序，将此默认属性页替换为自定义页。

有关如何替换增强属性页面的信息，请参阅[关于属性表](https://go.microsoft.com/fwlink/p/?linkid=106006)。

若要设计和实现自定义属性页提供程序，请执行以下步骤。

1. 创建自定义属性页。 有关详细信息，请参阅[创建属性表](https://go.microsoft.com/fwlink/p/?linkid=106006)。

2. 将你的属性页打包为一个 DLL。 有关将自定义页打包为 DLL 的详细信息，请参阅[创建和使用 dll](https://go.microsoft.com/fwlink/p/?linkid=106014)主题。

3. 修改[INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-inf-files)，为属性页安装和注册 DLL。

    以下 INF 文件片段显示了如何修改 INF 文件来注册自定义属性页。

    ```inf
    [SysFx.AddReg]
    ...
    HKR,"FX\\0",%PKEY_SYSFX_UiClsid%,,%SYSFX_UI_CLSID%
    ...
    [Strings]
    PKEY_SYSFX_UiClsid = "{D04E05A6-594B-4FB6-A80D-01AF5EED7D1D},3"
    SYSFX_UI_CLSID     = "{YOUR GUID GOES HERE}"
    ```

    作为上述 INF 文件说明的结果，安装过程将修改相应的注册表项，如下所示。

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

    默认属性页的 CLSID 将替换为自定义属性页的 CLSID。

4. 在 INF 文件的全局 AddReg 部分中，将 CLSID 注册到 COM。

    从 SYSVAD tabletaudiosample 文件中获取的示例 INF 文件部分显示了如何执行此操作。 0SWAPAPO. AddReg @ no__t 节位于 global AddReg 部分中。 @no__t 对于特定 ADDREG @ KSCATEGORY-NO__T 接口，\[SWAPAPO. Association0. AddReg @ no__t 是2AUDIO 节的一部分。

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

**使用或环绕 windows 效果**

如果直接使用 Windows 提供的效果或将其换行，请完成以下步骤：

1. 按照上面的步骤3操作，在 "效果" 属性存储中注册 CLSID。

2. 按照上述步骤4，将 CLSID 注册到 COM。 此外，还需要通过 INF 文件中的*Include 和 Include*语句来调用提供的*wdmaudio，如下*所示。

    ```cpp
    [YourGlobalSection]
    Include=wdmaudio.inf
    Needs=mssysfx.CopyFilesAndRegister
    ```

## <a name="span-idsysvad_swapapo_ui_sample_codespanspan-idsysvad_swapapo_ui_sample_codespanspan-idsysvad_swapapo_ui_sample_codespansysvad-swapapo-ui-sample-code"></a><span id="SYSVAD_SwapAPO_UI_Sample_Code"></span><span id="sysvad_swapapo_ui_sample_code"></span><span id="SYSVAD_SWAPAPO_UI_SAMPLE_CODE"></span>SYSVAD SwapAPO UI 示例代码


使用 SYVAD Swap APO 代码示例作为模板，可以加快自定义 APO 开发过程。 有关 SWAP APO 示例的常规信息，请参阅[实现音频处理对象](implementing-audio-processing-objects.md)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[音频处理对象体系结构](audio-processing-object-architecture.md)  
[Windows 音频处理对象](windows-audio-processing-objects.md)  
[实现音频处理对象](implementing-audio-processing-objects.md)  
