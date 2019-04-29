---
title: 处理大量的 SSID
description: 处理大量的 SSID
ms.assetid: 52bcfbd4-98f6-43e3-b697-c632f6660717
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e69275cd0077265dacde979e24e4ddb50b4298a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380159"
---
# <a name="handling-large-numbers-of-ssids"></a>处理大量的 SSID


本主题介绍如何处理大量的 Ssid 的要求。

Windows 8.1 和 Windows 10 通过增加可以在单个 WLAN 配置文件中配置的 Ssid 量显著提高对大量的 Ssid 的支持。 WLAN 配置文件现在可包含最多 10,000 个 Ssid。 此外，WLAN 配置文件支持 SSID 前缀。

本主题中包括以下各节：

-   [每个配置文件的多个 Ssid](#multssidpro)

-   [辅助 Ssid](#secssd)

-   [前缀](#prefixes)

-   [示例配置文件](#example)

## <a name="span-idmultssidprospanspan-idmultssidprospanmultiple-ssids-per-profile"></a><span id="multssidpro"></span><span id="MULTSSIDPRO"></span>每个配置文件的多个 Ssid


如果在预配 Windows 8、 Windows 8.1 或 Windows 10，若要连接到多个 Ssid，我们建议你提供每个配置文件的多个 Ssid。 这极大地减少了预配的文件的大小并提高计算机的响应能力。

如果你想要使用 Api 来标记应不再使用的网络，请注意这些操作适用于所有涵盖的相同的配置文件的 Ssid。 因此，它是最佳做法进行分组的单个配置文件中的相关的 Ssid。

您可以最多十个可以分别有 25 主 Ssid 在 Windows 8 和最多 10,000 Ssid Windows 8.1 中的配置文件。 在 Windows 8.1 中有两个独立 XML 的命名空间的 Ssid。 V1 命名空间支持最多 25 个 Ssid，如 Windows 8 中所示。 V2 命名空间支持最多 10,000 个 Ssid。 配置文件必须具有至少一个 SSID v1 命名空间中，并在总计中可以有最多 10,000 个 Ssid。

## <a name="span-idsecssdspanspan-idsecssdspansecondary-ssids"></a><span id="secssd"></span><span id="SECSSD"></span>辅助 Ssid


Windows 8 引入了辅助 Ssid WLAN 配置文件在 HotspotAuth 节来扩展包含在一个配置文件的 Ssid 量的概念。 在 Windows 8.1 和 Windows 10 中仍支持这样做，但我们建议改为使用 WLAN 配置文件的 SSID 节，以支持自动连接方案。

若要在 Windows 8 中配置每个配置文件的 25 个以上 Ssid，可以 HotspotAuth 部分 SSIDConfig 便笺中指定每个配置文件的辅助 Ssid。 这不会创建其他配置文件，对于这些网络，但将该 SSID 以及配置文件中的热点设置相关联。

如果用户手动在将来连接，并创建新的配置文件，此配置文件中的热点设置自动与相关联的用户创建配置文件。 由于辅助 Ssid 执行自动连接用户手动连接到它们一次，除非这些应是大多数用户不会遇到的不太常见网络。

您可以最多 250 辅助 Ssid，每个配置文件。

## <a name="span-idprefixesspanspan-idprefixesspanprefixes"></a><span id="prefixes"></span><span id="PREFIXES"></span>前缀


若要将与 Ssid 一特别大型的或动态组相关联，SSID 列表可以包含除了静态 Ssid 的前缀。 这样即可将你的移动宽带应用与一系列具有四个或多个八位字节共同的 SSID 开头的 Ssid 相关联。

在 Windows 8 中的第二 SSID 列表支持 SSID 前缀。 在 Windows 8.1 和 Windows 10 中，使用 v2 命名空间的 WLAN 配置文件的 SSIDConfig 部分支持 SSID 前缀。

## <a name="span-idexamplespanspan-idexamplespanexample-profile"></a><span id="example"></span><span id="EXAMPLE"></span>示例配置文件


本部分介绍包含在 v1 和 v2 命名空间和 SSID 前缀 SSID 的示例配置文件。

``` syntax
<WLANProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WLAN/v1"
             xmlns:v2="http://www.microsoft.com/networking/CarrierControl/WLAN/v2">
  <name>SampleProfile</name>
  <SSIDConfig>
    <SSID>
        <name>MySSID1</name>
    </SSID>
    <v2:SSID>
        <v2:name>MySSID2</v2:name>
    </v2:SSID>
    <v2:SSIDPrefix>
        <v2:name>MySSIDPrefix</v2:name>
    </v2:SSIDPrefix>
  </SSIDConfig>
  <MSM>
    <security>
        <authEncryption>
            <authentication>open</authentication>
            <encryption>none</encryption>
            <useOneX>false</useOneX>
        </authEncryption>
    </security>
  </MSM>
</WLANProfile>
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[WISPr 身份验证](wispr-authentication.md)

 

 






