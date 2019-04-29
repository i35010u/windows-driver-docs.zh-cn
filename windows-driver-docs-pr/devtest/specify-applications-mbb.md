---
title: 在移动宽带元数据创作向导中指定应用程序
description: 在移动宽带元数据创作向导中指定应用程序
ms.assetid: 58E95326-94C4-444F-BFE2-0E7DC8112119
keywords:
- 在移动宽带元数据创作向导中指定应用程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2b5f8d3483f58e4b3ac3171373eb0d14472e654
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387922"
---
# <a name="specify-applications-in-the-mobile-broadband-metadata-authoring-wizard"></a>在移动宽带元数据创作向导中指定应用程序


若要指定不同的应用程序为你的服务，包括 Microsoft Store 的设备应用程序和权限的应用程序，请单击**应用程序**选项卡。

下载并安装在用户首次连接设备时 UWP 设备应用程序。 权限的应用程序具有特殊访问设备。 您可以指定只有各之一。

有关 UWP 的设备应用程序和权限的应用程序的详细信息，请参阅[Windows 8 设备体验](https://go.microsoft.com/fwlink/p/?LinkId=227312)。

## <a name="span-idtospecifythewindowsstoredeviceappspanspan-idtospecifythewindowsstoredeviceappspanspan-idtospecifythewindowsstoredeviceappspanto-specify-the-microsoft-store-device-app"></a><span id="To_specify_the_Windows_Store_device_app"></span><span id="to_specify_the_windows_store_device_app"></span><span id="TO_SPECIFY_THE_WINDOWS_STORE_DEVICE_APP"></span>指定的 Microsoft Store 设备应用


若要指定应用程序，请填写以下字段：

-   **包名称**。 应用程序清单的包元素中的标识元素中输入名称属性的值。
-   **发布者**。 应用程序清单的包元素中的标识元素中输入将 Publisher 属性的值。 此值必须与安装在电脑上的发布服务器证书。
-   **应用程序 ID**。 应用程序清单的应用程序元素中输入的 ID 属性的值。

**包名称**，**发布者**，并**应用程序 ID**所有必须匹配应用 package.appxmanifest 中的信息。

下面是应用程序清单的示例：

```
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

## <a name="span-idtoseethepackagenameandpublisherspanspan-idtoseethepackagenameandpublisherspanspan-idtoseethepackagenameandpublisherspanto-see-the-package-name-and-publisher"></a><span id="To_see_the_Package_name_and_Publisher"></span><span id="to_see_the_package_name_and_publisher"></span><span id="TO_SEE_THE_PACKAGE_NAME_AND_PUBLISHER"></span>若要查看的包名称和发布服务器


1.  在 Visual Studio 中打开应用解决方案。
2.  单击解决方案资源管理器中的应用程序清单。
3.  双击“Package.appxmanifest”。
4.  在中**打包**选项卡上，查看**包名称**并**发布服务器**字段。

## <a name="span-idtoseetheappidspanspan-idtoseetheappidspanspan-idtoseetheappidspanto-see-the-app-id"></a><span id="To_see_the_App_ID_"></span><span id="to_see_the_app_id_"></span><span id="TO_SEE_THE_APP_ID_"></span>若要查看应用程序 ID


1.  在 Visual Studio 中打开应用解决方案。
2.  单击解决方案资源管理器中的应用程序清单。
3.  右键单击 Package.appxmanifest。
4.  选择**查看代码**。

## <a name="span-idprivilegedapplicationsspanspan-idprivilegedapplicationsspanspan-idprivilegedapplicationsspanprivileged-applications"></a><span id="Privileged_applications"></span><span id="privileged_applications"></span><span id="PRIVILEGED_APPLICATIONS"></span>权限的应用程序


为 Microsoft Store 的设备应用来访问特权的移动宽带接口，它需要下指定**权限的应用程序**。

若要指定权限的应用程序，填写以下字段下**权限的应用程序**:

**请注意**  有关的以下字段的详细信息，请参阅[Windows 8 设备体验](https://go.microsoft.com/fwlink/p/?LinkId=242009)。 有关特权设备接口属性项的信息，请参阅[DEVPKEY\_DeviceInterface\_Restricted](https://go.microsoft.com/fwlink/p/?linkid=256362)。

 

-   **包名称**。 应用程序清单的包元素中的标识元素中输入名称属性的值。
-   **发布者**。 应用程序清单的包元素中的标识元素中输入将 Publisher 属性的值。

下面是应用程序清单的示例：

```
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

## <a name="span-iddevicenotificationhandlerspanspan-iddevicenotificationhandlerspanspan-iddevicenotificationhandlerspandevice-notification-handler"></a><span id="Device_Notification_Handler"></span><span id="device_notification_handler"></span><span id="DEVICE_NOTIFICATION_HANDLER"></span>设备通知处理程序


移动宽带平台提供了用于接收和显示 m n O 管理短信或 USSD 通知，如接近数据使用限制、 国际漫游和低余额的增强的功能。 它还提供功能的响应数据使用情况和连接、 断开连接，或适用于移动网络提供商漫游 UWP 应用中的后台事件。

Windows 提供用于 UWP 应用运行一些代码以响应事件，即使 Microsoft Store 应用程序未运行的 broker 工具。 有关实现通知处理程序的详细信息，请参阅[启用移动运营商通知和系统事件](https://go.microsoft.com/fwlink/p/?linkid=242062)。

 

 





