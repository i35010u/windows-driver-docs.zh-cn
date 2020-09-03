---
title: 在移动宽带元数据创作向导中指定应用程序
description: 在移动宽带元数据创作向导中指定应用程序
ms.assetid: 58E95326-94C4-444F-BFE2-0E7DC8112119
keywords:
- 在移动宽带元数据创作向导中指定应用程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c303e70f76e80a236e66f754a9bf9192652b3b3d
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384319"
---
# <a name="specify-applications-in-the-mobile-broadband-metadata-authoring-wizard"></a>在移动宽带元数据创作向导中指定应用程序

若要为服务指定不同的应用程序（包括 Microsoft Store 设备应用和特权应用程序），请单击 " **应用程序** " 选项卡。

当用户首次连接设备时，将下载并安装 UWP 设备应用。 特权应用程序具有设备的特殊访问权限。 只能指定其中的一个。

## <a name="to-specify-the-microsoft-store-device-app"></a>指定 Microsoft Store 设备应用

若要指定应用，请填写以下字段：

- **包名称**。 在应用程序清单的 Package 元素中的 Identity 元素中输入 Name 属性的值。
- **发布者**。 在应用程序清单的 Package 元素中的 Identity 元素中输入 "发布服务器" 属性的值。 此值必须与计算机上安装的发布者证书匹配。
- **应用 ID**。 在应用程序清单的应用程序元素中输入 ID 属性的值。

**包名称**、**发布者**和**应用 ID**全部必须与应用程序包中的信息相匹配。 appxmanifest.xml。

下面是应用程序清单的示例：

```xml
<?xml version="1.0" encoding="utf-8" ?>
   <Package xmlns="http://schemas.microsoft.com/appx/2010/manifest">
      <Identity Name="Microsoft.SDKSamples.MoFx2App" Version="1.0.0.0" Publisher="CN=Microsoft\O=Microsoft Corp\L=Redmond\S=WA\C=US" ResourceId="NorthAmerica" />
   <Properties>
     <DisplayName>MoFx2App SDK Sample</DisplayName>
     <Description>MoFx2App SDK Sample</Description>
     <Logo>images\tile-sdk.png</Logo>
   </Properties>
<Resources>
  <Resource Language="en-us" />
</Resources>
<Applications>
  <Application Id="Microsoft.SDKSamples.MoFx2App" DisplayName="MoFx2App" Logo="images\tile-sdk.png" SmallLogo="images\tile-sdk.png" EntryPointType="startPage" EntryPoint="default.html">
```

## <a name="to-see-the-package-name-and-publisher"></a>查看包名称和发布服务器

1. 在 Visual Studio 中打开应用程序解决方案。
2. 单击解决方案资源管理器中的应用程序清单。
3. 双击“Package.appxmanifest”。
4. 在 " **打包** " 选项卡中，查看 " **包名称** " 和 " **发布者** " 字段。

## <a name="to-see-the-app-id"></a>查看应用 ID

1. 在 Visual Studio 中打开应用程序解决方案。
2. 单击解决方案资源管理器中的应用程序清单。
3. 右键单击 appxmanifest.xml。
4. 选择 " **查看代码**"。

## <a name="privileged-applications"></a>特权应用程序

要使 Microsoft Store 设备应用访问特权移动宽带接口，需要在 **特权应用程序**下指定它。

若要指定特权应用程序，请在 **特权应用程序**下填写以下字段：

>[!NOTE]
>有关特权设备接口属性密钥的信息，请参阅 [DEVPKEY \_ DeviceInterface \_ 限制](../install/devpkey-deviceinterface-restricted.md)。

- **包名称**。 在应用程序清单的 Package 元素中的 Identity 元素中输入 Name 属性的值。
- **发布者**。 在应用程序清单的 Package 元素中的 Identity 元素中输入 "发布服务器" 属性的值。

下面是应用程序清单的示例：

```xml
<?xml version="1.0" encoding="utf-8" ?>
   <Package xmlns="http://schemas.microsoft.com/appx/2010/manifest">
      <Identity Name="Microsoft.SDKSamples.MoFx2App" Version="1.0.0.0" Publisher="CN=Microsoft\O=Microsoft Corp\L=Redmond\S=WA\C=US" ResourceId="NorthAmerica" />
   <Properties>
     <DisplayName>MoFx2App SDK Sample</DisplayName>
     <Description>MoFx2App SDK Sample</Description>
     <Logo>images\tile-sdk.png</Logo>
   </Properties>
<Resources>
  <Resource Language="en-us" />
</Resources>
<Applications>
  <Application Id="Microsoft.SDKSamples.MoFx2App" DisplayName="MoFx2App" Logo="images\tile-sdk.png" SmallLogo="images\tile-sdk.png" EntryPointType="startPage" EntryPoint="default.html">
```

## <a name="device-notification-handler"></a>设备通知处理程序

移动宽带平台提供了增强的功能，可用于接收和显示 o 的管理短信或 USSD 通知，如接近数据使用量上限、国际化漫游和低平衡。 它还提供了用于响应移动网络提供程序的 UWP 应用中的数据使用和连接、断开或漫游背景事件的功能。

Windows 提供适用于 UWP 应用的 broker 功能，以运行某些代码来响应事件，即使 Microsoft Store 应用未运行也是如此。 有关实现通知处理程序的详细信息，请参阅 [启用移动运营商通知和系统事件简介](../mobilebroadband/enabling-mobile-operator-notifications-and-system-events.md)。