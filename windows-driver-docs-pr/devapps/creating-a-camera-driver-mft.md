---
title: 为 UWP 设备应用创建照相机驱动程序 MFT
description: UWP 设备应用允许设备制造商使用相机驱动程序 MFT （media foundation 转换）对照相机的视频流应用自定义设置和特殊影响。
ms.assetid: 079CB01E-D16C-4597-8F08-BD75F1D02427
ms.date: 09/14/2017
ms.localizationpriority: medium
ms.openlocfilehash: 452a5e9f56624f1a14b3be47b50959ecccef8594
ms.sourcegitcommit: 3ec971f54122b77408433f7f1e59c467099fb4de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86873862"
---
# <a name="creating-a-camera-driver-mft-for-a-uwp-device-app"></a>为 UWP 设备应用创建照相机驱动程序 MFT

> [!IMPORTANT]
> 本主题已被弃用。 请参阅[设备 MFT 设计指南](https://docs.microsoft.com/windows-hardware/drivers/stream/dmft-design)了解更新的指南。

UWP 设备应用允许设备制造商使用相机驱动程序 MFT （media foundation 转换）对照相机的视频流应用自定义设置和特殊影响。 本主题介绍了驱动程序 MFTs，并使用了[驱动程序 MFT](https://go.microsoft.com/fwlink/p/?LinkID=251566)示例演示如何创建一个。 若要详细了解 UWP 设备应用的详细信息，请参阅了解[uwp 设备应用](meet-uwp-device-apps.md)。

## <a name="the-driver-mft"></a>驱动程序 MFT

本部分介绍创建的用于将效果应用于照相机的媒体捕获流的媒体基础转换（MFT）。 这就是你为颜色效果、方案模式和人脸跟踪效果提供转换的方式，这些效果将相机与其他人区分开来。 当 UWP 应用开始视频捕获时，此 MFT 称为 "驱动程序 MFT" 将首先应用于照相机驱动程序所连接的视频流。 当应用程序调用**相机选项**UI 时，Windows 将自动提供对驱动程序 MFT 为控制其自定义效果而实现的任何接口的访问。

![相机驱动程序 mft 可帮助 windows 应用商店设备应用提供自定义效果。](images/372783-camera-drivermft-overview.png)

UWP 设备应用不需要驱动程序 MFT。 设备制造商可以选择在不使用驱动程序 MFT 的情况下实现 UWP 设备应用，只需为其硬件提供一个包含品牌的区分用户界面，而无需对视频流应用自定义设置和特殊效果。

### <a name="how-a-driver-mft-is-used"></a>如何使用驱动程序 MFT

照相机的 UWP 设备应用在不同于从[CameraCaptureUI](https://go.microsoft.com/fwlink/p/?LinkId=317985) API 调用它的 Microsoft Store 应用程序的进程中运行。 要使 Microsoft Store 设备应用控制驱动程序 MFT，必须在不同的进程空间中出现一系列特定的事件。

1. UWP 应用想要捕获照片，因此它将调用[CaptureFileAsync](https://go.microsoft.com/fwlink/p/?LinkId=317986)方法
2. Windows 请求驱动程序 MFT 指针和相机的设备 ID
3. 将驱动程序 MFT 指针传递到设置主机
4. 主机查询与相机关联的 Microsoft Store 设备应用的应用 ID 的设备属性（每个设备的元数据）
5. 如果未找到 UWP 设备应用，则默认飞出会与捕获引擎交互
6. 如果找到了 UWP 设备应用，则会将其激活，设置主机会将驱动程序 MFT 指针传递给它
7. UWP 设备应用使用通过指针公开的接口控制驱动程序 MFT

![用于调用 windows 应用商店设备应用程序的进程交互。](images/372798-cameradrivermft-internals.png)

### <a name="avstream-driver-model-requirement"></a>AvStream 驱动程序模型要求

照相机的驱动程序必须使用 AvStream 驱动程序模型。 有关 AVStream 驱动程序模型的详细信息，请参阅[AVStream 微型驱动程序 Design Guide](https://go.microsoft.com/fwlink/p/?LinkID=228585)。

### <a name="how-the-driver-mft-is-exposed-to-apps"></a>如何将驱动程序 MFT 公开给应用

驱动程序 MFT 注册为 Windows 作为 COM 接口，以便可以将其实现的转换应用于特定设备（如相机）中的媒体流。

**注意** 不应使用该函数注册驱动程序 MFT `MFTRegister` ，因为它是特定于设备，而不是常规用途的 mft。 有关注册表项的信息，请参阅本主题后面的[安装和注册驱动程序 MFT](#installing-and-registering-the-driver-mft)部分。

应用启动视频捕获时，会实例化媒体基础源读取器来提供视频流。 此媒体源从设备注册表项读取注册表值。 如果在注册表值中找到驱动程序 MFT 的 COM 类的 CLSID，则源读取器将实例化驱动程序 MFT，并将其插入到媒体管道中。

除了 UWP 设备应用外，还可以在使用关联的设备使用以下 Api 捕获视频时访问驱动程序 MFT 功能：

- &lt; &gt; 使用 HTML 的 UWP 应用中的 HTML5 视频标记。 驱动程序 MFT 启用的转换会影响使用视频元素播放的视频 &lt; &gt; ，如以下代码示例所示：

    ```cpp
    var video = document.getElementById('myvideo');
        video.src = URL.createObjectURL(fileItem);
        video.play();
    ```

- 使用 Windows 运行时的 UWP 应用中的 MediaCapture API。 有关如何使用此 API 的详细信息，请参阅[媒体捕获](https://go.microsoft.com/fwlink/p/?LinkId=243997)示例。

- 媒体基础的源读取器，用于处理媒体数据的应用程序。 调用时，驱动程序 MFT 将作为第一个（第0个） MFT 向应用程序公开 `IMFSourceReaderEx::GetTransformForStream` 。 将返回的类别为 `MFT_CATEGORY_VIDEO_EFFECT` 。

    ![源读取器在媒体捕获中的角色。](images/372842-cameracaptureengine.png)

### <a name="multi-pin-cameras"></a>多 pin 相机

如果有三针或其他多 pin 相机，请参阅[有关多 pin 相机上的驱动程序 MFTs 的注意事项](driver-mfts-on-multi-pin-cameras.md)。

## <a name="driver-mft-implementation"></a>驱动程序 MFT 实现

本部分提供了有关实施驱动程序 MFT 的信息。 有关与 UWP 设备应用一起工作的驱动程序 MFT 的完整示例，请参阅[驱动程序 mft](https://go.microsoft.com/fwlink/p/?LinkID=251566)示例。

### <a name="development-tools"></a>开发工具

Microsoft Visual Studio Professional 或 Microsoft Visual Studio Ultimate 是必需的。

### <a name="driver-mft-characteristics"></a>驱动程序 MFT 特性

驱动程序 MFT 按流实例化。 对于相机支持的每个流，会实例化 MFT 的实例并将其连接到该实例。 驱动程序 MFT 应有单个输入流和一个输出流。 驱动程序 MFT 可以是同步 MFT，也可以是异步 MFT。

### <a name="communication-between-the-camera-and-the-driver-mft"></a>照相机和驱动程序 MFT 之间的通信

若要在媒体源和驱动程序 MFT 之间启用双向通信，则将驱动程序 MFT 的输入流属性存储中的指针设置为，并将其设置为源流的属性存储 `MFT_CONNECTED_STREAM_ATTRIBUTE` 。 这种情况是通过在驱动程序 MFT 中公开而启用的握手过程来实现的 `MFT_ENUM_HARDWARE_URL_Attribute` ，如以下示例中所示：

```cpp
HRESULT CDriverMft::GetAttributes(IMFAttributes** ppAttributes)
{
    HRESULT hr = S_OK;
    if (NULL == ppAttributes)
    {
       return E_POINTER; 
    };
        if(!m_pGlobalAttributes) {
           MFCreateAttributes(&m_pGlobalAttributes, 1);
           m_pGlobalAttributes-> 
             SetString(MFT_ENUM_HARDWARE_URL_Attribute, L"driverMFT");
        }
        *ppAttributes = m_pGlobalAttributes;
        (*ppAttributes)->AddRef();
        return S_OK;
}
```

在此示例中， `MFT_CONNECTED_STREAM_ATTRIBUTE` 驱动程序 MFT 的属性存储中的设置为指向设备源流的属性存储。 请参阅[硬件握手序列](https://go.microsoft.com/fwlink/p/?LinkId=320139)，详细了解如何设置照相机与 MFT 之间的通信。

### <a name="how-to-access-device-source-information"></a>如何访问设备源信息

下面的代码示例演示了驱动程序 MFT 如何从其输入属性存储获取指向源转换的指针。 然后，驱动程序 MFT 可以使用源指针获取设备源信息。

```cpp
if(!m_pSourceTransform && m_pInputAttributes) {

          m_pInputAttributes->
              GetUnknown( MFT_CONNECTED_STREAM_ATTRIBUTE,
              IID_PPV_ARGS(&pSourceAttributes));
          pSourceAttributes-> 
              GetUnknown(
              MF_DEVICESTREAM_EXTENSION_PLUGIN_CONNECTION_POINT,            
              IID_PPV_ARGS(&pUnk)));
          pUnk->QueryInterface(__uuidof(IMFTransform), 
              (void**)&m_pSourceTransform));
      }
      if (m_pSourceTransform) {
         // Put code to get device source information here.         
      }
```

### <a name="how-to-implement-passthrough-mode"></a>如何实现 passthrough 模式

若要将驱动程序 MFT 置于直通模式，请为输入流和输出流指定相同的媒体类型。 `ProcessInput`并且 `ProcessOutput` 仍将对 MFT 调用。 此方法留给了驱动程序 MFT 实现，以确定是否在 passthrough 模式下进行任何处理。

### <a name="header-files-to-include"></a>要包含的头文件

需要包含 `IInspectable` `IMFTransform` 驱动程序 MFT 必须实现的和方法的标头文件。 有关要包括的标头文件的列表，请参阅[适用于照相机的 UWP 设备应用](https://go.microsoft.com/fwlink/p/?LinkID=227865)示例的**SampleMFT0**目录中的**stdafx.h。**

```cpp
// required for IInspectable
#include <inspectable.h>
```

### <a name="how-to-implement-iinspectable"></a>如何实现 IInspectable

旨在从照相机的 UWP 设备应用程序使用的驱动程序 MFT 必须实现的方法， `IInspectable` 以便 Microsoft Store 设备应用程序在启动时可以访问指向驱动程序 MFT 的指针。 驱动程序 MFT 应实现的方法， `IInspectable` 如下所示：

- **IInspectable：： GetIids**应在*iid* out 参数中返回 Null，并在*iidCount* out 参数中返回0。

- **IInspectable：： GetRuntimeClassName**应在 out 参数中返回 null。

- **IInspectable：： GetRuntiGetTrustLevel**应 `TrustLevel::BaseTrust` 在 out 参数中返回。

下面的代码示例演示如何 `IInspectable` 在示例驱动程序 MFT 中实现这些方法。 此代码可在示例的**SampleMFT0**目录中的**Mft0**文件中找到。

```cpp
// Mft0.cpp
STDMETHODIMP CMft0::GetIids( 
    /* [out] */ __RPC__out ULONG *iidCount,
    /* [size_is][size_is][out] */ __RPC__deref_out_ecount_full_opt(*iidCount) IID **iids)
{
    HRESULT hr = S_OK;
    do {
        CHK_NULL_PTR_BRK(iidCount);
        CHK_NULL_PTR_BRK(iids);
        *iids = NULL;
        *iidCount = 0;
    } while (FALSE);

    return hr;
}

STDMETHODIMP CMft0::GetRuntimeClassName( 
    /* [out] */ __RPC__deref_out_opt HSTRING *className)
{
    HRESULT hr = S_OK;
    do {
        CHK_NULL_PTR_BRK(className);
        *className = NULL;
    } while (FALSE);

    return hr;
}

STDMETHODIMP CMft0::GetTrustLevel( 
    /* [out] */ __RPC__out TrustLevel *trustLevel)
{
    HRESULT hr = S_OK;
    do {
        CHK_NULL_PTR_BRK(trustLevel);
        *trustLevel = TrustLevel::BaseTrust;
    } while (FALSE);

    return hr;
}
```

### <a name="com-implementation"></a>COM 实现

驱动程序 MFT 实现的每个接口都应该实现并从中派生 `IUnknown` ，以便正确地封送到照相机的 UWP 设备应用。 下面是一个说明此的驱动程序 MFT 的 .idl 文件示例 **。**

```cpp
// SampleMft0.idl : IDL source for SampleMft0
//

// This file will be processed by the MIDL tool to
// produce the type library (SampleMft0.tlb) and marshalling code.

import "oaidl.idl";
import "ocidl.idl";
import "Inspectable.idl";
import "mftransform.idl";
[
    object,
    uuid(F5208B72-A37A-457E-A309-AE3060780E21),
    oleautomation,
    nonextensible,
    pointer_default(unique)
]
interface IMft0 : IUnknown{
    [id(1)] HRESULT UpdateDsp([in] UINT32 uiPercentOfScreen);
    [id(2)] HRESULT Enable(void);
    [id(3)] HRESULT Disable(void);
    [id(4)] HRESULT GetDspSetting([out] UINT* puiPercentOfScreen, [out] BOOL* pIsEnabled);
};
[
    uuid(DE05674A-C564-4C0E-9B7C-E1519F7AA767),
    version(1.0),
]
library SampleMft0Lib
{
    importlib("stdole2.tlb");
    [
        uuid(7BB640D9-33A4-4759-B290-F41A31DCF848)      
    ]
    coclass Mft0
    {
        [default] interface IMft0;
        interface IInspectable;
        interface IMFTransform;
    };
};
```

**注意** 驱动程序 MFT 是常规的 COM 类，可以使用创建 `CoCreateInstance` 。 不应使用 `MFTRegister` 函数进行注册，因为它不是通用 MFT。

### <a name="creating-a-proxy"></a>创建代理

驱动程序 MFT 是进程外服务器。 若要在 UWP 设备应用中使用它，必须在代理中提供封送支持，以便可以跨进程边界使用驱动程序 MFT 接口。 可以在[驱动程序 MFT](https://go.microsoft.com/fwlink/p/?LinkID=251566)示例中找到此示例。 该示例使用 MIDL 编译器生成无存根代理。

### <a name="exposing-the-driver-mft-to-apps"></a>向应用程序公开驱动程序 MFT

若要在 c # 或 JavaScript 中编写与驱动程序 MFT 交互的 UWP 设备应用，需要在 Microsoft Store 设备应用的 Microsoft Visual Studio 项目中创建一个附加组件。 此组件是一个包装，该包装程序在 Microsoft Store 设备应用程序可见的 Windows 运行时组件中公开驱动程序 MFT 接口。

[适用于照相机的 UWP 设备应用](https://go.microsoft.com/fwlink/p/?LinkID=227865)示例中的包装子项目提供了一个示例，说明如何向 Windows 运行时公开驱动程序 MFT，以便可以从使用 c # 或 JavaScript 实现的 UWP 设备应用程序中使用它。 它设计为与[驱动程序 MFT](https://go.microsoft.com/fwlink/p/?LinkID=251566)示例一起使用。 请参阅[驱动程序 MFT](https://go.microsoft.com/fwlink/p/?LinkID=251566)示例页，获取有关安装、运行和测试示例的分步指南。

## <a name="installing-and-registering-the-driver-mft"></a>安装和注册驱动程序 MFT

本部分列出了安装驱动程序 MFT 的步骤：

1. 驱动程序 MFT DLL 必须安装在以下位置的子目录中：
    - % SystemDrive% \\ Program 文件\\
2. 照相机安装程序通过在驱动程序 MFT DLL 上调用**regsvr32**来注册驱动程序 mft，或为安装程序用于注册的 DLL 提供驱动程序清单（man）文件。
3. 设置 `CameraPostProcessingPluginCLSID` 相机的注册表项中的值。 INF 文件应通过将 `CameraPostProcessingPluginCLSID` 值设置为驱动程序 mft 类的 CLSID GUID 来指定设备的设备类注册表项中的驱动程序 mft 的 clsid。 下面是一个用于填充相机的注册表项的 INF 文件条目的示例：

```inf
KSCATEGORY_VIDEO_CAMERA:

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceClasses\{E5323777-F976-4f5b-9B55-B94699C46E44}\##?#USB#VID_045E&PID_075D&MI_00#8&23C3DB65&0&0000#{E5323777-F976-4f5b-9B55-B94699C46E44}\#GLOBAL\Device Parameters]
"CLSID"="{17CCA71B-ECD7-11D0-B908-00A0C9223196}"
"FriendlyName"="USB Video Device"
"RTCFlags"=dword:00000010
"CameraPostProcessingPluginCLSID"="{3456A71B-ECD7-11D0-B908-00A0C9223196}" 
```

```inf
KSCATEGORY_CAPTURE:

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceClasses\{ 65E8773D-8F56-11D0-A3B9-00A0C9223196}\##?#USB#VID_045E&PID_075D&MI_00#8&23C3DB65&0&0000#{65E8773D-8F56-11D0-A3B9-00A0C9223196}\#GLOBAL\Device Parameters]
"CLSID"="{17CCA71B-ECD7-11D0-B908-00A0C9223196}"
"FriendlyName"="USB Video Device"
"RTCFlags"=dword:00000010
"CameraPostProcessingPluginCLSID"="{3456A71B-ECD7-11D0-B908-00A0C9223196}"
```

**注意** `KSCATEGORY_VIDEO_CAMERA`对于照相机，建议使用。   通常只需要一个注册表项，具体取决于设备的注册方式。


## <a name="associate-your-app-with-the-camera"></a>将你的应用与相机关联

本部分包含有关在设备元数据和 Windows 注册表中标识相机所需的步骤的信息。 此元数据可让你配对 UWP 设备应用并标识应用，以便在第一次连接照相机时可以无缝下载该应用。

### <a name="updates"></a>更新

第一次安装应用程序后，如果用户下载应用程序的更新版本，则更新会自动集成到相机捕获体验中。 但是，不会自动下载更新。 用户必须从 Microsoft Store 下载附加的应用程序更新，因为应用仅在第一次连接时[自动安装](auto-install-for-uwp-device-apps.md)。 UWP 设备应用的主页可以提供更新可用的通知，并提供下载更新的链接。

**重要提示** 更新后的应用应与通过 Windows 更新分发的任何更新的驱动程序配合使用。

### <a name="multiple-cameras"></a>多个照相机

多个相机型号可以在其设备元数据中声明同一 UWP 设备应用。 如果系统中有多个内部嵌入的相机，则照相机必须共享同一 UWP 设备应用。 该应用包含确定正在使用哪种照相机的逻辑，并且可以在**更多的选项**体验中为每个相机显示不同的 UI。 有关自定义该体验的详细信息，请参阅[如何自定义相机选项](how-to-customize-camera-options.md)。

### <a name="internal-cameras"></a>内部照相机

用于内部相机的 UWP 设备应用可以从 Microsoft Store 进行[自动安装](auto-install-for-uwp-device-apps.md)，但建议预先安装这些应用以获得最无缝的用户体验。 还需要执行其他步骤来支持内部相机并将 UWP 设备应用与它们相关联。 有关详细信息，请参阅[标识内部照相机的位置](identifying-the-location-of-internal-cameras.md)。

### <a name="creating-the-device-metadata-package"></a>创建设备元数据包

对于内部和外部照相机，都需要创建设备元数据包。 当你将照相机的 UWP 设备应用提交到 Microsoft Store （或使用 OPK （对于内部相机）预安装它时，你将需要提供包含以下内容的元数据：

- 应用程序发布者名称
- 应用程序包名称
- 应用程序元素标识符
- 设备体验标识符

有关如何使用设备元数据将应用程序与设备关联的详细信息，请参阅[构建 UWP 设备应用](the-workflow.md)。

## <a name="related-topics"></a>相关主题

[构建 UWP 设备应用](the-workflow.md)

[UWP 设备应用的自动安装](auto-install-for-uwp-device-apps.md)

[硬件握手序列（硬件 MFTs）](https://go.microsoft.com/fwlink/p/?LinkId=320139)

[AVStream 微型驱动程序设计指南](https://go.microsoft.com/fwlink/p/?LinkID=228585)

[适用于照相机的 UWP 设备应用示例](https://go.microsoft.com/fwlink/p/?LinkID=227865)

[驱动程序 MFT 示例](https://go.microsoft.com/fwlink/p/?LinkID=251566)





