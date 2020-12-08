---
title: 在设备元数据创作向导中指定应用程序
description: 在设备元数据创作向导中指定应用程序
keywords:
- 在设备元数据创作向导中指定应用程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8551267f1b5b94a8c8ed33e9d86db4e43c6325c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816929"
---
# <a name="specify-applications-in-the-device-metadata-authoring-wizard"></a>在设备元数据创作向导中指定应用程序

你可以为设备指定不同的应用程序，包括 Microsoft Store 设备应用和特权应用程序。

当用户首次连接设备时，将下载并安装 UWP 设备应用。 特权应用程序具有设备的特殊访问权限。 只能指定其中的一个。

## <a name="to-specify-the-microsoft-store-device-app"></a>指定 Microsoft Store 设备应用

1. 单击“应用程序”选项卡。
2. 填写以下字段：
   1. **包名称**。 在应用程序清单的 Package 元素中的 Identity 元素中输入 Name 属性的值。 在将应用程序提交到 Microsoft Store 后，应获取包名称，因为 Microsoft Store 提交过程会更改包名称。 若要详细了解如何将应用与 Microsoft Store 相关联，并将更新的值复制到应用程序清单中，请参阅 [生成 UWP 设备应用](../devapps/the-workflow.md) 。
   2. **发布者**。 在应用程序清单的 Package 元素中的 Identity 元素中输入 "发布服务器" 属性的值。 发布者名称应与用于对包进行签名的开发人员证书和元数据的名称相同。
   3. **应用 ID**。 在应用程序清单的应用程序元素中输入 ID 属性的值。
   4. **通知处理程序**。 有关通知处理程序的信息，请参阅 [设备元数据架构参考](/previous-versions/windows/hardware/metadata/ff541452(v=vs.85))。

**包名称**、**发布者** 和 **应用 ID** 必须与应用包 appxmanifest.xml 中的信息匹配。

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
4. 在 " **打包** " 选项卡上，查看 " **包名称** " 和 " **发布者** " 字段。

## <a name="to-see-the-app-id"></a>查看应用 ID

1. 在 Visual Studio 中打开应用程序解决方案。
2. 单击解决方案资源管理器中的应用程序清单。
3. 右键单击 appxmanifest.xml。
4. 选择 " **查看代码**"。

## <a name="privileged-applications"></a>特权应用程序

要使 Microsoft Store 设备应用能够访问特权设备接口，必须在 **特权应用程序** 下指定应用。

若要指定特权应用程序，请在 **特权应用程序** 下填写以下字段：

>[!NOTE]
>有关特权设备接口属性键的详细信息，请参阅 [DEVPKEY \_ DeviceInterface \_ 限制](../install/devpkey-deviceinterface-restricted.md)。

- **包名称**。 在应用程序清单的 Package 元素中的 Identity 元素中输入 Name 属性的值。
- **发布者**。 在应用程序清单的 Package 元素中的 Identity 元素中输入 "发布服务器" 属性的值。
- 如果特权应用程序访问自定义驱动程序，请选择 " **AccessCustomDriver**"。

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

## <a name="related-topics"></a>相关主题

[设备元数据架构引用](/previous-versions/windows/hardware/metadata/dn465877(v=vs.85))
