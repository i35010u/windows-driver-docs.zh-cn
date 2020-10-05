---
title: WLAN Direct
description: WLAN Direct
ms.assetid: 52D09B1D-5832-48C9-B200-46B8DDC14BE5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3fdc4a4c9624f41edae2a37e94c8f908e03175e
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732501"
---
# <a name="wi-fi-direct"></a>WLAN Direct


Windows 10 中的 WDI 驱动程序和关联的 Wi-fi 直接 Api 会将 NDIS 驱动程序和关联的 SoftAP Api 替换 Windows 8.1 中。 尽管你可以继续使用 SoftAP API 在 Windows 10 中使用 NDIS 驱动程序，但从 Windows 8.1 开始，Api 已弃用。 这包括 IDot11AdHocManager 和相关接口。

对于 Windows 10 中的全部功能，应改为将 Wi-fi Direct WinRT Api 与 WDI 驱动程序一起使用。

但是，可以在经典 Windows 应用程序中使用某些 Wi-fi Direct WinRT Api。 例如，可以在经典 Windows 应用程序中使用 Wi-fi Direct WinRT Api 来替代 WFDOpenHandle 和相关的 Api。 WiFiDirectLegacySettings 类允许不支持 Wi-fi Direct 的设备连接到支持该设备的设备，并使用 Wi-fi Direct 设备提供的服务。

WiFiDirectLegacySettings 允许指定 SSID 和密码。 有关如何在经典 Windows 应用程序中使用 WiFiDirectLegacySettings 的示例，请参阅 Microsoft 下载中心上的 [WiFiDirectLegacyAPDemo \_v1.0.zip](https://go.microsoft.com/fwlink/?LinkId=617905) 下载。

从 Windows 10 版本1607开始支持移动热点。 移动热点是移动宽带 tethering 功能的增强版本。 请注意，不能同时使用移动热点和旧的 Wi-fi Direct 组所有者功能。 此外，移动热点优先于所有 Wi-fi Direct 方案。

桌面应用程序的开发人员可以使用此示例来了解如何将不推荐使用的 WlanHostedNetwork api 替换为 \* 新的 WINRT api，而无需修改应用程序即可成为通用 Windows 应用程序。 通过这些 API，应用程序可以启动 Wi-fi Direct 组所有者 (充当 AP)  (接入点) 。 这允许不支持 Wi-fi Direct 的设备连接到运行此应用程序的 Windows 设备，并通过 TCP/UDP 进行通信。 利用 API，开发人员可以根据需要指定 SSID 和密码，或使用随机生成的密码。

**注意**   在经典 Windows 应用程序中，不需要设置 WinRT 设备功能，因为没有 appxmanifest.xml 文件。

 

## <a name="resources"></a>资源


### <a name="recorded-sessions"></a>记录的会话

-   [Wi-fi Direct 和 Wi-fi Direct Services API (包括示例代码) ](https://go.microsoft.com/fwlink/?LinkId=617632)

### <a name="articles"></a>文章

-   [Wi-fi Direct 服务 API](/uwp/api/Windows.Devices.WiFiDirect.Services)
-   [驱动程序开发有哪些新功能？]( https://go.microsoft.com/fwlink/?LinkId=617634)
-   [在 Win32 应用中使用 WinRT API]( https://go.microsoft.com/fwlink/?LinkId=617635)

### <a name="wi-fi-direct-in-windows-8"></a>Windows 8 中的 wi-fi Direct

-   [了解 Windows 8 中的 Wi-fi Direct](https://go.microsoft.com/fwlink/?LinkId=617636)
-   [咨询专家面板：连接的应用](https://go.microsoft.com/fwlink/?LinkId=617637)
-   [构建使用 Wi-fi Direct (Windows 8.1 的 Windows 应用) ](https://go.microsoft.com/fwlink/?LinkId=617638)

 

