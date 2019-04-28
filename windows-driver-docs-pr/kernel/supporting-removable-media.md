---
title: 支持可移动媒体
description: 支持可移动媒体
ms.assetid: f70c404c-8a38-4f53-8681-6efb52b30656
keywords:
- 可移动媒体 WDK 内核
- 可移动媒体 WDK 内核，有关可移动媒体设备
- Irp WDK 内核，可移动媒体
- 内核模式驱动程序 WDK，可移动媒体
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e45fd807106ac6f798386430d834798e5efccae7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330549"
---
# <a name="supporting-removable-media"></a>支持可移动媒体





文件系统和可移动介质设备驱动程序共享负责确保正确的媒体装载时在可移动介质设备上打开文件和正确的介质保持装载访问媒体的操作过程。 分层文件系统和可移动介质设备驱动程序之间的任何中间驱动程序还会与此职责。

因此使用可移动介质设备的驱动程序应该能够执行一个或多项操作：

[若要检查验证从文件系统的请求的响应](responding-to-check-verify-requests-from-the-file-system.md)

[通知可能的介质更改的文件系统](notifying-the-file-system-of-possible-media-changes.md)

[检查设备对象中的标志](checking-flags-in-the-device-object.md)

[在中间的驱动程序中设置 Irp](setting-up-irps-in-intermediate-drivers.md)

 

 




