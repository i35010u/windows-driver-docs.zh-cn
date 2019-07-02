---
title: 实现音频处理对象
description: 本主题介绍如何实现音频处理对象 (APO)。 有关 a p o s 的常规信息，请参阅音频处理对象体系结构。
ms.assetid: 822FAF10-DAB3-48D1-B782-0C80B072D3FB
ms.date: 06/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: a34bf6b46e8420aa95d638c7a374abdf434fa8f1
ms.sourcegitcommit: 2854c02cbe5b2c0010d0c64367cfe8dbd201d3f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67499799"
---
# <a name="implementing-audio-processing-objects"></a>实现音频处理对象


本主题介绍如何实现音频处理对象 (APO)。 有关 a p o s 的常规信息，请参阅[音频处理对象体系结构](audio-processing-object-architecture.md)。

## <a name="span-idimplementingcustomaposspanspan-idimplementingcustomaposspanspan-idimplementingcustomaposspanimplementing-custom-apos"></a><span id="Implementing_Custom_APOs"></span><span id="implementing_custom_apos"></span><span id="IMPLEMENTING_CUSTOM_APOS"></span>实现自定义 a p o s


自定义不以进程内 COM 对象实现，使它们在用户模式下运行和打包在动态链接库 (DLL) 中。 有三种类型的 APO，基于他们在信号处理关系图中的插入位置。

-   Stream 效果 (SFX)
-   模式效果 (MFX)
-   终结点效果 (EFX)

每个逻辑设备可以与每种类型的一个 APO 相关联。 模式和影响的详细信息，请参阅[音频信号处理模式](audio-signal-processing-modes.md)。

可以通过使基于 CBaseAudioProcessingObject 基类，这在 Baseaudioprocessingobject.h 文件中声明的自定义类来实现 APO。 这种方法涉及到添加到要创建自定义的 APO 的 CBaseAudioProcessingObject 基本类的新功能。 CBaseAudioProcessingObject 基类实现的许多 APO 需要的功能。 它提供的默认实现的大部分中三个必需的接口的方法。 主要的例外是[ **IAudioProcessingObjectRT::APOProcess** ](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess)方法。

执行以下步骤来实现自定义未。

1.  创建自定义 APO com 对象提供所需的音频处理。
2.  根据需要创建用于配置自定义 a p o s 的用户界面。
3.  创建一个 INF 文件以安装并注册 a p o s 和自定义用户界面。

实现自定义属性页的详细信息，请参阅[对于配置 APO 效果实现 UI](implementing-a-ui-for-configuring-apo-effects.md)。 下面的屏幕快照显示了 SwapAPO 属性。

![演讲者属性显示系统效果示例提供了系统配置的效果的选项卡](images/audio-apo-speaker-properties.png)

## <a name="span-iddesignconsiderationsforcustomapodevelopmentspanspan-iddesignconsiderationsforcustomapodevelopmentspanspan-iddesignconsiderationsforcustomapodevelopmentspandesign-considerations-for-custom-apo-development"></a><span id="Design_Considerations_for_Custom_APO_Development"></span><span id="design_considerations_for_custom_apo_development"></span><span id="DESIGN_CONSIDERATIONS_FOR_CUSTOM_APO_DEVELOPMENT"></span>有关自定义 APO 开发的设计注意事项


所有自定义未必须具有以下常规特征：

-   APO 必须具有一个输入和一个输出连接。 这些连接是音频缓冲区，并且可能具有多个通道。
-   APO 可以修改仅音频数据传递给它通过其[ **IAudioProcessingObjectRT::APOProcess** ](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess)例程。 APO 不能更改基础的逻辑设备，包括其 KS 拓扑的设置。
-   除 IUnknown，不必须公开以下接口：

    - [IAudioProcessingObject](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nn-audioenginebaseapo-iaudioprocessingobject)。 处理安装程序任务，例如初始化和格式协商一个接口。

    - [IAudioProcessingObjectConfiguration](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nn-audioenginebaseapo-iaudioprocessingobjectconfiguration)。 配置界面。

    - [IAudioProcessingObjectRT](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nn-audioenginebaseapo-iaudioprocessingobjectrt)。 处理音频处理实时接口。 它可从实时处理线程调用。

    - [IAudioSystemEffects](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nn-audioenginebaseapo-iaudiosystemeffects)。 使音频引擎的接口将 DLL 识别为系统效果 APO。

- 所有未必须都具有实时系统的兼容性。 这表示：

  - 必须为非阻止性成员实现实时接口的成员的所有方法。 它们必须不能阻止、 使用分页的内存，或调用任何阻止系统例程。

  - 由 APO 处理的所有缓冲区都必须不可分页。 所有代码和进程路径中的数据必须都是不可分页。

  - 不应引入到音频处理链明显的延迟。

- 自定义未必须公开 IAudioProcessingObjectVBR 接口。

**请注意**  有关所需的接口的详细信息，请参阅 Windows 工具包中的 Audioenginebaseapo.h 和 Audioenginebaseapo.idl 文件\\&lt;内部版本号&gt;\\包括\\um 文件夹。

 

## <a name="span-idusingsamplecodetoacceleratethedevelopmentprocessspanspan-idusingsamplecodetoacceleratethedevelopmentprocessspanspan-idusingsamplecodetoacceleratethedevelopmentprocessspanusing-sample-code-to-accelerate-the-development-process"></a><span id="Using_Sample_Code_to_Accelerate_the_Development_Process"></span><span id="using_sample_code_to_accelerate_the_development_process"></span><span id="USING_SAMPLE_CODE_TO_ACCELERATE_THE_DEVELOPMENT_PROCESS"></span>使用示例代码来加速开发过程


使用 SYSVAD 交换 APO 代码示例作为模板可加速自定义 APO 开发过程。 交换示例是开发是为了说明音频处理对象的某些功能的示例。 交换 APO 示例交换具有正确的信道的左的通道，并实现 SFX 和 MFX 效果。 您可以启用和禁用通道交换音频效果使用属性对话框。

SYSVAD 音频示例位于[Windows 驱动程序示例 GitHub](https://github.com/Microsoft/Windows-driver-samples)。

您可以浏览 Sysvad 音频此处的示例：

<https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad>

**下载并从 GitHub 提取 Sysvad 音频示例**

请按照下列步骤以下载并打开 SYSVAD 示例。

a. 可以使用 GitHub 工具以使用这些示例。 此外可以下载一个 zip 文件中的通用驱动程序示例。

<https://github.com/Microsoft/Windows-driver-samples/archive/master.zip>

b. Master.zip 文件下载到本地硬盘。

c. 右键单击*Windows 驱动程序示例 master.zip*，然后选择**全部提取**。 指定新文件夹，或浏览到一个现有将存储提取的文件。 例如，可以指定*c:\\DriverSamples\\* 作为新文件将被提取到其中的文件夹。

d. 提取文件后，导航到以下子文件夹。

*C:\\DriverSamples\\音频\\Sysvad*

**在 Visual Studio 中打开驱动程序解决方案**

在 Microsoft Visual Studio 中，单击**文件** &gt; **打开** &gt; **项目/解决方案...** 并导航到包含所提取的文件的文件夹 (例如， *c:\\DriverSamples\\音频\\Sysvad*)。 双击*Sysvad*解决方案文件以将其打开。

在 Visual Studio 中找到解决方案资源管理器。 (如果尚未打开，请将此选择**解决方案资源管理器**从**视图**菜单。)在解决方案资源管理器，可以看到一个具有六个项目的解决方案。

**SwapAPO 示例代码**

SYSVAD 示例，主 APO 开发人员感兴趣的是其中之一中有五个项目。

|                    |                                       |
|--------------------|---------------------------------------|
| **Project**        | **说明**                       |
| SwapAPO            | 有关示例 APO 的示例代码。       |

 

下面总结了 Sysvad 示例中的其他项目。

|                        |                                            |
|------------------------|--------------------------------------------|
| **Project**            | **说明**                            |
| PhoneAudioSample       | 移动的音频驱动程序的示例代码。     |
| TabletAudioSample      | 另一个音频驱动程序的示例代码。 |
| KeywordDetectorAdapter | 关键字检测程序适配器的示例代码 |
| EndpointsCommon        | 公共终结点的示例代码。          |

 

SwapAPO 示例的主头文件是 swapapo.h。 下面总结了其他主代码元素。

|                      |                                                                   |
|----------------------|-------------------------------------------------------------------|
| **文件**             | **说明**                                                   |
| Swap.cpp             | C++包含交换 APO 的实现代码。        |
| SwapAPOMFX.cpp       | CSwapAPOMFX 的实现                                     |
| SwapAPOSFX.cpp       | CSwapAPOSFX 的实现                                     |
| SwapAPODll.cpp       | DLL 导出的实现。                                    |
| SwapAPODll.idl       | DLL 的 COM 接口和组件类的定义。           |
| SwapAPOInterface.idl | 交换 APO 功能的接口和类型定义。    |
| swapapodll.def       | COM 导出定义                                           |

 

## <a name="span-idimplementingthecomobjectaudioprocessingcodespanspan-idimplementingthecomobjectaudioprocessingcodespanspan-idimplementingthecomobjectaudioprocessingcodespanimplementing-the-com-object-audio-processing-code"></a><span id="Implementing_the_COM_Object_Audio_Processing_Code"></span><span id="implementing_the_com_object_audio_processing_code"></span><span id="IMPLEMENTING_THE_COM_OBJECT_AUDIO_PROCESSING_CODE"></span>实现 COM 对象音频处理代码


通过基于自定义类进行包装系统提供 APO **CBaseAudioProcessingObject**基类，该 Baseaudioprocessingobject.h 文件中声明。 这种方法涉及到引入新功能分为**CBaseAudioProcessingObject**基类，以创建自定义的 APO。 **CBaseAudioProcessingObject**基类实现的许多 APO 需要的功能。 它提供的默认实现的大部分中三个必需的接口的方法。 主要的例外是[ **IAudioProcessingObjectRT::APOProcess** ](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess)方法。

通过使用**CBaseAudioProcessingObject**，可以更轻松地实现 APO。 如果 APO 没有特殊的格式要求，并对所需的 float32 格式，包含在接口方法的默认实现**CBaseAudioProcessingObject**应该是够用的。 给定的默认实现，必须实现只有三个主要方法：[**IAudioProcessingObject::IsInputFormatSupported**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobject-isinputformatsupported)， [ **IAudioProcessingObjectRT::APOProcess**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess)，和**ValidateAndCacheConnectionInfo**.

若要开发基于你未**CBaseAudioProcessingObject**类中，执行以下步骤：

1.  创建一个类继承自**CBaseAudioProcessingObject**。

    以下C++的代码示例演示如何创建继承的类**CBaseAudioProcessingObject**。 这一概念的实际实现，请按照中的说明**音频处理对象驱动程序示例**部分以转到交换示例中，并指向*Swapapo.h*文件。

    ```cpp
    // Custom APO class - LFX
    Class MyCustomAPOLFX: public CBaseAudioProcessingObject
    {
     public:
    //Code for custom class goes here
    ...
    };
    ```

    **请注意**  因为 SFX APO 由执行的信号处理不同于由 MFX 或 EFX APO 执行的信号处理，必须为每个创建单独的类。

     

2.  实现以下三种方法：

    -   [**IAudioProcessingObject::IsInputFormatSupported**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobject-isinputformatsupported)。 此方法将处理与音频引擎格式协商。

    -   [**IAudioProcessingObjectRT::APOProcess**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess)。 此方法使用自定义算法执行信号处理。

    -   **ValidateAndCacheConnectionInfo**。 此方法分配的内存来存储格式的详细信息，例如，通道计数，采样率、 示例深度和通道掩码。

以下C++的代码示例演示一种实现[ **APOProcess** ](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess)步骤 1 中创建的示例类的方法。 这一概念的实际实现，请按照中的说明**音频处理对象驱动程序示例**部分以转到交换示例中，并指向*Swapapolfx.cpp*文件。

```cpp
// Custom implementation of APOProcess method
STDMETHODIMP_ (Void) MyCustomAPOLFX::APOProcess (...)
{
// Code for method goes here. This code is the algorithm that actually
// processes the digital audio signal.
...
}
```

下面的代码示例演示的实现**ValidateAndCacheConnectionInfo**方法。 此方法的实际实现，请按照中的说明**音频处理对象驱动程序示例**部分以转到交换示例中，并指向*Swapapogfx.cpp*文件。

```cpp
// Custom implementation of the ValidateAndCacheConnectionInfo method.
HRESULT CSwapAPOGFX::ValidateAndCacheConnectionInfo( ... )
{
// Code for method goes here.
// The code should validate the input/output format pair.
...
}
```

**请注意**  剩余的接口和方法的类继承自**CBaseAudioProcessingObject** Audioenginebaseapo.idl 文件中的详细信息中所述。

 

对于桌面 Pc，可以提供一个用户界面来配置添加到自定义 APO 的功能。 有关详细信息，请参阅[为配置未实现 UI](implementing-a-ui-for-configuring-sapos.md)。

## <a name="span-idreplacingsystem-suppliedaposspanspan-idreplacingsystem-suppliedaposspanspan-idreplacingsystem-suppliedaposspanreplacing-system-supplied-apos"></a><span id="Replacing_System-supplied_APOs"></span><span id="replacing_system-supplied_apos"></span><span id="REPLACING_SYSTEM-SUPPLIED_APOS"></span>替换系统提供 a p o s


当实现 APO 接口时，有两种方法： 可以编写您自己的实现，也可以调入收件箱 a p o s。

此伪代码演示了包装 APO 的系统。

```cpp
CMyWrapperAPO::CMyWrapperAPO {
    CoCreateInstance(CLSID_InboxAPO, m_inbox);
}

CMyWrapperAPO::IsInputFormatSupported {
    Return m_inbox->IsInputFormatSupported(…);
}
```

此伪代码说明了如何创建你自己的自定义 APO。

```cpp
CMyFromScratchAPO::IsInputFormatSupported {
    my custom logic
}
```

开发时将不替换系统提供的您必须为接口和方法在以下列表中，使用相同的名称。 一些接口具有除了列出的所需方法的更多方法。 请参阅以确定你是否想要实现的方法或仅必需的那些接口的参考页。

实现步骤的其余部分是自定义 APO 相同。

实现以下接口和 COM 组件的方法：

-   [IAudioProcessingObject](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nn-audioenginebaseapo-iaudioprocessingobject)。 此接口所需的方法是：[**初始化**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobject-initialize)并[ **IsInputFormatSupported。** ](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobject-isinputformatsupported)
-   [IAudioProcessingObjectConfiguration](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nn-audioenginebaseapo-iaudioprocessingobjectconfiguration)。 此接口所需的方法是：[**LockForProcess** ](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectconfiguration-lockforprocess)并[ **UnlockForProcess**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectconfiguration-unlockforprocess)
-   [IAudioProcessingObjectRT](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nn-audioenginebaseapo-iaudioprocessingobjectrt)。 此接口所需的方法是[ **APOProcess** ](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess)它是实现 DSP 算法的方法。
-   [IAudioSystemEffects](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nn-audioenginebaseapo-iaudiosystemeffects)。 此接口可以将 DLL 识别为 APO 的音频引擎。

## <a name="span-idworkingwithvisualstudioandaposspanspan-idworkingwithvisualstudioandaposspanspan-idworkingwithvisualstudioandaposspanworking-with-visual-studio-and-apos"></a><span id="Working_with_Visual_Studio_and_APOs"></span><span id="working_with_visual_studio_and_apos"></span><span id="WORKING_WITH_VISUAL_STUDIO_AND_APOS"></span>使用 Visual Studio 和 a p o s


在使用不在 Visual Studio 中，为每个 APO 项目执行这些任务。

**链接到 CRT**

面向 Windows 10 的驱动程序应动态链接对通用 CRT。

如果你需要支持 Windows 8,1，启用通过在 C 中设置项目属性的静态链接 /C++，代码生成。 设置为"运行时库" */MT*为发布生成或 */MTd*对于调试版本。 进行此更改，因为驱动程序很难重新分发 MSVCRT&lt;n&gt;二进制.dll。 解决方案是以静态方式链接 libcmt.dll。 有关详细信息请参阅[/MD、 /MT、 /LD （使用运行时库）](https://docs.microsoft.com/cpp/build/reference/md-mt-ld-use-run-time-library) 。

**禁用使用嵌入的清单**

通过设置 APO 项目的项目属性来禁用使用嵌入的清单。 选择**清单工具**，**输入和输出**。 然后将更改从默认值为的"嵌入清单"*是*到*否*。 如果嵌入式的清单，这会触发某些 Api 禁止在受保护的环境中使用。 这意味着你 APO 将运行与 DisableProtectedAudioDG = 1，但删除此测试密钥后，你 APO 将加载失败，即使它是 WHQL 签名。

## <a name="span-idpackagingyourapowithadriverspanspan-idpackagingyourapowithadriverspanspan-idpackagingyourapowithadriverspanpackaging-your-apo-with-a-driver"></a><span id="Packaging_your_APO_with_a_Driver"></span><span id="packaging_your_apo_with_a_driver"></span><span id="PACKAGING_YOUR_APO_WITH_A_DRIVER"></span>打包你 APO 与的驱动程序


时开发你自己的音频驱动程序和自动换行或替换系统提供不时，必须安装的驱动程序和不提供驱动程序包。 适用于 Windows 10，请参阅[音频的通用 Windows 驱动程序](audio-universal-drivers.md)。 您相关的音频驱动程序的包应遵循的策略和打包模式那里详细介绍。  

自定义 APO 打包为 DLL，并且 UI 打包为单独的 UWP 或桌面桥应用程序的任何配置。 APO 设备 INF 将 Dll 复制到关联的 INF CopyFile 指令中指示的系统文件夹。 包含 a p o s 的 DLL 必须注册的 INF 文件中包括 AddReg 部分。

以下各段和 INF 文件片段显示是使用标准的 INF 文件以复制并注册 a p o s 所必需的修改。

Sysvad 示例随附的 tabletaudiosample.inf 和 phoneaudiosample.inf 文件演示了如何注册 SwapApo.dll a p o s。

## <a name="span-idregisteringaposforprocessingmodesandeffectsintheinffilespanspan-idregisteringaposforprocessingmodesandeffectsintheinffilespanspan-idregisteringaposforprocessingmodesandeffectsintheinffilespan-registering-apos-for-processing-modes-and-effects-in-the-inf-file"></a><span id="_Registering_APOs_for_Processing_Modes_and_Effects_in_the_INF_File"></span><span id="_registering_apos_for_processing_modes_and_effects_in_the_inf_file"></span><span id="_REGISTERING_APOS_FOR_PROCESSING_MODES_AND_EFFECTS_IN_THE_INF_FILE"></span> 未注册用于处理模式和 INF 文件中的影响


您可以注册未使用注册表项的某些允许组合的特定模式。 影响在其的可用和常规信息 a p o s 的详细信息，请参阅[音频处理对象体系结构](audio-processing-object-architecture.md)。

请参阅以下参考主题，获取每 APO INF 文件设置的信息。

[PKEY\_FX\_StreamEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-streameffectclsid)

[PKEY\_FX\_ModeEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-modeeffectclsid)

[PKEY\_FX\_EndpointEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-endpointeffectclsid)

[PKEY\_SFX\_ProcessingModes\_Supported\_For\_Streaming](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-sfx-processingmodes-supported-for-streaming)

[PKEY\_MFX\_ProcessingModes\_Supported\_For\_Streaming](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-mfx-processingmodes-supported-for-streaming)

[PKEY\_EFX\_ProcessingModes\_Supported\_For\_Streaming](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-efx-processingmodes-supported-for-streaming)

以下的 INF 文件示例演示如何注册音频处理对象 (Apo) 的特定模式。 它们说明了此列表中提供的可能组合。

-   主键\_FX\_StreamEffectClsid 与主键\_SFX\_ProcessingModes\_支持\_为\_流式处理
-   主键\_FX\_ModeEffectClsid 与主键\_MFX\_ProcessingModes\_Suppoted\_为\_流式处理
-   主键\_FX\_而无需主键 ModeEffectClsid\_MFX\_ProcessingModes\_Suppoted\_为\_流式处理
-   主键\_FX\_而无需主键 EndpointEffectClsid\_EFX\_ProcessingModes\_支持\_为\_流式处理

还有一个额外的有效组合，这些示例不会显示。

-   主键\_FX\_EndpointEffectClsid 与主键\_EFX\_ProcessingModes\_支持\_为\_流式处理

**SYSVAD Tablet 多模式流式处理效果 APO INF 示例**

此示例演示多模式流式处理影响正在注册 SYSVAD Tablet INF 文件中使用 AddReg 条目。

此示例代码来自 SYSVAD 音频示例，可在 GitHub 上找到： <https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad>。

此示例演示了此系统效果的组合：

-   主键\_FX\_StreamEffectClsid 与主键\_SFX\_ProcessingModes\_支持\_为\_流式处理

-   主键\_FX\_ModeEffectClsid 与主键\_MFX\_ProcessingModes\_Suppoted\_为\_流式处理

```inf
[SWAPAPO.I.Association0.AddReg]
; Instruct audio endpoint builder to set CLSID for property page provider into the
; endpoint property store
HKR,EP\0,%PKEY_AudioEndpoint_ControlPanelPageProvider%,,%AUDIOENDPOINT_EXT_UI_CLSID%

; Instruct audio endpoint builder to set the CLSIDs for stream, mode, and endpoint APOs
; into the effects property store
HKR,FX\0,%PKEY_FX_StreamEffectClsid%,,%FX_STREAM_CLSID%
HKR,FX\0,%PKEY_FX_ModeEffectClsid%,,%FX_MODE_CLSID%
HKR,FX\0,%PKEY_FX_UserInterfaceClsid%,,%FX_UI_CLSID%

; Driver developer would replace the list of supported processing modes here
; Concatenate GUIDs for DEFAULT, MEDIA, MOVIE
HKR,FX\0,%PKEY_SFX_ProcessingModes_Supported_For_Streaming%,%REG_MULTI_SZ%,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%,%AUDIO_SIGNALPROCESSINGMODE_MEDIA%,%AUDIO_SIGNALPROCESSINGMODE_MOVIE%

; Concatenate GUIDs for DEFAULT, MEDIA, MOVIE
HKR,FX\0,%PKEY_MFX_ProcessingModes_Supported_For_Streaming%,%REG_MULTI_SZ%,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%,%AUDIO_SIGNALPROCESSINGMODE_MEDIA%,%AUDIO_SIGNALPROCESSINGMODE_MOVIE%

;HKR,FX\0,%PKEY_EFX_ProcessingModes_Supported_For_Streaming%,0x00010000,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%
```

请注意，在示例 INF 文件中，EFX\_流式处理属性已被注释掉因为音频处理已转换到内核模式下，上面的层，以便流式处理属性不是必需的不会使用。 它可以有效地指定主键\_FX\_EndpointEffectClsid 发现目的，但它将是一个错误，以指定主键\_EFX\_ProcessingModes\_支持\_为\_流式处理。 这是因为模式混合 / tee 发生更低时堆栈，其中不能插入 APO 的终结点中。

**组件化的 APO 安装**

从 Windows 10 开始版本 1809年，APO 注册与音频引擎使用的组件化的音频驱动程序模型。 使用音频组件化创建更流畅、 更可靠的安装体验，并更好地支持组件服务。 有关详细信息，请参阅[创建的组件化的音频驱动程序安装](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-universal-drivers#creating-a-componentized-audio-driver-installation)。

下面的代码示例从公共 ComponentizedAudioSampleExtension.inf 和 ComponentizedApoSample.inf 提取。 请参阅 GitHub 上提供了 SYSVAD 音频示例： <https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad>。
 
完成的与音频引擎 APO 注册使用的是新创建的 APO 设备。 要使其使用新的 APO 设备的音频引擎必须是即插即用的音频设备的音频的终结点的同级子。 新的组件化的 APO 设计不允许针对 APO 全局注册并由多个不同的驱动程序使用。 每个驱动程序必须注册其自己 APO。

在两个部分完成 APO 的安装。 首先，驱动程序扩展 INF 将向系统添加 APO 设备：
 
```inf
[DeviceExtension_Install.Devices]
AddDevice = SwapApo,,Apo_AddDevice
 
[Apo_AddDevice]
HardwareIds = APO\VEN_SMPL&CID_APO
Description = "Audio Proxy APO Sample"
Capabilities = 0x00000008 ; SWDeviceCapabilitiesDriverRequired
```

此 APO 设备触发的第二部分，APO INF，这是在 ComponentizedApoSample.inf SYSVAD 示例中的安装。 此 INF 文件专用于 APO 设备。 它作为 AudioProcessingObject 指定的设备类并添加所有 CLSID 注册和注册音频引擎的 APO 属性。 
 
```inf
[Version]
Signature   = "$WINDOWS NT$"
Class       = AudioProcessingObject
ClassGuid   = {5989fce8-9cd0-467d-8a6a-5419e31529d4}
 
[ApoComponents.NT$ARCH$]
%Apo.ComponentDesc% = ApoComponent_Install,APO\VEN_SMPL&CID_APO
 
[Apo_AddReg]
; CLSID registration
HKCR,CLSID\%SWAP_FX_STREAM_CLSID%,,,%SFX_FriendlyName%
HKCR,CLSID\%SWAP_FX_STREAM_CLSID%\InProcServer32,,0x00020000,%%SystemRoot%%\System32\swapapo.dll
HKCR,CLSID\%SWAP_FX_STREAM_CLSID%\InProcServer32,ThreadingModel,,"Both"
…
;Audio engine registration
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"FriendlyName",,%SFX_FriendlyName%
...
```

当此 INF 安装组件化的 APO 时，桌面系统上"音频处理对象"将显示在 Windows 设备管理器。 


**蓝芽音频示例 APO INF 示例**

此示例演示了此系统效果的组合：

-   主键\_FX\_StreamEffectClsid 与主键\_SFX\_ProcessingModes\_支持\_为\_流式处理

-   主键\_FX\_ModeEffectClsid 与主键\_MFX\_ProcessingModes\_Suppoted\_为\_流式处理

此示例代码支持蓝牙免提和立体声设备。

```inf
; wdma_bt.inf – example usage
...
[BthA2DP]
Include=ks.inf, wdmaudio.inf, BtaMpm.inf
Needs=KS.Registration,WDMAUDIO.Registration,BtaMPM.CopyFilesOnly,mssysfx.CopyFilesAndRegister
...
[BTAudio.SysFx.Render]
HKR,"FX\\0",%PKEY_ItemNameDisplay%,,%FX_FriendlyName%
HKR,"FX\\0",%PKEY_FX_StreamEffectClsid%,,%FX_STREAM_CLSID%
HKR,"FX\\0",%PKEY_FX_ModeEffectClsid%,,%FX_MODE_CLSID%
HKR,"FX\\0",%PKEY_FX_UiClsid%,,%FX_UI_CLSID%
HKR,"FX\\0",%PKEY_FX_Association%,,%KSNODETYPE_ANY%
HKR,"FX\\0",%PKEY_SFX_ProcessingModes_Supported_For_Streaming%,0x00010000,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%
HKR,"FX\\0",%PKEY_MFX_ProcessingModes_Supported_For_Streaming%,0x00010000,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%
...
[Strings]
FX_UI_CLSID      = "{5860E1C5-F95C-4a7a-8EC8-8AEF24F379A1}"
FX_STREAM_CLSID  = "{62dc1a93-ae24-464c-a43e-452f824c4250}"
PKEY_FX_StreamEffectClsid   = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},5"
PKEY_FX_ModeEffectClsid     = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},6"
PKEY_SFX_ProcessingModes_Supported_For_Streaming = "{D3993A3F-99C2-4402-B5EC-A92A0367664B},5"
PKEY_MFX_ProcessingModes_Supported_For_Streaming = "{D3993A3F-99C2-4402-B5EC-A92A0367664B},6"
AUDIO_SIGNALPROCESSINGMODE_DEFAULT = "{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}"
```

**APO INF 音频示例**

此示例 INF 文件说明了以下系统效果的组合：

-   主键\_FX\_StreamEffectClsid 与主键\_SFX\_ProcessingModes\_支持\_为\_流式处理

-   主键\_FX\_ModeEffectClsid 与主键\_MFX\_ProcessingModes\_Suppoted\_为\_流式处理

-   主键\_FX\_而无需主键 EndpointEffectClsid\_EFX\_ProcessingModes\_支持\_为\_流式处理

```inf
[MyDevice.Interfaces]
AddInterface=%KSCATEGORY_AUDIO%,%MyFilterName%,MyAudioInterface
 
[MyAudioInterface]
AddReg=MyAudioInterface.AddReg
 
[MyAudioInterface.AddReg]
;To register an APO for discovery, use the following property keys in the .inf (or at runtime when registering the KSCATEGORY_AUDIO device interface):
HKR,"FX\\0",%PKEY_FX_StreamEffectClsid%,,%FX_STREAM_CLSID%
HKR,"FX\\0",%PKEY_FX_ModeEffectClsid%,,%FX_MODE_CLSID%
HKR,"FX\\0",%PKEY_FX_EndpointEffectClsid%,,%FX_MODE_CLSID%
 
;To register an APO for streaming and discovery, add the following property keys as well (to the same section):
HKR,"FX\\0",%PKEY_SFX_ProcessingModes_For_Streaming%,%REG_MULTI_SZ%,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%,%AUDIO_SIGNALPROCESSINGMODE_MOVIE%,%AUDIO_SIGNALPROCESSINGMODE_COMMUNICATIONS%
 
;To register an APO for streaming in multiple modes, use a REG_MULTI_SZ property and include all the modes:
HKR,"FX\\0",%PKEY_MFX_ProcessingModes_For_Streaming%,%REG_MULTI_SZ%,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%,%AUDIO_SIGNALPROCESSINGMODE_MOVIE%,%AUDIO_SIGNALPROCESSINGMODE_COMMUNICATIONS%
```

**定义自定义 APO 和 CLSID APO INF 示例**

此示例演示如何定义您自己的自定义 APO 的 CLSID。 此示例使用 MsApoFxProxy CLSID {889C03C8-ABAD-4004-BF0A-BC7BB825E166}。 共同创建 ing 此 GUID 实例化的类中用于实现 IAudioProcessingObject 接口并查询基础驱动程序，通过 KSPROPSETID MsApoFxProxy.dll\_AudioEffectsDiscovery 属性集。

此 INF 文件示例演示\[BthHfAud\]部分中，并带入了\[MsApoFxProxy.Registration\]从 wdmaudio.inf \[BthHfAud.AnlgACapture.AddReg.Wave\]，后者然后注册主键\_FX\_EndpointEffectClsid 作为 MsApoFxProxy.dll 的已知 CLSID。

此 INF 文件示例还演示如何使用此系统效果的组合：

-   主键\_FX\_而无需主键 EndpointEffectClsid\_EFX\_ProcessingModes\_支持\_为\_流式处理

```inf
;wdma_bt.inf
[BthHfAud]
Include=ks.inf, wdmaudio.inf, BtaMpm.inf
Needs=KS.Registration, WDMAUDIO.Registration, BtaMPM.CopyFilesOnly, MsApoFxProxy.Registration
CopyFiles=BthHfAud.CopyList
AddReg=BthHfAud.AddReg

; Called by needs entry in oem inf 
[BthHfAudOEM.CopyFiles]
CopyFiles=BthHfAud.CopyList

[BthHfAud.AnlgACapture.AddReg.Wave]
HKR,,CLSID,,%KSProxy.CLSID%
HKR,"FX\\0",%PKEY_FX_Association%,,%KSNODETYPE_ANY%
HKR,"FX\\0",%PKEY_FX_EndpointEffectClsid%,,%FX_DISCOVER_EFFECTS_APO_CLSID%
#endif
```

此示例 INF 文件显示\[MsApoFxProxy.Registration\]并\[MsApoFxProxy.AddReg\]部分。 这将注册与 COM 使用的已知 GUID \[MsApoFxProxy.CopyList\]部分。 本部分中，将复制到 c: MsApoFxProxy.dll\\Windows\\system32。

```inf
; wdmaudio.inf – this is where WmaLfxGfxDsp.dll is registered
...
;; MsApoFxProxy.Registration section can be called by OEM's to install the discover-effects APO
[MsApoFxProxy.Registration]
AddReg = MsApoFxProxy.AddReg
CopyFiles = MsApoFxProxy.CopyList

[MsApoFxProxy.CopyList]
MsApoFxProxy.dll,,,0x100
...
[MsApoFxProxy.AddReg]
; Discover Effects APO COM registration
HKCR,CLSID\%FX_DISCOVER_EFFECTS_APO_CLSID%,,,%FX_DiscoverEffectsApo_FriendlyName%
HKCR,CLSID\%FX_DISCOVER_EFFECTS_APO_CLSID%\InProcServer32,,,%11%\MsApoFxProxy.dll
HKCR,CLSID\%FX_DISCOVER_EFFECTS_APO_CLSID%\InProcServer32,ThreadingModel,,"Both"

; Discover Effects APO registration
HKCR,AudioEngine\AudioProcessingObjects\%FX_DISCOVER_EFFECTS_APO_CLSID%, "FriendlyName", ,%FX_DiscoverEffectsApo_FriendlyName%
HKCR,AudioEngine\AudioProcessingObjects\%FX_DISCOVER_EFFECTS_APO_CLSID%, "Copyright", ,%MsCopyRight%
HKCR,AudioEngine\AudioProcessingObjects\%FX_DISCOVER_EFFECTS_APO_CLSID%, "MajorVersion", 0x00010001, 1
HKCR,AudioEngine\AudioProcessingObjects\%FX_DISCOVER_EFFECTS_APO_CLSID%, "MinorVersion", 0x00010001, 1
HKCR,AudioEngine\AudioProcessingObjects\%FX_DISCOVER_EFFECTS_APO_CLSID%, "Flags", 0x00010001, 0x0000000d
HKCR,AudioEngine\AudioProcessingObjects\%FX_DISCOVER_EFFECTS_APO_CLSID%, "MinInputConnections", 0x00010001, 1
HKCR,AudioEngine\AudioProcessingObjects\%FX_DISCOVER_EFFECTS_APO_CLSID%, "MaxInputConnections", 0x00010001, 1
HKCR,AudioEngine\AudioProcessingObjects\%FX_DISCOVER_EFFECTS_APO_CLSID%, "MinOutputConnections", 0x00010001, 1
HKCR,AudioEngine\AudioProcessingObjects\%FX_DISCOVER_EFFECTS_APO_CLSID%, "MaxOutputConnections", 0x00010001, 1
HKCR,AudioEngine\AudioProcessingObjects\%FX_DISCOVER_EFFECTS_APO_CLSID%, "MaxInstances", 0x00010001, 0xffffffff
HKCR,AudioEngine\AudioProcessingObjects\%FX_DISCOVER_EFFECTS_APO_CLSID%, "NumAPOInterfaces", 0x00010001, 1
HKCR,AudioEngine\AudioProcessingObjects\%FX_DISCOVER_EFFECTS_APO_CLSID%, "APOInterface0", ,"{FD7F2B29-24D0-4B5C-B177-592C39F9CA10}"
...
```

## <a name="span-idaporegistrationspanspan-idaporegistrationspanspan-idaporegistrationspanapo-registration"></a><span id="APO_Registration"></span><span id="apo_registration"></span><span id="APO_REGISTRATION"></span>APO 注册


APO 注册用于支持动态匹配到终结点使用加权的计算效果的进程。 加权的计算使用以下属性存储。 音频的每个接口有零个或多*终结点属性存储*并*效果属性存储*通过.inf 或在运行时注册。 在最具体的终结点属性存储和最具体的效果属性存储具有最高的权重，并使用。 将忽略所有其他属性存储。

特异性的计算方式如下：

终结点属性存储的权重

1. 与特定 KSNODETYPE FX
2. 使用 KSNODETYPE FX\_ANY
3. 与特定 KSNODETYPE MSFX
4. 使用 KSNODETYPE MSFX\_ANY

影响权重的属性存储

1. 与特定 KSNODETYPE EP
2. 使用 KSNODETYPE EP\_ANY
3. 与特定 KSNODETYPE MSEP
4. 使用 KSNODETYPE MSEP\_ANY

数字必须从 0 开始，按顺序增加：MSEP\\0，MSEP\\1，...，MSEP\\n 如果 （例如） EP\\3 缺失，Windows 将停止查找 EP\\n，将不会看到 EP\\4，即使存在

主键的值\_FX\_（适用于效果属性存储） 的关联或主键\_EP\_（适用于终结点属性存储） 的关联与 KSPINDESCRIPTOR 进行比较。硬件末尾的信号路径，如公开的内核流式处理的 pin 工厂的类别值。

仅 Microsoft 收件箱类驱动程序 （这可以包装由第三方开发人员） 应使用 MSEP 和 MSFX;所有第三方驱动程序应使用 EP 和 FX。

**APO 节点类型兼容性**

下面的 INF 文件示例说明如何设置主键\_FX\_为 GUID 的关联键与 APO 相关联。

```inf
;; Property Keys
PKEY_FX_Association = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},0"
"
```

```inf
;; Key value pairs
HKR,"FX\\0",%PKEY_FX_Association%,,%KSNODETYPE_ANY%
```

因为音频适配器能够支持多个输入和输出，必须显式指示内核流式处理的自定义 APO 是与兼容 (KS) 节点类型的类型。 在前面的 INF 文件片段中，APO 显示为与 %ksnodetype KS 节点类型关联\_任何 %。 更高版本中此 INF 文件中，KSNODETYPE\_任何已定义的如下所示：

```inf
[Strings]
;; Define the strings used in MyINF.inf
...
KSNODETYPE_ANY      = "{00000000-0000-0000-0000-000000000000}"
KSNODETYPE_SPEAKER  = "{DFF21CE1-F70F-11D0-B917-00A0C9223196}"
...
```

值为**NULL**为 KSNODETYPE\_任何意味着此 APO 与 KS 节点类型的任何类型兼容。 若要指示，例如，你 APO 才 KSNODETYPE KS 节点类型与兼容\_演讲者，INF 文件会显示 KS 节点类型和 APO 关联，如下所示：

```inf
;; Key value pairs
...
HKR,"FX\\0",%PKEY_FX_Association%,,%KSNODETYPE_SPEAKER%
...
```

有关不同 KS 节点类型的 GUID 值的详细信息，请参阅 Ksmedia.h 标头文件。

## <a name="span-idtroubleshootingapoloadfailuresspanspan-idtroubleshootingapoloadfailuresspanspan-idtroubleshootingapoloadfailuresspantroubleshooting-apo-load-failures"></a><span id="Troubleshooting_APO_Load_Failures"></span><span id="troubleshooting_apo_load_failures"></span><span id="TROUBLESHOOTING_APO_LOAD_FAILURES"></span>故障排除 APO 加载失败


提供以下信息来帮助你了解如何为未监视失败。 可以使用此信息来解决不无法获取合并到音频图形的。

APO 的音频系统监视器返回代码以确定是否不已成功加入到关系图。 它将监视的返回代码的任何一种指定的方法跟踪返回的 HRESULT 值。 系统会为每个 SFX、 MFX 和将被合并到关系图的 EFX APO 维护单独失败计数值。

音频系统监视从以下四个方法返回的 HRESULT 值。

-   CoCreateInstance

-   IsInputFormatSupported

-   IsOutputFormatSupported

-   LockForProcess

每次下列方法之一返回了失败代码时，将针对 APO 递增失败计数值。 失败计数重置为零 APO 时返回的代码，指示它已成功合并到音频图形。 在成功调用[ **LockForProcess** ](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectconfiguration-lockforprocess)方法很好反映 APO 已成功合并。

有关[ **CoCreateInstance** ](https://docs.microsoft.com/windows/desktop/api/combaseapi/nf-combaseapi-cocreateinstance)具体而言，有多种原因而返回的 HRESULT 代码可能指示失败的原因。 三个主要原因是，如下所示：

-   在关系图正在运行受保护的内容，并且 APO 未正确签名。

-   APO 未注册。

-   APO 已重命名或被篡改。

此外，如果失败计数值为 SFX，MFX 或 EFX APO 达到系统指定的限制，SFX、 MFX 和 EFX 未禁用通过设置主键\_终结点\_禁用\_SysFx 注册表项为"1"。 系统指定限制当前为值为 10。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[实现 UI 用于配置 APO 效果](implementing-a-ui-for-configuring-apo-effects.md)  

[Windows 音频处理对象](windows-audio-processing-objects.md)  



