---
title: 从 UMDF 调用 WinUSB
description: 从 UMDF 调用 WinUSB
ms.assetid: 33455d61-0eb3-47ef-998a-6e1b5d7db24e
keywords:
- WinUSB WDK UMDF
- WinUSB WDK UMDF，转义 WinUSB
- 用户模式驱动程序 WDK UMDF，转义给 WinUSB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73adde18d0a88a20a3a7a21d9818560d2e5cf38e
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185061"
---
# <a name="calling-winusb-from-umdf"></a>从 UMDF 调用 WinUSB


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

当驱动程序无法使用 USB 特定的 UMDF 接口执行特定操作时，UMDF 驱动程序可以直接调用 [WinUSB 函数](/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb) 。 若要调用 WinUSB 函数，驱动程序必须首先通过调用 [**IWDFUsbTargetDevice：： GetWinUsbHandle**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-getwinusbhandle) 或 [**IWDFUsbInterface：： GetWinUsbHandle**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getwinusbhandle)获取 WinUSB 接口句柄。 WinUSB 接口句柄用于定义所选配置中的第一个接口。

有关详细信息，请参阅 [如何使用 WinUSB 功能访问 USB 设备](/windows-hardware/drivers/ddi/index)。

 

