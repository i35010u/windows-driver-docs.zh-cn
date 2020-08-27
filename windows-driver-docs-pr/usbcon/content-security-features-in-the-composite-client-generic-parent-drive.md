---
description: 数字 Rights Management (DRM) 系统通常利用设备序列号来确保合法客户有权访问数字化的知识产权。
title: Usbccgp.sys 中的内容安全功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e37c562ac5bd7debf4438b70a035e3e2bba5e9b7
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968516"
---
# <a name="content-security-features-in-usbccgpsys"></a>Usbccgp.sys 中的内容安全功能


数字 Rights Management (DRM) 系统通常利用设备序列号来确保合法客户有权访问数字化的知识产权。 如果 USB 设备有 CSM 1 的内容安全接口，客户端驱动程序可以通过向一般父驱动程序发送 [**IOCTL \_ 存储 \_ GET \_ MEDIA \_ 序列 \_ 号**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_get_media_serial_number) 请求来查询其序列号。

## <a name="related-topics"></a>相关主题
[USB 常规父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)  
[Microsoft 提供的 USB 驱动程序](system-supplied-usb-drivers.md)  



