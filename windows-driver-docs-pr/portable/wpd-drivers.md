---
description: WPD 驱动程序
title: WPD 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 069c2a6d6271d76b9fc96c1f3016263173a2cac4
ms.sourcegitcommit: ec7bebe3f94536455e62b372c2a28fe69d1717f7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2020
ms.locfileid: "93349759"
---
# <a name="wpd-drivers"></a>WPD 驱动程序

Microsoft Windows 便携设备 (WPD) 使计算机能够与附加的媒体和存储设备进行通信。 此系统通过提供一种灵活、可靠的方式来使计算机与音乐播放器、存储设备、移动电话以及许多其他类型的连接设备通信，同时取代 Windows Media 设备管理器 (WMDM) 和 Windows 图像获取 (WIA) 。

Microsoft 为标准协议和设备提供了几个驱动程序，包括图片传输协议 (PTP) 、媒体传输协议 (MTP) 设备和大容量存储类 (MSC) 设备。 如果设备支持独特的协议，则可能需要开发自己的驱动程序。 使用 User-Mode Driver Framework (UMDF) 来编写此驱动程序。 有关此框架的详细信息，请参阅 [UMDF](../wdf/getting-started-with-umdf-version-2.md)入门。

有关为 Windows 便携设备编写的应用程序的详细信息，请参阅 [WPD SDK 文档](/windows/win32/windows-portable-devices)。

有关 WPD 驱动程序开发和 WPD 应用程序开发的详细信息，请参阅 [WPD 博客 (Archive) ](/archive/blogs/wpdblog/)，它对于 Windows 10 是准确的。