---
title: 适用于应用开发人员的硬件支持应用（HSA）步骤
description: 使用自定义功能开发硬件支持应用（HSA）的指南
keywords:
- 自定义，功能
- UWP 应用
- 自定义功能
- UWP
- 硬件
ms.date: 08/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed2ed079ee815762a788ec37c62cbb53f1efd621
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235426"
---
# <a name="hardware-support-app-hsa-steps-for-app-developers"></a>硬件支持应用（HSA）：应用开发人员的步骤

本主题介绍如何将设备特定的应用程序与驱动程序或[RPC （远程过程调用）](https://docs.microsoft.com/windows/desktop/Rpc/rpc-start-page)终结点相关联。  当配对时，应用被称为硬件支持应用（HSA）。  可以通过 Microsoft Store 分发和更新硬件支持应用。

从[通用 Windows 平台（UWP）应用](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide)或桌面（Win32）应用开始。  如果你想要使用桌面应用，请使用[桌面桥](https://docs.microsoft.com/windows/uwp/porting/desktop-to-uwp-root)创建 Windows 应用包，你可以将其上传到应用商店。

此页介绍了 UWP 应用的过程，但在 Win32 选项中的步骤是类似的。 

有关驱动程序开发人员的步骤，请参阅[硬件支持应用（HSA）：驱动程序开发人员的步骤](hardware-support-app--hsa--steps-for-driver-developers.md)。

## <a name="getting-started"></a>入门

首先，安装最新版本的 Visual Studio 并创建 UWP 应用项目。  若要使用自定义功能生成 UWP 应用，需要 Windows SDK 版本10.0.15063 （Windows 10 创意者更新）或更高版本。 项目文件还必须指定 version 10.0.15063 或更高版本。 有关配置的更多帮助，请参阅[使用 Visual Studio 开发 UWP 应用](/windows/uwp/develop/)。

从 Windows 10 版本1709开始，你可以指定通用 Windows 平台（UWP）应用只应在存在特定驱动程序时加载。  若要了解如何操作，请参阅[将驱动程序与 UWP 应用配对](../install/pairing-app-and-driver-versions.md)。

## <a name="create-a-microsoft-store-account"></a>创建 Microsoft Store 帐户

需要 Microsoft Store 上的开发人员帐户。 硬件伙伴需要不同于其硬件伙伴帐户的 Microsoft Store 帐户。 在后续步骤中创作应用程序清单和设备元数据时，需要发布者名称。 创建存储配置文件后，还可以为应用保留一个名称。

若要创建 Microsoft Store 帐户，请参阅[UWP 应用注册页](https://go.microsoft.com/fwlink/p/?LinkId=302197)。 有关详细信息，请参阅[打开开发人员帐户](https://docs.microsoft.com/windows/uwp/publish/opening-a-developer-account)。

## <a name="choosing-a-programming-language-for-the-app"></a>为应用程序选择编程语言

如果你的应用程序将与驱动程序通信，则可以使用[Windows. Custom](https://docs.microsoft.com/uwp/api/windows.devices.custom)，它是 WinRT API 的一部分，因此在 JavaScript、c # 和 c + + 中可用。

如果你的应用程序将与 NT 服务通信，则需要使用 RPC Api。  由于 RPC Api 是不能在 WinRT 中使用的 Win32 Api，因此需要使用 c + +，或使用 .NET 互操作（PInvoke）包装 RPC 调用。  有关详细信息，请参阅[从托管代码调用本机函数](https://docs.microsoft.com/cpp/dotnet/calling-native-functions-from-managed-code)。

## <a name="contact-the-custom-capability-owner"></a>与自定义功能所有者联系

现在，你已准备好从功能所有者请求对自定义功能的访问权限。  需要收集以下信息：

-   Microsoft Store 中的应用 PFN （包系列名称）
-   自定义功能的名称
-   应用签名证书的签名哈希，可使用 certutil 从 .cer 文件生成。 证书必须是 SHA-256。

若要生成签名哈希，请运行 `C:\Windows\System32\certutil.exe -dump CertificateName.cer` 。

查找底部附近的签名哈希，并确保其为 SHA256。  否则，请使用 SHA256 证书对应用进行签名。  结果应如下所示：

```cpp
Signature Hash:
ca9fc964db7e0c2938778f4559946833e7a8cfde0f3eaa07650766d4764e86c4
```

功能所有者使用此信息生成[签名的自定义功能描述符](hardware-support-app--hsa--steps-for-driver-developers.md#sccd-xml-schema)文件，并将此文件发送给应用开发人员。

应用开发人员可以继续使用开发人员模式开发自定义功能，同时等待功能所有者批准请求。 例如，在[开发人员模式下](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development)，在台式计算机上的 SCCD 中使用以下内容：

-   SCCD 中的目录条目。

    ```xml
    <Catalog>FFFF</Catalog>
    ```
-   SCCD 中授权实体条目中的证书签名哈希。 尽管既未强制实施也未验证64，

    ```xml
    <AuthorizedEntity AppPackageFamilyName="MicrosoftHSATest.Microsoft.SDKSamples.Hsa.CPP_q536wpkpf5cy2" CertificateSignatureHash="ca9fc964db7e0c2938778f4559946833e7a8cfde0f3eaa07650766d4764e86c4"></AuthorizedEntity>
    ```

## <a name="add-a-custom-capability-to-the-app-package-manifest"></a>将自定义功能添加到应用程序包清单

接下来，将[应用程序包清单](https://docs.microsoft.com/uwp/schemas/appxpackage/appx-package-manifest)源文件（ `Package.appxmanifest` ）修改为包含功能属性。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Package
  ...
  xmlns:uap4="http://schemas.microsoft.com/appx/manifest/uap/windows10/4">
...
<Capabilities>
    <uap4:CustomCapability Name="CompanyName.customCapabilityName_PublisherID"/>
</Capabilities>
</Package>
```

然后，将 SCCD 文件复制到 appx 包的包根目录。 在 Visual Studio 的解决方案资源管理器中，右键单击 "项目- &gt; 添加 &gt; 现有项 ..." 将 SCCD 添加到你的项目。

![将 SCCD 文件添加到 appx 包](images/addSCCDToAppx.png)

右键单击 SCCD 文件，然后将**内容**更改为**TRUE**，将 SCCD 标记为 "生成内容"。  对于 c # 项目，请使用属性 `Build Action = Content` ，对于 JavaScript 项目，请使用 `Package Action = Content` 。 

![将 SCCD 标记为内容](images/markSCCDAsContent.png)

最后，右键单击项目，选择 "**存储**"，然后单击 "**创建应用包**"。

**注意**：不支持在移动平台上具有自定义功能的 UWP 应用。

## <a name="install-the-app"></a>安装应用程序

若要使用自定义功能预安装 UWP 应用，请使用[DISM-部署映像服务和管理](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism---deployment-image-servicing-and-management-technical-reference-for-windows)。

## <a name="troubleshooting"></a>疑难解答

如果目标计算机处于开发人员模式，则可以尝试以下步骤来调试应用注册失败：

1.  删除 AppX 清单中的自定义功能条目。
2.  生成并部署你的应用。
3.  在 PowerShell 窗口中，键入 `Get-AppxPackage` 。
4.  在列表中查找应用，并验证应用的确切包系列名称。
5.  将 SCCD 更新为包系列名称。
6.  将自定义功能条目添加回 AppX 清单中。
7.  重新生成并部署。 

## <a name="see-also"></a>另请参阅

* [硬件支持应用（HSA）：驱动程序开发人员的步骤](hardware-support-app--hsa--steps-for-driver-developers.md)
* [启用设备进行开发](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development)
* [自定义功能示例](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CustomCapability)
* [Windows 驱动程序入门](../develop/getting-started-with-windows-drivers.md)
* [将驱动程序与通用 Windows 平台 (UWP) 应用配对](../install/pairing-app-and-driver-versions.md)
* [通用 Windows 平台简介](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide)
* [通用 Windows 平台 (UWP)](https://docs.microsoft.com/windows/uwp/design/basics/design-and-ui-intro)
