---
title: 设置短信声明
description: 设置短信声明
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1eebd727c612c70975f9301489b3fd64d683f25
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803533"
---
# <a name="set-sms-declarations"></a>设置短信声明


## <a name="span-idsms_device_capability_declaration_in_package_manifestspanspan-idsms_device_capability_declaration_in_package_manifestspanspan-idsms_device_capability_declaration_in_package_manifestspansms-device-capability-declaration-in-package-manifest"></a><span id="SMS_device_capability_declaration_in_package_manifest"></span><span id="sms_device_capability_declaration_in_package_manifest"></span><span id="SMS_DEVICE_CAPABILITY_DECLARATION_IN_PACKAGE_MANIFEST"></span>包清单中的 SMS 设备功能声明


使用 SMS 的 UWP 应用必须在其在 Visual Studio 中的包清单中声明 SMS 功能。

示例 **appxmanifest.xml**：

``` syntax
  <Capabilities>
    <DeviceCapability Name="sms" />
  </Capabilities>
```

有关详细信息，请参阅 [ (UWP apps) 的应用功能声明 ](/previous-versions/windows/apps/hh464936(v=win.10))。

## <a name="span-idsms_app_declaration_in_device_metadataspanspan-idsms_app_declaration_in_device_metadataspanspan-idsms_app_declaration_in_device_metadataspansms-app-declaration-in-device-metadata"></a><span id="SMS_app_declaration_in_device_metadata"></span><span id="sms_app_declaration_in_device_metadata"></span><span id="SMS_APP_DECLARATION_IN_DEVICE_METADATA"></span>设备元数据中的 SMS 应用声明


移动宽带设备可以确定它信任哪些应用来发送和接收短信。 为此，它会将它信任的包名称添加到 [服务元数据](service-metadata.md)中，如以下条目所示：

**\\包 \\ SoftwareInformation \\SoftwareInfo.xml**

``` syntax
<PrivilegedApplications>
  <Package>
    <Identity Name="Microsoft.SDKSamples.SMSSendReceive.JS" Version="1.0.0.0" Publisher="CN=Contoso Corporation, O=Contoso Corporation, L=Redmond, S=Washington, C=US" />
  </Package>
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[开发短信应用](developing-sms-apps.md)

 

