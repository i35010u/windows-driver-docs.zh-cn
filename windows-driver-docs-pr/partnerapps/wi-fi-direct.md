---
title: WLAN Direct
description: WLAN Direct
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdb737ca33ff96f40454e3ac4e4ada6b356a117c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806059"
---
# <a name="wi-fi-direct"></a>WLAN Direct

Windows 10 中的 WDI 驱动程序和关联的 Wi-Fi 直接 Api 在 Windows 8.1 中替换 NDIS 驱动程序和关联的 SoftAP Api。 尽管你可以继续使用 SoftAP API 在 Windows 10 中使用 NDIS 驱动程序，但从 Windows 8.1 开始，Api 已弃用。 这包括 IDot11AdHocManager 和相关接口。

若要在 Windows 10 中使用完整功能，应改用 WDI 驱动程序的 Wi-Fi 直接 WinRT Api。

但是，可以在经典 Windows 应用程序中使用某些 Wi-Fi 直接 WinRT Api。 例如，可以在经典 Windows 应用程序中使用 Wi-Fi Direct WinRT Api 来替代 WFDOpenHandle 和相关的 Api。 WiFiDirectLegacySettings 类允许不支持 Wi-Fi Direct 的设备连接到支持它的设备，并使用 Wi-Fi Direct 设备提供的服务。

WiFiDirectLegacySettings 允许指定 SSID 和密码。 有关如何在经典 Windows 应用程序中使用 WiFiDirectLegacySettings 的示例，请参阅 Microsoft 下载中心上的 [WiFiDirectLegacyAPDemo \_v1.0.zip](https://go.microsoft.com/fwlink/?LinkId=617905) 下载。

从 Windows 10 版本1607开始支持移动热点。 移动热点是移动宽带 tethering 功能的增强版本。 请注意，不能同时使用移动热点和旧 Wi-Fi 直接组所有者功能。 此外，移动热点优先于所有 Wi-Fi 直接方案。

桌面应用程序的开发人员可以使用此示例来了解如何将不推荐使用的 WlanHostedNetwork api 替换为 \* 新的 WINRT api，而无需修改应用程序即可成为通用 Windows 应用程序。 通过这些 API，应用程序可以启动一个 Wi-Fi 的直接组所有者， (作为接入点 (AP) 的) 。 这允许不支持 Wi-Fi 定向的设备连接到运行此应用程序的 Windows 设备，并通过 TCP/UDP 进行通信。 利用 API，开发人员可以根据需要指定 SSID 和密码，或使用随机生成的密码。

>纪录在经典 Windows 应用程序中，不需要设置 WinRT 设备功能，因为没有 appxmanifest.xml 文件。

## <a name="see-also"></a>请参阅

- [生成2015视频： Wi-Fi 直接和 Wi-Fi 直接服务 API (包括示例代码) ](https://channel9.msdn.com/Events/Build/2015/3-98)

- [Wi-fi Direct 服务 API](/uwp/api/windows.devices.wifidirect.services)

- [生成2011视频：了解 Windows 8 中的 Wi-Fi Direct](https://channel9.msdn.com/Events/Build/BUILD2011/HW-329T)

- [生成2013视频：生成使用 Wi-Fi 直接 (Windows 8.1 的 Windows 应用) ](https://channel9.msdn.com/Events/Build/2013/3-9030)
