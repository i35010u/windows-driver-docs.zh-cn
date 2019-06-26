---
title: 在设备元数据创作向导中指定应用程序
description: 在设备元数据创作向导中指定应用程序
ms.assetid: B3ECEBF3-FBC6-45E7-9FF5-439F1CDF351F
keywords:
- 在设备元数据创作向导中指定应用程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbd76aa954f2063e228e33e48627207e1ba9bdc1
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391959"
---
# <a name="specify-applications-in-the-device-metadata-authoring-wizard"></a>在设备元数据创作向导中指定应用程序


您可以为你的设备，包括 Microsoft Store 设备应用和特权应用程序指定各种应用程序。

下载并安装在用户首次连接设备时 UWP 设备应用程序。 权限的应用程序具有特殊访问设备。 您可以指定只有各之一。

有关 UWP 设备应用程序和权限的应用程序的详细信息，请参阅[Windows 8 设备体验](https://go.microsoft.com/fwlink/p/?LinkId=227312)。

## <a name="span-idtospecifythewindowsstoredeviceappspanspan-idtospecifythewindowsstoredeviceappspanspan-idtospecifythewindowsstoredeviceappspanto-specify-the-microsoft-store-device-app"></a><span id="To_specify_the_Windows_Store_device_app"></span><span id="to_specify_the_windows_store_device_app"></span><span id="TO_SPECIFY_THE_WINDOWS_STORE_DEVICE_APP"></span>指定的 Microsoft Store 设备应用


1.  单击“应用程序”  选项卡。
2.  填写以下字段：
    -   **包名称**。 应用程序清单的包元素中的标识元素中输入名称属性的值。 包名称应获取应用程序提交到 Microsoft Store 创建之后，因为通过 Microsoft Store 提交过程发生了更改包名称。 请参阅[UWP 设备应用程序生命周期](https://go.microsoft.com/fwlink/p/?linkid=246571)有关如何使用 Microsoft Store 将应用程序并将更新后的值复制到应用程序清单的详细信息。
    -   **发布者**。 应用程序清单的包元素中的标识元素中输入将 Publisher 属性的值。 发布者名称应与开发人员中的一个相同用于包和元数据进行签名的证书。
    -   **应用程序 ID**。 应用程序清单的应用程序元素中输入的 ID 属性的值。
    -   **通知处理程序**。 有关通知处理程序的信息，请参阅[元数据包架构引用 Windows 8 设备](https://go.microsoft.com/fwlink/p/?LinkId=226753)。

**包名称**，**发布者**，并**应用程序 ID**必须匹配在应用包.appxmanifest 中的信息。

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

## <a name="span-idtoseethepackagenameandpublisherspanspan-idtoseethepackagenameandpublisherspanspan-idtoseethepackagenameandpublisherspanto-see-the-package-name-and-publisher"></a><span id="To_see_the_Package_name_and_Publisher_"></span><span id="to_see_the_package_name_and_publisher_"></span><span id="TO_SEE_THE_PACKAGE_NAME_AND_PUBLISHER_"></span>若要查看的包名称和发布服务器


1.  在 Visual Studio 中打开应用解决方案。
2.  单击解决方案资源管理器中的应用程序清单。
3.  双击“Package.appxmanifest”。
4.  上**打包**选项卡上，查看**包名称**并**发布服务器**字段。

## <a name="span-idtoseetheappidspanspan-idtoseetheappidspanspan-idtoseetheappidspanto-see-the-app-id"></a><span id="To_see_the_App_ID_"></span><span id="to_see_the_app_id_"></span><span id="TO_SEE_THE_APP_ID_"></span>若要查看应用程序 ID


1.  在 Visual Studio 中打开应用解决方案。
2.  单击解决方案资源管理器中的应用程序清单。
3.  右键单击 Package.appxmanifest。
4.  选择**查看代码**。

## <a name="span-idprivilegedapplicationsspanspan-idprivilegedapplicationsspanspan-idprivilegedapplicationsspanprivileged-applications"></a><span id="Privileged_applications"></span><span id="privileged_applications"></span><span id="PRIVILEGED_APPLICATIONS"></span>权限的应用程序


能够访问特权的设备接口的 Microsoft Store 设备应用，该应用程序必须指定下**权限的应用程序**。

若要指定权限的应用程序，填写以下字段下**权限的应用程序**:

**注意**  
有关特权的设备接口属性项的详细信息，请参阅[DEVPKEY\_DeviceInterface\_Restricted](https://go.microsoft.com/fwlink/p/?linkid=256362)。



-   **包名称**。 应用程序清单的包元素中的标识元素中输入名称属性的值。
-   **发布者**。 应用程序清单的包元素中的标识元素中输入将 Publisher 属性的值。
-   如果权限的应用程序访问自定义驱动程序，请选择**AccessCustomDriver**。

下面是一个应用程序清单，其中显示了设备元数据创建向导中输入的标识名称、 发布者和应用程序 Id 字段的示例：

```XML
<?xml version="1.0" encoding="utf-8"?>
<Package xmlns="http://schemas.microsoft.com/appx/2010/manifest">
  <Identity Name="64022FABRIKAM.FabrikamDeviceApp" Publisher="CN=05558413-FFF6-4AA5-8176-AD43036533FA" Version="1.0.0.0" />
  <Properties>
    <DisplayName>Fabrikam Device App</DisplayName>
    <PublisherDisplayName>Fabrikam</PublisherDisplayName>
    <Logo>Assets\storeLogo-sdk.png</Logo>
  </Properties>
  <Prerequisites>
    <OSMinVersion>6.2</OSMinVersion>
    <OSMaxVersionTested>6.2</OSMaxVersionTested>
  </Prerequisites>
  <Resources>
    <Resource Language="x-generate" />
  </Resources>
  <Applications>
    <Application Id="DeviceAppForPrinters" Executable="$targetnametoken$.exe" 
        EntryPoint="DeviceAppForPrinters.App">
      <VisualElements DisplayName="Fabrikam Device App" Logo="Assets\squareTile-sdk.png" 
         SmallLogo="Assets\smallTile-sdk.png" Description="DeviceAppForPrinters" ForegroundText="light" BackgroundColor="#00b2f0" ToastCapable="true">
        <DefaultTile ShowName="allLogos" ShortName="App4PrinterCS" WideLogo="Assets\tile-sdk.png" />
        <SplashScreen Image="Assets\splash-sdk.png" BackgroundColor="#00b2f0" />
      </VisualElements>
      <Extensions>
          <Extension Category="windows.backgroundTasks" 
             EntryPoint="Fabrikam.Printing.PrintApp.PrintNotificationHandler">
               <BackgroundTasks>
                 <Task Type="systemEvent" />
               </BackgroundTasks>
          </Extension>
          <Extension Category="windows.printTaskSettings" 
             Executable="$targetnametoken$.exe" EntryPoint="DeviceAppForPrinters.App" />
      </Extensions>
    </Application>
  </Applications>
</Package>
```

以下是对应于应用程序清单字段中的设备元数据创建向导生成的 XML 元素的示例：

```XML
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<SoftwareInfo xmlns="http://schemas.microsoft.com/windows/2010/08/DeviceMetadata/SoftwareInfo">

  <DeviceCompanionApplications>
       <Package>
         <Identity Name="64022FABRIKAM.FabrikamDeviceApp" 
          Publisher="CN=05558413-FFF6-4AA5-8176-AD43036533FA" />
         <Applications>
          <Application Id="DeviceAppForPrinters">
           <DeviceNotificationHandlers>
                   <DeviceNotificationHandler
                      EventID="PrintNotificationHandler"
            EventAsset="Fabrikam.Printing.PrintApp.PrintNotificationHandler" />
                </DeviceNotificationHandlers>
         </Application>
          </Applications>
       </Package>
  </DeviceCompanionApplications>

  <PrivilegedApplications>
    <Package>
         <Identity Name="64022FABRIKAM.FabrikamDeviceApp" 
              Publisher="CN=05558413-FFF6-4AA5-8176-AD43036533FA"
              AccessCustomDriver="false" />  
    </Package>
  </PrivilegedApplications>
</SoftwareInfo>
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[设备元数据架构参考](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/dn465877(v=vs.85))










