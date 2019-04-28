---
Description: 固件是内部的一台设备，并独立于操作系统。 但是，固件下载会导致操作系统错误。
title: 配置 USB 设备的固件更新
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4c1d98ac24d0381046fbed203ab3550707ea4ff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352595"
---
# <a name="configuring-a-usb-device-for-firmware-update"></a>配置 USB 设备的固件更新


固件是内部的设备，独立于操作系统。 但是，固件下载会导致操作系统错误。

-   在 Windows XP 中，将你的设备连接到系统可能会导致多个插入和拔出声音，从而导致不佳的最终用户体验。

-   每次设备启动时，会下载固件，因为它可能无法正常后立即尚未插入在中，或在从 S3 和 S4 电源状态恢复操作系统。

-   在从 S3 或 S4 恢复你的设备可能会导致意外删除对话框弹出，因为大多数计算机截断到 S4 模式中的自供电设备的电源。

若要避免出现系统错误：

-   请确保该设备具有两个单独的供应商和设备 Id 集。

    两次通过系统枚举设备的固件更新。 系统检测到设备时，它加载初步的驱动程序通过使用供应商和设备 id。 此驱动程序便于固件下载。

    固件加载后，初步的驱动程序将导致系统要再次枚举设备的总线重置。 新的固件提供了一组不同的供应商和设备 id。 在第二个枚举期间系统使用一组新的 Id，并加载的主要设备驱动程序。

-   请确保供应商和设备 Id 是唯一的特定于您的产品。

    如果你的设备包括第三方的可编程 USB 芯片，芯片可能通过使用一组标准的 Id 来标识自身。 如果使用同一系统上的另一台设备使用同一芯片，则可能有一组相同的 Id，导致操作系统无法正常工作的两个设备之间的争用。

## <a name="related-topics"></a>相关主题
[针对 Windows 构建的 USB 设备](building-usb-devices-for-windows.md)  
