---
title: 在设备元数据创作向导中指定应用程序
description: 在设备元数据创作向导中指定应用程序
ms.assetid: B3ECEBF3-FBC6-45E7-9FF5-439F1CDF351F
keywords:
- 在设备元数据创作向导中指定应用程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3498cc6c1979dd7edfd47e21f1a1c389bae26aa9
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769509"
---
# <a name="specify-applications-in-the-device-metadata-authoring-wizard"></a>在设备元数据创作向导中指定应用程序


你可以为设备指定不同的应用程序，包括 Microsoft Store 设备应用和特权应用程序。

当用户首次连接设备时，将下载并安装 UWP 设备应用。 特权应用程序具有设备的特殊访问权限。 只能指定其中的一个。

## <a name="span-idto_specify_the_windows_store_device_appspanspan-idto_specify_the_windows_store_device_appspanspan-idto_specify_the_windows_store_device_appspanto-specify-the-microsoft-store-device-app"></a><span id="To_specify_the_Windows_Store_device_app"></span><span id="to_specify_the_windows_store_device_app"></span><span id="TO_SPECIFY_THE_WINDOWS_STORE_DEVICE_APP"></span>指定 Microsoft Store 设备应用


1.  单击“应用程序”**** 选项卡。
2.  填写以下字段：
    -   **包名称**。 在应用程序清单的 Package 元素中的 Identity 元素中输入 Name 属性的值。 在将应用程序提交到 Microsoft Store 后，应获取包名称，因为 Microsoft Store 提交过程会更改包名称。 若要详细了解如何将应用与 Microsoft Store 相关联，并将更新的值复制到应用程序清单中，请参阅[生成 UWP 设备应用](https://docs.microsoft.com/windows-hardware/drivers/devapps/the-workflow)。
    -   **发布者**。 在应用程序清单的 Package 元素中的 Identity 元素中输入 "发布服务器" 属性的值。 发布者名称应与用于对包进行签名的开发人员证书和元数据的名称相同。
    -   **应用 ID**。 在应用程序清单的应用程序元素中输入 ID 属性的值。
    -   **通知处理程序**。 有关通知处理程序的信息，请参阅[设备元数据架构参考](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541452(v=vs.85))。

**包名称**、**发布者**和**应用 ID**必须与应用包 appxmanifest.xml 中的信息匹配。

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

## <a name="span-idto_see_the_package_name_and_publisher_spanspan-idto_see_the_package_name_and_publisher_spanspan-idto_see_the_package_name_and_publisher_spanto-see-the-package-name-and-publisher"></a><span id="To_see_the_Package_name_and_Publisher_"></span><span id="to_see_the_package_name_and_publisher_"></span><span id="TO_SEE_THE_PACKAGE_NAME_AND_PUBLISHER_"></span>查看包名称和发布服务器


1.  在 Visual Studio 中打开应用程序解决方案。
2.  单击解决方案资源管理器中的应用程序清单。
3.  双击“Package.appxmanifest”。
4.  在 "**打包**" 选项卡上，查看 "**包名称**" 和 "**发布者**" 字段。

## <a name="span-idto_see_the_app_id_spanspan-idto_see_the_app_id_spanspan-idto_see_the_app_id_spanto-see-the-app-id"></a><span id="To_see_the_App_ID_"></span><span id="to_see_the_app_id_"></span><span id="TO_SEE_THE_APP_ID_"></span>查看应用 ID


1.  在 Visual Studio 中打开应用程序解决方案。
2.  单击解决方案资源管理器中的应用程序清单。
3.  右键单击 appxmanifest.xml。
4.  选择 "**查看代码**"。

## <a name="span-idprivileged_applicationsspanspan-idprivileged_applicationsspanspan-idprivileged_applicationsspanprivileged-applications"></a><span id="Privileged_applications"></span><span id="privileged_applications"></span><span id="PRIVILEGED_APPLICATIONS"></span>特权应用程序


要使 Microsoft Store 设备应用能够访问特权设备接口，必须在**特权应用程序**下指定应用。

若要指定特权应用程序，请在**特权应用程序**下填写以下字段：

**注意**  
有关特权设备接口属性键的详细信息，请参阅[DEVPKEY \_ DeviceInterface \_ 限制](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-deviceinterface-restricted)。



-   **包名称**。 在应用程序清单的 Package 元素中的 Identity 元素中输入 Name 属性的值。
-   **发布者**。 在应用程序清单的 Package 元素中的 Identity 元素中输入 "发布服务器" 属性的值。
-   如果特权应用程序访问自定义驱动程序，请选择 " **AccessCustomDriver**"。

下面是应用程序清单的示例，其中显示了在设备元数据创作向导中输入的标识名称、发布者和应用程序 Id 字段：

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

下面是在设备元数据创作向导生成的 XML 中的元素的一个示例，它对应于应用程序清单字段：

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

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[设备元数据架构引用](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/dn465877(v=vs.85))










