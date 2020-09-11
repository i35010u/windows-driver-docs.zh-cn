---
description: 数字 Rights Management (DRM) 系统通常利用设备序列号来确保合法客户有权访问数字化的知识产权。
title: Usbccgp.sys 中的内容安全功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4607c08e02df501a40c20848dba5617b3a1192d5
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010345"
---
# <a name="content-security-features-in-usbccgpsys"></a>Usbccgp.sys 中的内容安全功能


数字 Rights Management (DRM) 系统通常利用设备序列号来确保合法客户有权访问数字化的知识产权。 如果 USB 设备有 CSM 1 的内容安全接口，客户端驱动程序可以通过向一般父驱动程序发送 [**IOCTL \_ 存储 \_ GET \_ MEDIA \_ 序列 \_ 号**](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_get_media_serial_number) 请求来查询其序列号。

## <a name="related-topics"></a>相关主题
[USB 常规父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)  
[Microsoft 提供的 USB 驱动程序](system-supplied-usb-drivers.md)