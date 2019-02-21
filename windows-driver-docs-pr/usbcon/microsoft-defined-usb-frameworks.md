---
Description: This topic describes the Microsoft-provided driver framework for USB devices that do not have their own USB device class specification.
title: Microsoft 定义的 USB 驱动程序框架
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 36da55865d5fd59933918286bd6500e4cf658bb0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540413"
---
# <a name="microsoft-defined-usb-driver-frameworks"></a>Microsoft 定义的 USB 驱动程序框架


本主题介绍适用于不具有其自己的 USB 设备类规范的 USB 设备由 Microsoft 提供的驱动程序框架。

Microsoft 提供的用于某些类型不具有其自己的 USB 设备类规范的 USB 设备的驱动程序框架。 想要开发这些类型的设备的供应商应开发为设备类型使用指定的框架的设备驱动程序。

目前 Microsoft 提供以下驱动程序框架，适用于以下的 USB 设备：

-   USB 生物识别设备

    Microsoft 通过提供 Windows 生物识别框架来支持 USB 生物识别设备 （指纹读取器）。 有关详细信息请参阅[生物识别框架概述](https://msdn.microsoft.com/library/windows/desktop/dd560897.aspx)。

## <a name="related-topics"></a>相关主题
[Microsoft 提供的 USB 驱动程序](system-supplied-usb-drivers.md)  



