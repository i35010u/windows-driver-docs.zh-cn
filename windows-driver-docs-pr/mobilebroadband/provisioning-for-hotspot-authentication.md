---
title: 针对热点身份验证的预配
description: 针对热点身份验证的预配
ms.assetid: bfb4e1ec-9887-4b25-bfcc-be642b1a0101
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba902f2f0edcabf737275fba02fdbc1889a87c8e
ms.sourcegitcommit: 67efcd26f7be8f50c92b141ccd14c9c68f4412d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88902568"
---
# <a name="provisioning-for-hotspot-authentication"></a>针对热点身份验证的预配

要使应用参与热点身份验证过程，必须先为 Wi-fi 热点创建一个或多个配置文件。 这是通过使用 [元数据配置移动宽带体验](using-metadata-to-configure-mobile-broadband-experiences.md)中讨论的预配代理界面来实现的。 热点必须使用开放式身份验证，并且必须包含 **HotspotProfile** 元素。 以下预配文件示例显示了如何将 SSID 与应用关联：

``` syntax
<WLANProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WLAN/v1">
  <name>Contoso Wi-Fi</name>
  <SSIDConfig>
    <SSID>
      <name>Contoso Wi-Fi___33</name>
    </SSID>
  </SSIDConfig>
  <MSM>
    <security>
      <authEncryption>
        <authentication>open</authentication>
        <encryption>none</encryption>
        <useOneX>false</useOneX>
      </authEncryption>
      <HotspotProfile xmlns="http://www.microsoft.com/networking/WLAN/HotspotProfile/v1">
        <ExtAuth>
          <ExtensionId>YourAppIdGoesHere</ExtensionId>
        </ExtAuth>
        <TrustedDomains>
          <TrustedDomain>www.mycaptiveportal.com</TrustedDomain>
        </TrustedDomains>
        <UserAgent>contoso</UserAgent>
      </HotspotProfile>
    </security>
  </MSM>
</WLANProfile>
```

ExtensionId 字段包含生成热点凭据的应用的包系列名称。 包系列名称由 Visual Studio 自动生成。 若要查找应用程序的包系列名称，请打开 Visual Studio 解决方案中的 **appxmanifest.xml** 文件，并中转到 "打包" 窗口。

处理预配文件后，具有包系列名称 "YourAppIdGoesHere" 的应用必须注册热点身份验证事件。 需要首先处理预配文件，以便向指定的应用授予对此事件的访问权限。 应用可以为此事件注册单个处理程序。 只要至少有一个引用相应应用的配置文件，事件注册就会保持有效。

## <a name="sign-the-provisioning-file"></a>签署预配文件

由于预配修改了用户退出或卸载应用后保留的系统设置，因此需要对大多数 Api 进行更严格的验证。 此验证由操作员特定硬件的组合提供 (SIM) 、加密签名和用户确认。 下表列出了验证要求：

|存在 SIM|设置源|签名要求|用户确认要求|
|----|----|----|----|
|是，MB 提供程序|移动宽带应用|无|无|
|是，MB 提供程序|Operator 网站|证书必须：</br>-链式返回到受信任的根 CA</br>-与 APN 数据库中的移动宽带硬件或体验元数据关联|无|
|否，Wi-fi 提供程序|移动宽带应用或网站|证书必须：</br>-链式返回到受信任的根 CA</br>-已标记为进行扩展验证|首次使用证书时，系统会提示用户确认;无。|

## <a name="related-topics"></a>相关主题

[WISPr 身份验证](wispr-authentication.md)
