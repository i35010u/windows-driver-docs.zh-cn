---
title: 热点身份验证的预配
description: 热点身份验证的预配
ms.assetid: bfb4e1ec-9887-4b25-bfcc-be642b1a0101
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7c4492aa45e671f3ab9edc36c43169f2463bb01
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546652"
---
# <a name="provisioning-for-hotspot-authentication"></a>热点身份验证的预配


热点身份验证过程中参与的应用，它必须先创建一个或多个配置文件的 Wi-fi 热点。 这是通过使用中所述的预配代理接口[使用元数据来配置移动宽带体验](using-metadata-to-configure-mobile-broadband-experiences.md)。 作用点必须使用开放式身份验证，并且必须包括**HotspotProfile**元素。 以下预配文件示例演示如何将 SSID 与您的应用程序相关联：

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

扩展 Id 字段包含生成热点凭据的应用包系列名称。 Visual Studio 自动生成包系列名称。 若要查找你的应用程序的包系列名称，打开**package.appxmanifest** Visual Studio 解决方案文件，并转到打包窗口中。

处理预配文件后，必须注册有包系列名称"YourAppIdGoesHere"的应用的热点身份验证事件。 这是必需的预配文件首先处理以授予对此事件的指定的应用程序访问权限。 应用可以注册此事件的单个处理程序。 只要至少一个引用相应的应用程序的配置文件将保持有效事件注册。

## <a name="span-idsignspanspan-idsignspansign-the-provisioning-file"></a><span id="sign"></span><span id="SIGN"></span>预配文件进行签名


预配修改后用户已退出，或即使卸载应用程序保留的系统设置，因为更严格的验证度量值都需要比大多数 Api。 此验证提供的特定于运算符的硬件 (SIM)、 加密签名和用户进行确认的组合。 下表列出了验证要求：

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>SIM 存在</th>
<th>设置源</th>
<th>签名要求</th>
<th>用户确认要求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是的 MB 提供程序</p></td>
<td><p>移动宽带应用</p></td>
<td><p>无</p></td>
<td><p>无</p></td>
</tr>
<tr class="even">
<td><p>是的 MB 提供程序</p></td>
<td><p>运算符 web 站点</p></td>
<td><p>证书必须：</p>
<ul>
<li><p>后向链接到受信任的根 CA</p></li>
<li><p>与 APN 数据库中的移动宽带硬件相关联或体验元数据</p></li>
</ul></td>
<td><p>无</p></td>
</tr>
<tr class="odd">
<td><p>否，Wi-fi 提供程序</p></td>
<td><p>移动宽带应用或网站</p></td>
<td><p>证书必须：</p>
<ul>
<li><p>后向链接到受信任的根 CA</p></li>
<li><p>标记为要扩展的验证</p></li>
</ul></td>
<td><p>系统会提示用户确认第一次使用该证书;此后 none。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[WISPr 身份验证](wispr-authentication.md)

 

 






