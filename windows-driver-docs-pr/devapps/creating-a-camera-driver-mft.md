---
title: 创建 UWP 设备应用的照相机驱动程序 MFT
description: UWP 设备应用程序还允许设备制造商上与相机驱动程序 MFT （媒体基础转换） 的照相机的视频流应用自定义设置和特殊效果。
ms.assetid: 079CB01E-D16C-4597-8F08-BD75F1D02427
ms.date: 09/14/2017
ms.localizationpriority: medium
ms.openlocfilehash: 842c15524c0e3517c15a666666719fcfb67f8954
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902764"
---
# <a name="creating-a-camera-driver-mft-for-a-uwp-device-app"></a>创建 UWP 设备应用的照相机驱动程序 MFT

> [!IMPORTANT]
> 本主题已弃用。 请参阅[设备 MFT 设计指南](https://docs.microsoft.com/windows-hardware/drivers/stream/dmft-design)更新的指南。

UWP 设备应用程序还允许设备制造商上与相机驱动程序 MFT （媒体基础转换） 的照相机的视频流应用自定义设置和特殊效果。 本主题介绍驱动程序 Mft 并使用[驱动程序 MFT](https://go.microsoft.com/fwlink/p/?LinkID=251566)示例来演示如何创建一个。 若要在一般情况下了解有关 UWP 的设备应用程序的详细信息，请参阅[满足 UWP 设备应用](meet-uwp-device-apps.md)。

## <a name="the-driver-mft"></a>驱动程序 MFT

本部分介绍 Media Foundation 转换 (MFT) 创建将效果应用于来自摄像头的媒体捕获流。 这是如何为颜色效果、 方案模式和真正将您的照相机区别于其他的人脸跟踪效果提供转换。 此 MFT，称为驱动程序 MFT，首先将应用于已连接的视频流时的 UWP 应用开始视频捕获来自照相机驱动程序。 当该应用程序调用**照相机选项**UI 中，Windows 会自动提供与任何接口访问驱动程序 MFT 实现用于控制其自定义效果。

![照相机的驱动程序 mft 有助于 windows 应用商店设备应用程序提供自定义效果。](images/372783-camera-drivermft-overview.png)

驱动程序 MFT 不需要对 UWP 设备应用。 设备制造商可以选择实现一个 UWP 设备应用，而无需驱动程序 MFT，只是为了提供与众不同的用户界面包含适用于的品牌硬件，而无需将自定义设置和特殊效果应用于视频流。

### <a name="how-a-driver-mft-is-used"></a>如何使用驱动程序 MFT

用于相机的 UWP 设备的应用程序比调用从 Microsoft Store 应用程序的不同进程中运行[CameraCaptureUI](https://go.microsoft.com/fwlink/p/?LinkId=317985) API。 若要控制驱动程序 MFT 的 Microsoft Store 设备应用，必须出现一系列特定的不同进程空间中的事件。

1. UWP 应用程序想要捕获照片，这样它便可以调用[CaptureFileAsync](https://go.microsoft.com/fwlink/p/?LinkId=317986)方法
2. Windows 请求驱动程序 MFT 指针和照相机的设备 ID
3. 驱动程序 MFT 指针传递给设置主机
4. 在主机中的 Microsoft Store 设备应用使用照相机 （每个设备元数据） 相关联的应用程序 ID 查询设备属性
5. 如果不找到任何 UWP 设备应用，则默认浮出控件与捕获引擎进行交互
6. 如果找到 UWP 设备应用，则它激活和设置主机将驱动程序 MFT 指针传递给它
7. UWP 设备应用程序控制驱动程序 MFT 使用通过指针所公开的接口

![用于调用 windows 应用商店设备应用程序进程交互。](images/372798-cameradrivermft-internals.png)

### <a name="avstream-driver-model-requirement"></a>AvStream 驱动程序模型要求

照相机的驱动程序必须使用 AvStream 驱动程序模型。 有关 AVStream 驱动程序模型的详细信息，请参阅[AVStream 微型驱动程序设计指南](https://go.microsoft.com/fwlink/p/?LinkID=228585)。

### <a name="how-the-driver-mft-is-exposed-to-apps"></a>如何向应用程序公开的驱动程序 MFT

驱动程序 MFT 已注册 Windows 为 COM 接口，以便实现转换可以应用于来自特定设备，如摄像头的媒体流。

**请注意**驱动程序不应使用注册 MFT`MFTRegister`函数，因为它是特定的设备并不是通用 MFT。 注册表项的信息，请参阅[安装和注册的驱动程序 MFT](#installing-and-registering-the-driver-mft)本主题后面的部分。

当应用启动时视频捕获时，Media Foundation 源读取器实例化提供视频流。 此媒体源设备注册表项中读取的注册表值。 如果注册表值中找到驱动程序 MFT 的 COM 类的 CLSID，则源读取器实例化驱动程序 MFT，并将其插入到媒体管道。

除了 UWP 的设备应用程序，与它关联的设备用于捕获视频使用以下 Api 时，可以访问驱动程序 MFT 功能：

- HTML5&lt;视频&gt;使用 HTML 的 UWP 应用中的标记。 转换的驱动程序 MFT 已启用，会影响使用正在播放的视频&lt;视频&gt;元素，如以下代码示例所示：

    ```cpp
    var video = document.getElementById('myvideo');
        video.src = URL.createObjectURL(fileItem);
        video.play();
    ```

- 使用 Windows 运行时的 UWP 应用中 Windows.Media.MediaCapture API。 有关如何使用此 API 的详细信息，请参阅[媒体捕获](https://go.microsoft.com/fwlink/p/?LinkId=243997)示例。

- 媒体基础源读取器，用于处理媒体数据的应用程序。 驱动程序 MFT 会公开给应用程序作为第一个 （第 0 个） MFT 调用时`IMFSourceReaderEx::GetTransformForStream`。 将返回该类别是`MFT_CATEGORY_VIDEO_EFFECT`。

    ![媒体捕获中的源读取器的角色。](images/372842-cameracaptureengine.png)

### <a name="multi-pin-cameras"></a>在多针相机

如果您有三个 pin 或其他多针相机，请参阅[多针相机上的驱动程序 Mft 的注意事项](driver-mfts-on-multi-pin-cameras.md)。

## <a name="driver-mft-implementation"></a>驱动程序 MFT 实现

本部分提供有关实施您的驱动程序 MFT 的信息。 有关驱动程序 MFT 一起使用的 UWP 设备应用程序的完整示例，请参阅[驱动程序 MFT](https://go.microsoft.com/fwlink/p/?LinkID=251566)示例。

### <a name="development-tools"></a>开发工具

Microsoft Visual Studio Professional 或 Microsoft Visual Studio Ultimate 是必需的。

### <a name="driver-mft-characteristics"></a>驱动程序 MFT 特征

驱动程序 MFT 是实例化每个流。 每个流照相机支持，在 MFT 的实例已实例化并连接到它。 驱动程序 MFT 应具有单个输入的流和单个输出流。 驱动程序 MFT 可能是同步的 MFT 或异步 MFT。

### <a name="communication-between-the-camera-and-the-driver-mft"></a>照相机和驱动程序 MFT 之间的通信

若要启用的媒体源和驱动程序 MFT 之间的双向通信，源流的属性存储的指针上设置驱动程序 MFT 的输入的流属性存储为`MFT_CONNECTED_STREAM_ATTRIBUTE`。 通过启用通过公开的握手过程将发生这种情况`MFT_ENUM_HARDWARE_URL_Attribute`在驱动程序 MFT，如以下示例所示：

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

在此示例中，`MFT_CONNECTED_STREAM_ATTRIBUTE`驱动程序 MFT 属性中存储设置以指向设备源流的属性存储。 请参阅[硬件握手序列](https://go.microsoft.com/fwlink/p/?LinkId=320139)，详细了解如何设置照相机和 MFT 之间的通信。

### <a name="how-to-access-device-source-information"></a>如何访问设备源信息

以下代码示例演示如何驱动程序 MFT 可以获取指向源转换从其输入的属性存储区。 然后，驱动程序 MFT 可用源指针来获取设备源信息。

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

### <a name="how-to-implement-passthrough-mode"></a>如何实现直通模式

若要将驱动程序 MFT 放在直通模式下，指定输入和输出流的相同媒体类型。 `ProcessInput` 和`ProcessOutput`仍可进行对 MFT 的调用。 它是应由驱动程序 MFT 实现，以决定在直通模式下进行任何处理。

### <a name="header-files-to-include"></a>要包含的标头文件

将需要包含的标头文件`IInspectable`和`IMFTransform`驱动程序 MFT 必须实现的方法。 要包含的标头文件的列表，请参阅**stdafx.h**中**SampleMFT0**目录[UWP 用于相机的设备应用程序](https://go.microsoft.com/fwlink/p/?LinkID=227865)示例。

```cpp
// required for IInspectable
#include <inspectable.h>
```

### <a name="how-to-implement-iinspectable"></a>如何实现 IInspectable

驱动程序 MFT 的目标是使用从照相机的 UWP 设备应用程序必须实现的方法的`IInspectable`，以便 Microsoft Store 设备应用可以访问指向驱动程序 MFT 启动时的指针。 您的驱动程序 MFT 应实现的方法`IInspectable`，如下所示：

- **IInspectable::GetIids**应返回 null，在*iid* out 参数，并返回 0 *iidCount* out 参数。

- **IInspectable::GetRuntimeClassName**应返回 null，在输出参数。

- **IInspectable::GetRuntiGetTrustLevel**应返回`TrustLevel::BaseTrust`输出参数中。

下面的代码示例演示如何将`IInspectable`中的示例驱动程序 MFT 实现方法。 此代码可在**Mft0.cpp**文件中，在**SampleMFT0**示例的目录。

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

每个接口驱动程序 MFT 实现应实现和派生自`IUnknown`，以便正确封送到相机的 UWP 设备应用程序。 以下是一个示例 **.idl**驱动程序 MFT 演示此文件。

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

**请注意**驱动程序 MFT 是一个常规的 COM 类，可以使用创建`CoCreateInstance`。 不应使用`MFTRegister`函数以将其注册，因为它不是常规用途 MFT。

### <a name="creating-a-proxy"></a>创建代理

驱动程序 MFT 是一个进程外服务器。 若要在 UWP 设备应用中使用它，必须提供代理中的封送处理支持，以便在驱动程序 MFT 接口可以使用跨进程边界。 您可以找到出现在这种[驱动程序 MFT](https://go.microsoft.com/fwlink/p/?LinkID=251566)示例。 此示例使用 MIDL 编译器来生成无存根代理。

### <a name="exposing-the-driver-mft-to-apps"></a>公开到应用程序的驱动程序 MFT

若要在中编写的 UWP 设备应用程序C#或与驱动程序 MFT 交互的 JavaScript，则需进行 Microsoft Store 设备应用的 Microsoft Visual Studio 项目中创建一个附加组件。 此组件是公开可见的 Microsoft Store 设备应用到 Windows 运行时组件中的驱动程序 MFT 接口的包装。

中的包装器子项目[UWP 用于相机的设备应用程序](https://go.microsoft.com/fwlink/p/?LinkID=227865)示例举例说明如何将您的驱动程序 MFT 到 Windows 运行时公开，以便可以使用它从 UWP 设备应用中实现C#或 JavaScript。 它用于处理一起[驱动程序 MFT](https://go.microsoft.com/fwlink/p/?LinkID=251566)示例。 请参阅[驱动程序 MFT](https://go.microsoft.com/fwlink/p/?LinkID=251566)有关安装、 运行和测试示例的分步指南的示例页面。

## <a name="installing-and-registering-the-driver-mft"></a>安装和注册的驱动程序 MFT

本部分列出了安装驱动程序 MFT 的步骤：

1. 必须在以下位置中的子目录中安装驱动程序 MFT DLL:
    - %Systemdrive%\\程序文件\\
2. 您相机的安装程序通过调用注册的驱动程序 MFT **regsvr32**上您的驱动程序 MFT DLL，或通过安装程序使用来注册该 DLL 的清单 (.man) 文件提供一个驱动程序。
3. 设置`CameraPostProcessingPluginCLSID`照相机的注册表项中的值。 INF 文件应通过设置设备，设备类注册表项中指定的驱动程序 MFT CLSID`CameraPostProcessingPluginCLSID`到驱动程序 MFT 类的 CLSID 的 GUID 值。 以下是从填充照相机的注册表项的 INF 文件条目示例：

    ```cpp
    KSCATEGORY_VIDEO_CAMERA:

    [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceClasses\{E5323777-F976-4f5b-9B55-B94699C46E44}\##?#USB#VID_045E&PID_075D&MI_00#8&23C3DB65&0&0000#{E5323777-F976-4f5b-9B55-B94699C46E44}\#GLOBAL\Device Parameters]
    "CLSID"="{17CCA71B-ECD7-11D0-B908-00A0C9223196}"
    "FriendlyName"="USB Video Device"
    "RTCFlags"=dword:00000010
    "CameraPostProcessingPluginCLSID"="{3456A71B-ECD7-11D0-B908-00A0C9223196}" 



KSCATEGORY_CAPTURE:

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceClasses\{ 65E8773D-8F56-11D0-A3B9-00A0C9223196}\##?#USB#VID_045E&PID_075D&MI_00#8&23C3DB65&0&0000#{65E8773D-8F56-11D0-A3B9-00A0C9223196}\#GLOBAL\Device Parameters]
"CLSID"="{17CCA71B-ECD7-11D0-B908-00A0C9223196}"
"FriendlyName"="USB Video Device"
"RTCFlags"=dword:00000010
"CameraPostProcessingPluginCLSID"="{3456A71B-ECD7-11D0-B908-00A0C9223196}"
```

**请注意**`KSCATEGORY_VIDEO_CAMERA`建议针对相机。 通常情况下将只需要一个注册表项，具体取决于如何注册设备。


## <a name="associate-your-app-with-the-camera"></a>将您的应用程序与相机关联

本部分包含标识您的照相机和 Windows 注册表中的设备元数据所需的步骤的信息。 此元数据使您能够对 UWP 设备应用，并标识您的应用程序，以便可将其下载无缝第一次连接照相机。

### <a name="updates"></a>更新

在应用程序首次安装，如果用户下载更新的版本的应用程序中，然后更新会自动集成到相机捕获体验。 但是，更新将不会自动下载。 用户必须从 Microsoft Store 中，下载更多的应用更新，因为此应用经[自动安装](auto-install-for-uwp-device-apps.md)仅在第一个连接。 对 UWP 设备应用的主页可以提供通知更新可用，并提供链接以下载更新。

**重要**更新的应用程序应使用通过 Windows 更新分配任何更新的驱动程序。

### <a name="multiple-cameras"></a>多个照相机

多个相机模型可以声明相同的 UWP 设备应用在其设备元数据。 如果一个系统有多个内部嵌入的相机，照相机必须共享相同的 UWP 设备应用程序。 该应用包含用于确定哪个相机正在使用中，可以显示不同的 UI 中的每个相机逻辑及其**更多选项**体验。 有关自定义这种体验的详细信息，请参阅[如何自定义照相机选项](how-to-customize-camera-options.md)。

### <a name="internal-cameras"></a>内部相机

UWP 应用的内部相机的设备应用程序有资格[自动安装](auto-install-for-uwp-device-apps.md)从 Microsoft Store 中，但它们预装最无缝用户体验的建议。 一些支持内部相机并将其与关联的 UWP 设备应用程序所需的其他步骤。 有关详细信息，请参阅[确定内部相机的位置](identifying-the-location-of-internal-cameras.md)。

### <a name="creating-the-device-metadata-package"></a>创建设备元数据包

用于内部和外部相机，您需要创建设备元数据包。 当你照相机的 UWP 设备应用程序提交到 Microsoft Store （或预安装使用 OPK，在内部相机的情况下），除了应用自身，将需要提供包含以下元数据：

- 应用程序发布者名称
- 应用程序包名称
- 应用程序元素标识符
- 设备体验标识符

有关如何使用设备元数据来将您的应用程序与你的设备相关联的详细信息，请参阅[构建 UWP 设备应用](the-workflow.md)。

## <a name="related-topics"></a>相关主题

[构建 UWP 设备应用程序](the-workflow.md)

[UWP 设备应用的自动安装](auto-install-for-uwp-device-apps.md)

[硬件握手序列 (硬件 Mft)](https://go.microsoft.com/fwlink/p/?LinkId=320139)

[AVStream 微型驱动程序设计指南](https://go.microsoft.com/fwlink/p/?LinkID=228585)

[用于相机示例的 UWP 设备应用程序](https://go.microsoft.com/fwlink/p/?LinkID=227865)

[驱动程序 MFT 示例](https://go.microsoft.com/fwlink/p/?LinkID=251566)





