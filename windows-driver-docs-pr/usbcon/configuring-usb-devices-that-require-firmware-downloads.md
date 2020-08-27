---
description: 固件是设备内部的，与操作系统无关。 但是，固件下载可能会导致操作系统错误。
title: 配置用于固件更新的 USB 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ed34f09980701590472607a622afa856dca629a
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969536"
---
# <a name="configuring-a-usb-device-for-firmware-update"></a>配置用于固件更新的 USB 设备


固件是设备内部的，与操作系统无关。 但是，固件下载可能会导致操作系统错误。

-   在 Windows XP 中，将设备连接到系统可能会导致多个插即用声音，导致最终用户体验不佳。

-   由于固件是在设备每次启动时下载的，因此它可能无法在接通电源后立即运行，或者在操作系统从 S3 或 S4 电源状态恢复之后运行。

-   在从 S3 或 S4 恢复的情况下，你的设备可能会导致 "意外删除" 对话框弹出，因为大多数计算机会在 S4 模式下切断自供电设备的电源。

避免系统错误：

-   请确保该设备具有两个不同的供应商和设备 Id 集。

    系统对支持固件更新的设备进行两次枚举。 当系统检测到设备时，它将使用供应商和设备 ID 加载初步驱动程序。 此驱动程序便于下载固件。

    加载固件后，初步驱动程序会重置总线，导致系统再次枚举设备。 新固件提供一组不同的供应商和设备 ID。 在第二个枚举过程中，系统使用新的 Id 集并加载主设备驱动程序。

-   请确保供应商和设备 Id 是唯一的且特定于你的产品。

    如果设备包含第三方的可编程 USB 芯片，则芯片可能使用一组标准的 Id 进行自我标识。 如果同一芯片与同一系统上的另一台设备一起使用，则这两个设备之间可能存在争用同一组 Id 的争用，导致操作系统出现故障。

## <a name="related-topics"></a>相关主题
[为 Windows 构建 USB 设备](building-usb-devices-for-windows.md)  
