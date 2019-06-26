---
Description: 数字版权管理 (DRM) 系统经常做出的设备序列号以确保合法客户有权使用数字化知识产权。
title: Usbccgp.sys 中的内容安全功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2784727d29e18fb93c15103a63f3a12097a93cd7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378352"
---
# <a name="content-security-features-in-usbccgpsys"></a>Usbccgp.sys 中的内容安全功能


数字版权管理 (DRM) 系统经常做出的设备序列号以确保合法客户有权使用数字化知识产权。 如果 USB 设备已 CSM 1 内容安全接口，客户端驱动程序可以查询其序列号的发送[ **IOCTL\_存储\_获取\_媒体\_序列\_数量**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_get_media_serial_number)泛型父驱动程序的请求。

## <a name="related-topics"></a>相关主题
[USB 泛型父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)  
[Microsoft 提供的 USB 驱动程序](system-supplied-usb-drivers.md)  



