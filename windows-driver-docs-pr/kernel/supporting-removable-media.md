---
title: 支持可移动媒体
description: 支持可移动媒体
keywords:
- 可移动媒体 WDK 内核
- 可移动媒体 WDK 内核，关于可移动媒体设备
- Irp WDK 内核，可移动介质
- 内核模式驱动程序 WDK，可移动介质
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9383af4a8f72800033a878be806173e48fcfb4aa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799457"
---
# <a name="supporting-removable-media"></a>支持可移动媒体





文件系统和可移动媒体设备驱动程序分担了在可移动媒体设备上打开文件时，确保装载了正确介质的责任，并且在访问媒体的操作过程中保留了正确的介质。 在文件系统和可移动媒体设备驱动程序之间进行分层的任何中间驱动程序也共享此责任。

因此，适用于可移动媒体设备的驱动程序应该能够执行下列一项或多项操作：

[响应检查-从文件系统验证请求](responding-to-check-verify-requests-from-the-file-system.md)

[向文件系统通知可能的媒体更改](notifying-the-file-system-of-possible-media-changes.md)

[检查设备对象中的标志](checking-flags-in-the-device-object.md)

[在中间驱动程序中设置 Irp](setting-up-irps-in-intermediate-drivers.md)

 

 




