---
title: 面向应用开发人员的硬件支持应用程序 (HSA) 步骤
description: 开发自定义功能的硬件支持应用程序 (HSA) 的指南
keywords:
- 自定义功能
- UWP 应用
- 自定义功能
- UWP
- 硬件
ms.date: 08/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f362f1de55cd44db984bd28926f2bd42c4add3d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369386"
---
# <a name="hardware-support-app-hsa-steps-for-app-developers"></a>硬件支持应用 (HSA)：适用于应用开发人员的步骤

本主题介绍如何将驱动程序相关联的特定于设备的应用程序或[RPC （远程过程调用）](https://docs.microsoft.com/windows/desktop/Rpc/rpc-start-page)终结点。  如果搭配使用以这种方式，应用程序即为作为硬件支持应用程序 (HSA)。  分发和更新硬件支持应用程序，通过 Microsoft Store。

开头[通用 Windows 平台 (UWP) 应用](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide)或桌面 (Win32) 应用。  如果你想要使用桌面应用程序，使用[桌面桥](https://docs.microsoft.com/windows/uwp/porting/desktop-to-uwp-root)创建 Windows 应用程序包可以上传到存储区。

此页介绍了为 UWP 应用，该过程，但步骤是类似于 Win32 选项。 

驱动程序开发人员的步骤所述[硬件支持应用程序 (HSA):适用于驱动程序开发人员的步骤](hardware-support-app--hsa--steps-for-driver-developers.md)。

## <a name="getting-started"></a>入门

首先，安装最新版本的 Visual Studio 并创建 UWP 应用项目。  若要生成 UWP 应用，而自定义功能，您将需要 Windows SDK 版本 10.0.15063 （Windows 10 创意者更新） 或更高版本。 你的项目文件还必须指定版本 10.0.15063 或更高版本。 获取配置的更多帮助，请参阅[使用 Visual Studio 开发 UWP 应用](/windows/uwp/develop/)。

从 Windows 10 1709年版开始，可以指定特定驱动程序是否存在应仅加载通用 Windows 平台 (UWP) 应用。  若要了解如何操作，请参阅[配对使用 UWP 应用的驱动程序](../install/pairing-app-and-driver-versions.md)。

## <a name="create-a-microsoft-store-account"></a>创建 Microsoft Store 帐户

Microsoft Store 上的开发人员帐户是必需的。 硬件合作伙伴将需要不同于其硬件合作伙伴帐户的 Microsoft Store 帐户。 当您编写应用程序清单和更高版本的步骤中的设备元数据时，将需要发布者名称。 创建存储配置文件后，你也可以保留您的应用程序的名称。

若要创建的 Microsoft Store 帐户，请转到[UWP 应用注册页](https://go.microsoft.com/fwlink/p/?LinkId=302197)。 有关详细信息，请参阅[打开开发人员帐户](https://docs.microsoft.com/windows/uwp/publish/opening-a-developer-account)。

## <a name="choosing-a-programming-language-for-the-app"></a>选择应用程序的编程语言

如果您的应用程序将与驱动程序进行通信，则可以使用[Windows.Devices.Custom](https://docs.microsoft.com/uwp/api/windows.devices.custom)，这是 WinRT API 的一部分，因此可在 JavaScript 中， C#，并C++。

如果您的应用程序将与 NT 服务进行通信，然后您需要使用 RPC Api。  因为 RPC Api 是在 WinRT 中不可用的 Win32 Api，你需要使用C++，或将包装的 RPC 调用使用.NET 互操作 (PInvoke)。  有关详细信息，请参阅[从托管代码调用本机函数](https://docs.microsoft.com/cpp/dotnet/calling-native-functions-from-managed-code)。

## <a name="contact-the-custom-capability-owner"></a>与自定义功能所有者联系

现在你已准备好请求功能所有者从自定义功能的访问。  你将需要收集以下信息：

-   从 Microsoft Store 应用 PFN （包系列名称）
-   自定义功能的名称
-   应用签名可从你使用 certutil.exe 的.cer 文件生成的证书的签名哈希值。 该证书必须是 SHA-256。

若要生成的签名哈希值，请运行`C:\Windows\System32\certutil.exe -dump CertificateName.cer`。

底部附近的签名哈希查找，并确保它为 SHA256。  否则，使用 SHA256 证书对应用签名。  结果应如下所示：

```cpp
Signature Hash:
ca9fc964db7e0c2938778f4559946833e7a8cfde0f3eaa07650766d4764e86c4
```

功能所有者使用此信息来生成[签名的自定义功能描述符](hardware-support-app--hsa--steps-for-driver-developers.md#sccd-xml-schema)文件，并将此文件发送到应用程序开发人员。

应用程序开发人员可以继续等待功能所有者批准该申请时开发带有自定义功能在开发人员模式下的应用程序。 例如，使用以下中在台式计算机上 SCCD[开发人员模式](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development):

-   目录 SCCD 中的条目。

    ```xml
    <Catalog>FFFF</Catalog>
    ```
-   授权的实体项 SCCD 中证书签名哈希。 虽然它不强制也不验证，请将放 64 字符序列。

    ```xml
    <AuthorizedEntity AppPackageFamilyName="MicrosoftHSATest.Microsoft.SDKSamples.Hsa.CPP_q536wpkpf5cy2" CertificateSignatureHash="ca9fc964db7e0c2938778f4559946833e7a8cfde0f3eaa07650766d4764e86c4"></AuthorizedEntity>
    ```

## <a name="add-a-custom-capability-to-the-app-package-manifest"></a>将自定义功能添加到应用程序的包清单

接下来，修改您[应用程序包清单](https://docs.microsoft.com/uwp/schemas/appxpackage/appx-package-manifest)源文件 (`Package.appxmanifest`)，包含功能属性。

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

然后将 SCCD 文件复制到 appx 包的包根目录中。 在 Visual Studio 的解决方案资源管理器中，右键单击"项目-&gt;添加-&gt;现有项..." 若要将 SCCD 添加到你的项目。

![将 SCCD 文件添加到 appx 包](images/addSCCDToAppx.png)

将标记作为通过右键单击 SCCD 文件并更改生成内容 SCCD**内容**到**True**。  有关C#项目中，使用属性`Build Action = Content`，对于 JavaScript 项目，并用`Package Action = Content`。 

![将 SCCD 标记作为内容](images/markSCCDAsContent.png)

最后，右键单击该项目中，选择**应用商店**，然后**创建应用程序包**。

**注意**：没有适用于 UWP 应用与移动平台上的自定义功能支持。

## <a name="install-the-app"></a>安装应用

若要预安装 UWP 应用，而自定义功能，请使用[DISM-部署映像服务和管理](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism---deployment-image-servicing-and-management-technical-reference-for-windows)。

## <a name="troubleshooting"></a>疑难解答

开发人员模式下在目标计算机时，可以尝试以下步骤来调试应用程序注册失败：

1.  AppX 清单中删除自定义功能条目。
2.  构建您的应用程序并将其部署。
3.  在 PowerShell 窗口中，键入`Get-AppxPackage`。
4.  查找你的应用列表中，并验证您的应用程序的完全相同的包系列名称。
5.  更新你 SCCD 的包系列名称。
6.  添加自定义功能项恢复到 AppX 清单。
7.  重新生成并部署。 

## <a name="see-also"></a>请参阅

* [硬件支持应用 (HSA)：适用于驱动程序开发人员的步骤](hardware-support-app--hsa--steps-for-driver-developers.md)
* [启用设备进行开发](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development)
* [自定义功能示例](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CustomCapability)
* [通用 Windows 驱动程序入门](../develop/getting-started-with-universal-drivers.md)
* [配对的驱动程序有一个通用 Windows 平台 (UWP) 应用程序](../install/pairing-app-and-driver-versions.md)
* [通用 Windows 平台简介](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide)
* [通用 Windows 平台 (UWP)](https://docs.microsoft.com/windows/uwp/design/basics/design-and-ui-intro)
