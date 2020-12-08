---
title: 处理大量的 SSID
description: 处理大量的 SSID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbd341c3672cbd0eb96a44bf02dccaba07522c9b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788513"
---
# <a name="handling-large-numbers-of-ssids"></a>处理大量的 SSID

本主题介绍处理大量 Ssid 的要求的方法。

Windows 8.1 和 Windows 10 通过增加可在单个 WLAN 配置文件中配置的 Ssid 数量，大大提高了对大量 Ssid 的支持。 现在，WLAN 配置文件最多可以包含 10000 Ssid。 此外，WLAN 配置文件支持 SSID 前缀。

本主题包括以下部分：

- [每个配置文件多个 Ssid](#multiple-ssids-per-profile)

- [辅助 Ssid](#secondary-ssids)

- [前缀](#prefixes)

- [示例配置文件](#example-profile)

## <a name="multiple-ssids-per-profile"></a>每个配置文件多个 Ssid

如果你正在预配 Windows 8、Windows 8.1 或 Windows 10 以连接到多个 Ssid，则建议你为每个配置文件提供多个 Ssid。 这极大地减少了设置文件的大小，并提高了计算机的响应能力。

如果你打算使用 Api 来标记不应再使用的网络，请注意，这些操作适用于同一配置文件涵盖的所有 Ssid。 因此，最佳做法是将相关 Ssid 分组到单个配置文件中。

在 Windows 8.1 中，最多可以有10个配置文件，每个配置文件最多有25个主要 10000 Ssid。 在 Windows 8.1 中，Ssid 有两个单独的 XML 命名空间。 V1 命名空间最多支持25个 Ssid，就像在 Windows 8 中一样。 V2 命名空间最多支持 10000 Ssid。 配置文件在 v1 命名空间中必须至少有一个 SSID，并且最多可以有 10000 Ssid。

## <a name="secondary-ssids"></a>辅助 Ssid

Windows 8 在 WLAN 配置文件的 HotspotAuth 部分中引入了辅助 Ssid 的概念，以扩展配置文件所涵盖的 Ssid 量。 Windows 8.1 和 Windows 10 中仍支持此项，但建议改为使用 WLAN 配置文件的 SSID 部分来支持自动连接方案。

若要在 Windows 8 中配置每个配置文件25个以上的 Ssid，可以在 HotspotAuth 节的 SSIDConfig 说明中为每个配置文件指定辅助 Ssid。 这不会为这些网络创建其他配置文件，但会将配置文件中的热点设置与该 SSID 关联起来。

如果用户以后手动连接并创建新的配置文件，则此配置文件中的热点设置将自动与用户创建的配置文件关联。 由于辅助 Ssid 不会自动连接，除非用户手动连接到它们一次，因此，大多数用户不会遇到这些不太常见的网络。

每个配置文件最多可以有250个辅助 Ssid。

## <a name="prefixes"></a>前缀

若要与特别大的或动态的 Ssid 集相关联，SSID 列表除了包含静态 Ssid 外，还可以包含前缀。 这样，你就可以将移动宽带应用与一组广泛的 Ssid 关联，这些 Ssid 在 SSID 的开头有一个通用的四个或更多个八进制。

在 Windows 8 中，仅在辅助 SSID 列表中支持 SSID 前缀。 在 Windows 8.1 和 Windows 10 中，使用 v2 命名空间的 WLAN 配置文件的 SSIDConfig 部分支持 SSID 前缀。

## <a name="example-profile"></a>示例配置文件

本部分显示了一个示例配置文件，其中包含 v1 和 v2 命名空间中的一个 SSID 以及一个 SSID 前缀。

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

## <a name="related-topics"></a>相关主题

[WISPr 身份验证](wispr-authentication.md)
