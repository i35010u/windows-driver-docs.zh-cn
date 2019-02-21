---
title: WLAN Direct
description: WLAN Direct
ms.assetid: 52D09B1D-5832-48C9-B200-46B8DDC14BE5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00a5c1f5a1bca8bde86b33a8b1089d9d34afe21f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533909"
---
# <a name="wi-fi-direct"></a>WLAN Direct


在 Windows 10 和相关联的 Wi-Fi Direct Api WDI 驱动程序替换的 NDIS 驱动程序和 Windows 8.1 中的关联的 SoftAP Api。 可以继续使用 SoftAP API 以使用 Windows 10 中的 NDIS 驱动程序，而 API 已弃用在 Windows 8.1 中启动。 其中包括 IDot11AdHocManager 和相关的接口。

Windows 10 中的全部功能，您应改用 Wi-Fi Direct WinRT Api 通过 WDI 驱动程序。

但是，可以使用 Wi-Fi Direct WinRT Api 的一些经典 Windows 应用程序中。 例如可以在经典 Windows 应用程序中使用 Wi-Fi Direct WinRT Api 代替 WFDOpenHandle 和相关的 Api。 WiFiDirectLegacySettings 类允许不支持 Wi-Fi Direct 连接到设备支持它，并使用 Wi-Fi Direct 设备提供的服务的设备。

WiFiDirectLegacySettings 允许您指定的 SSID 和密码。 有关如何在经典 Windows 应用程序中使用 WiFiDirectLegacySettings 的示例，请参阅[WiFiDirectLegacyAPDemo\_v1.0.zip](https://go.microsoft.com/fwlink/?LinkId=617905)上 Microsoft 下载中心进行下载。

从 Windows 10，版本 1607年开始支持移动热点。 移动热点是移动宽带 tethering 功能的增强的版本。 请注意，不能在同一时间使用的移动热点和 Wi-Fi Direct 旧组所有者功能。 此外，移动热点将优先于所有 Wi-Fi Direct 方案。

桌面应用程序的开发人员可以使用此示例，了解如何将为不推荐使用的 WlanHostedNetwork\* API 与新 WinRT API 而无需修改应用程序变得通用 Windows 应用程序。 这些 API 的允许启动 Wi-Fi Direct 组所有者 （继续），充当接入点 (AP) 作为应用程序。 这样，不支持 Wi-Fi Direct 连接到运行此应用程序的 Windows 设备，并通过 TCP/UDP 通信的设备。 该 API 允许开发人员还可以选择指定 SSID 和通行短语，或使用随机生成的。

**请注意**  在经典 Windows 应用，你无需设置的 WinRT 设备功能，因为没有 Package.appxmanifest 文件。

 

## <a name="resources"></a>资源


### <a name="recorded-sessions"></a>录制的会话

-   [Wi-Fi Direct 和 Wi-Fi Direct 服务 API （包括示例代码）](https://go.microsoft.com/fwlink/?LinkId=617632)

### <a name="articles"></a>文章

-   [Wi-Fi Direct 服务 API](https://go.microsoft.com/fwlink/?LinkId=617633)
-   [什么是驱动程序开发中的新增功能？]( https://go.microsoft.com/fwlink/?LinkId=617634)
-   [使用 WinRT API 在 Win32 应用程序]( https://go.microsoft.com/fwlink/?LinkId=617635)

### <a name="wi-fi-direct-in-windows-8"></a>Wi-Fi Direct Windows 8 中

-   [在 Windows 8 中了解 Wi-Fi Direct](https://go.microsoft.com/fwlink/?LinkId=617636)
-   [向专家咨询面板：连接的应用](https://go.microsoft.com/fwlink/?LinkId=617637)
-   [使用 Wi-Fi Direct 的构建 Windows 应用 (Windows 8.1)](https://go.microsoft.com/fwlink/?LinkId=617638)

 

 





