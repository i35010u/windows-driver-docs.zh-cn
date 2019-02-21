---
title: 集 SMS 声明
description: 集 SMS 声明
ms.assetid: fad7fb60-eb08-43e9-bc58-afb8d6b5633c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14710d0bd2e4c8f5a769a83c57607d0873c005c4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544853"
---
# <a name="set-sms-declarations"></a>集 SMS 声明


## <a name="span-idsmsdevicecapabilitydeclarationinpackagemanifestspanspan-idsmsdevicecapabilitydeclarationinpackagemanifestspanspan-idsmsdevicecapabilitydeclarationinpackagemanifestspansms-device-capability-declaration-in-package-manifest"></a><span id="SMS_device_capability_declaration_in_package_manifest"></span><span id="sms_device_capability_declaration_in_package_manifest"></span><span id="SMS_DEVICE_CAPABILITY_DECLARATION_IN_PACKAGE_MANIFEST"></span>包清单中的短信设备功能声明


使用 SMS 的 UWP 应用必须声明其在 Visual Studio 中的包清单中的短信功能。

示例**package.appxmanifest**:

``` syntax
  <Capabilities>
    <DeviceCapability Name="sms" />
  </Capabilities>
```

有关详细信息，请参阅[应用功能声明 （UWP 应用）](https://go.microsoft.com/fwlink/p/?linkid=317125)。

## <a name="span-idsmsappdeclarationindevicemetadataspanspan-idsmsappdeclarationindevicemetadataspanspan-idsmsappdeclarationindevicemetadataspansms-app-declaration-in-device-metadata"></a><span id="SMS_app_declaration_in_device_metadata"></span><span id="sms_app_declaration_in_device_metadata"></span><span id="SMS_APP_DECLARATION_IN_DEVICE_METADATA"></span>设备元数据中的短信应用程序声明


移动宽带设备可以确定哪些应用它信任发送和接收 SMS 消息。 若要执行此操作，它将添加它信任中的包名[服务元数据](service-metadata.md)，以下条目中所示：

**\\Package\\SoftwareInformation\\SoftwareInfo.xml**

``` syntax
<PrivilegedApplications>
  <Package>
    <Identity Name="Microsoft.SDKSamples.SMSSendReceive.JS" Version="1.0.0.0" Publisher="CN=Contoso Corporation, O=Contoso Corporation, L=Redmond, S=Washington, C=US" />
  </Package>
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[开发 SMS 应用程序](developing-sms-apps.md)

 

 






