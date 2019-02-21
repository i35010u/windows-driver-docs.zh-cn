---
title: 从 UMDF 调用 WinUSB
description: 从 UMDF 调用 WinUSB
ms.assetid: 33455d61-0eb3-47ef-998a-6e1b5d7db24e
keywords:
- WinUSB WDK UMDF
- WinUSB WDK UMDF，转义到 WinUSB
- 用户模式驱动程序 WDK UMDF，转义到 WinUSB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3d541be43dd9d00e12f688823962347f71baf7a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524339"
---
# <a name="calling-winusb-from-umdf"></a>从 UMDF 调用 WinUSB


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

UMDF 驱动程序可以调用[WinUSB 函数](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)直接如果驱动程序无法使用特定于 USB 的 UMDF 接口来执行特定操作。 若要调用 WinUSB 函数，该驱动程序必须首先获取 WinUSB 接口句柄通过调用[ **IWDFUsbTargetDevice::GetWinUsbHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff560369)或[ **IWDFUsbInterface::GetWinUsbHandle**](https://msdn.microsoft.com/library/windows/hardware/ff560337)。 WinUSB 接口句柄用于所选的配置中定义的第一个接口。

有关详细信息，请参阅[如何访问由使用 WinUSB 函数 USB 设备](https://msdn.microsoft.com/library/windows/hardware/ff540174)。

 

 





