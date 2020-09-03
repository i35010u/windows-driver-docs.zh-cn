---
title: 创建合作伙伴设置应用
description: 创建合作伙伴设置应用
ms.assetid: 3b549c11-f8b2-46e8-9d22-4edc787743ee
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85f95cab56ef9f640dee7df5ce8ccde9b4ed3e53
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383559"
---
# <a name="create-a-partner-settings-app"></a>创建合作伙伴设置应用

Oem 和移动运营商可以公开设备硬件功能的自定义设置，以便将其与其他设备区分开来。 一些示例包括扬声器、传感器或麦克风。 在其中一个 "设置" 应用的级别中，多达5个自定义设置将显示为其他链接。  

例如，在 "**设置**" 应用的 "**设备**" 选项卡中，每个页面可以具有多达五个指向自定义设置应用的其他链接：

* 打印机和扫描仪
* 已连接的设备
* 蓝牙
* 鼠标
* 触摸板
* Typing
* 笔和 Windows Ink
* 自动播放
* USB

![设置应用中的设备列表](images/devices-list-in-settings.png)

你可以在 [启动 Windows 设置应用](/windows/uwp/launch-resume/launch-settings-app) 主题中找到所有级别为两页的列表。 请务必注意，所有链接都必须与它们所在的页面相关。

此外，还可以在每个页面上添加最多五个搜索词，它们必须与页面上的内容相关。 为了获得最佳搜索体验，请使用特定短语。 使用 "常规" 和 "单字" 条件可能会导致链接不会出现在相关搜索中。  

例如，如果你有一个 "Fabricam.com multipen" 设备，请创建一个搜索短语，如 "设置 fabricam.com mulitipen"，而不是 "笔" 等通用搜索词。

## <a name="characteristics-of-partner-settings-app"></a>合作伙伴设置应用的特征

合作伙伴设置应用具有以下特征：

* 它们是通用 Windows 平台 (UWP) 应用程序或 Windows Phone Silverlight 应用程序。

* 用户可以直接卸载它们，如其他应用。

* 可以通过更新存储中的 "设置" 应用程序来升级它们，如其他 Windows 应用程序。

* 它们是首次启动时安装的预安装应用程序。

    与任何其他预安装的应用程序一样，合作伙伴必须将系统设置应用程序提交到 Windows 开发人员中心，才能：
  * 认证应用程序
  * 获取在设备映像中包含应用程序所需的已签名的 .appx 文件和许可证文件。

* 它们发布到应用商店中的隐藏位置，用户无法使用搜索进行浏览或查找。

## <a name="creating-system-settings-applications"></a>创建系统设置应用程序

> [!NOTE]
> 设置应用程序通用 Windows 平台应用程序，应符合所有 UWP 编程准则。 有关详细信息，请参阅 [通用 Windows 平台 (UWP) 应用的准则](https://developer.microsoft.com/windows/apps/design) 。

1. 使用 Windows 软件开发工具包 (SDK) 创建 Windows 通用应用。 有关创建 Windows 通用应用的详细信息，请参阅 [使用 Visual Studio 生成 UWP 应用](/windows/uwp/get-started/create-uwp-apps)。

    如果要将设置应用目标 Windows Phone，还可以创建 Windows Phone 的 Silverlight 应用。

2. 在下面的应用程序清单中：

    `xmlns:rescap=http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities`
  
    使用属性描述应用程序链接所列出的页面 `SettingsPageUri` 。 使用 `AppActivationMode` 特性指向此链接。 使用下面的代码示例作为示例：

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

   请注意，此包不能包含 "所有应用" 列表中的条目。 若要实现此目的，请将 [AppListEntry](/uwp/api/windows.applicationmodel.core.applistentry) 属性设置为 **none**。

    ```xml
     <uap:VisualElements AppListEntry="none" DisplayName="OptionalPackage"
       ....
     </uap:VisualElements>
    ```

3. 若要将配置为预安装的应用程序，请将设置应用程序提交到 Windows 开发人员中心。 接收到已签名的 .appx 文件并获取许可证文件后，在设备映像中包括该应用程序。

## <a name="updating-system-settings-applications"></a>更新系统设置应用程序

将设置应用程序更新提交到 Microsoft Store。 提交更新后，已安装设置应用的客户将收到更新通知，并可通过应用商店安装更新。

"系统设置" 应用不会显示在 "设备应用程序列表" 中。 若要避免在用户收到应用更新通知时产生混淆，请确保其存储说明指定它提供了在设备的 " **设置** " 中显示的系统级设置。

## <a name="what-happens-to-legacy-control-panel-or-system-settings-apps-when-the-os-upgrades-to-windows-10"></a>如果 OS 升级到 Windows 10，旧版控制面板或系统设置应用会发生什么情况

如果你的控制面板应用程序是为 Windows 7、Windows 8 或 Windows 8.1 编写的，则该应用程序将继续工作，并在旧控制面板中显示 (，直到在将来的版本) 中将其删除，但不会在 Windows 10 系统设置应用中显示，并支持其任何功能。

同样，如果你的旧系统设置应用是为 Windows 8 或 Windows 8.1 编写的，则该应用程序将继续运行，但不支持 Windows 10 系统设置应用程序的任何功能。