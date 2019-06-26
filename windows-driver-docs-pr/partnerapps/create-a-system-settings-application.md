---
title: 创建合作伙伴设置应用
description: 创建合作伙伴设置应用
ms.assetid: 3b549c11-f8b2-46e8-9d22-4edc787743ee
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7417af3e917a7bc6d0aed64ddd8db2511a914183
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353577"
---
# <a name="create-a-partner-settings-app"></a>创建合作伙伴设置应用

Oem 和移动运营商可以公开自定义功能设置的设备硬件将它与其他设备区分开来。 一些示例包括扬声器、 传感器、 或麦克风。 最多五个这些自定义设置将显示为一个设置应用的级别的两个页面中的其他链接。  

例如，在**设备**选项卡**设置**应用程序中，以下页每个最多可有五个自定义设置应用到的其他链接：

* 打印机和扫描仪
* 连接的设备
* 蓝牙
* 鼠标
* 触摸板
* 键入
* 笔和 Windows Ink
* AutoPlay
* USB

![在设置应用中的设备列表](images/devices-list-in-settings.png)

您可以找到一系列中的所有级别两个页面[启动 Windows 设置应用](https://docs.microsoft.com/windows/uwp/launch-resume/launch-settings-app)主题。 请务必注意，必须与在放入的页面相关的所有链接。

此外，您就能够将最多五个搜索词添加在每个页上，它必须是与页面上的内容。 为获得最佳的搜索体验，使用特定的短语。 使用常规和一个 word 条款可能会导致您不相关搜索结果中出现的链接。  

例如，如果你有"Fabricam multipen"设备，创建搜索短语，例如"设置 fabricam mulitipen"而不是泛型的搜索词，例如"笔"。

## <a name="characteristics-of-partner-settings-app"></a>合作伙伴设置应用程序的特征

合作伙伴设置应用具有以下特征：

* 它们是通用 Windows 平台 (UWP) 应用或 Windows Phone Silverlight 应用程序。

* 用户可以卸载它们直接，其他应用一样。

* 它们可以通过更新存储区，如其他 Windows 应用中的设置应用程序进行升级。

* 它们是在首次启动安装的预安装应用程序。

    与任何其他预安装应用程序，合作伙伴必须提交到 Windows 开发人员中心，以便为系统设置应用程序：
  * 认证应用程序
  * 获取已签名的.appx 文件和要包含在设备图像中的应用程序所需的许可证文件。

* 它们被发布到用户无法浏览到或使用搜索查找的存储区中的隐藏位置。

## <a name="creating-system-settings-applications"></a>创建系统设置应用程序

> [!NOTE]
> 设置应用程序通用 Windows 平台应用，应遵守所有 UWP 编程原则。 请参阅[适用于通用 Windows 平台 (UWP) 应用准则](https://developer.microsoft.com/windows/apps/design)有关详细信息。

1. 使用 Windows 软件开发工具包 (SDK) 来创建 Windows 通用应用。 创建 Windows 通用应用程序的详细信息，请参阅[使用 Visual Studio 构建 UWP 应用](https://docs.microsoft.com/windows/uwp/get-started/create-uwp-apps)。

    如果您要编写面向 Windows Phone 的设置应用程序，还可以创建 Windows Phone Silverlight 应用程序。

2. 在以下应用程序清单：

    `xmlns:rescap=http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities`
  
    描述页在你的应用程序链接列出使用`SettingsPageUri`属性。 使用`AppActivationMode`属性以指向此链接。 使用下面的代码示例为例：

    ```xml
    <Extensions>
      <rescap:Extension Category="windows.settingsApp">
        <rescap:SettingsApp SettingsPageUri="ms-settings:yourl2pageuri">
          <rescap:AppLinks>
            <rescap:Link AppActivationMode ="uri://yourapp#deeplink" DisplayName="Link 1 Title" />
            <rescap:Link AppActivationMode ="uri://yourapp#deeplink" DisplayName="Link 2 Title" />
          </rescap:AppLinks>
            <rescap:SearchTerms>
            <rescap:Term>setup foo</rescap:Term>
            <rescap:Term>disable foo</rescap:Term>
            </rescap:SearchTerms>
          </rescap:SettingsApp>
        </rescap:Extension>
    </Extensions>
    ```

   请注意此包中的所有应用列表不能有一个条目。 若要完成此操作，设置[AppListEntry](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.applistentry)属性设置为**none**。

    ```xml
     <uap:VisualElements AppListEntry="none" DisplayName="OptionalPackage"
       ....
     </uap:VisualElements>
    ```

3. 若要将配置为预安装的应用程序，你设置应用程序提交到 Windows 开发人员中心。 接收已签名的.appx 文件并获取许可证文件之后, 在设备图像中包括的应用。

## <a name="updating-system-settings-applications"></a>更新系统设置的应用程序

提交到 Microsoft Store 设置应用程序更新。 提交更新后，已安装的设置应用程序的客户更新通知，并可安装更新，通过应用商店。

系统设置应用程序不会显示在设备应用程序列表中。 为避免混淆，用户会收到通知的应用程序的更新时，请确保其应用商店说明指定，它提供了系统级设置，显示在**设置**设备。

## <a name="what-happens-to-legacy-control-panel-or-system-settings-apps-when-the-os-upgrades-to-windows-10"></a>在 OS 升级到 Windows 10，传统控件面板或系统设置应用程序会发生什么情况

如果控制面板应用程序专为 Windows 7、 8 或 Windows 8.1，它将继续工作并 （之前的未来版本中删除），会显示旧的控制面板中，但不会显示在 Windows 10 系统设置应用并支持任何其功能。

同样，如果您的旧系统设置的应用程序专为 Windows 8 或 Windows 8.1，它将继续工作，但将不支持任何 Windows 10 系统设置应用的功能。
