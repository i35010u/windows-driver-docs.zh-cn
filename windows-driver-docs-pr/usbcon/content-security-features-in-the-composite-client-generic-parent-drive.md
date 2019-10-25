---
Description: 数字 Rights Management （DRM）系统通常利用设备序列号来确保合法客户有权访问数字化的知识产权。
title: Usbccgp.sys 中的内容安全功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59d7faabb4ab369405b1d67f80cf2223f0208086
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842399"
---
# <a name="content-security-features-in-usbccgpsys"></a>Usbccgp.sys 中的内容安全功能


数字 Rights Management （DRM）系统通常利用设备序列号来确保合法客户有权访问数字化的知识产权。 如果 USB 设备有 CSM 1 的内容安全接口，则客户端驱动程序可以通过发送 IOCTL\_存储来查询其序列号，\_获取对泛型父驱动程序[ **\_串行\_号请求\_媒体**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_get_media_serial_number)。

## <a name="related-topics"></a>相关主题
[USB 通用父驱动程序（Usbccgp）](usb-common-class-generic-parent-driver.md)  
[Microsoft 提供的 USB 驱动程序](system-supplied-usb-drivers.md)  



