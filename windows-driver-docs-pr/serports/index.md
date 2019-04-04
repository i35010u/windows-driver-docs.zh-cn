---
title: 串行控制器驱动程序设计指南
description: 你可以设计使用串行 I/O 请求接口与连接到串行端口的外围设备进行通信的驱动程序或应用程序。
ms.assetid: 66120e14-20dc-4220-b340-c05cbc59dac8
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: e92cc876a4d4f125577338b34d6dfb7e72e10069
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56465512"
---
# <a name="serial-controller-driver-design-guide"></a>串行控制器驱动程序设计指南


你可以设计使用[串行 I/O 请求接口](serial-i-o-request-interface.md)与连接到串行端口的外围设备进行通信的驱动程序或应用程序。 串行端口是串行控制器（16550 UART 或兼容设备）上的硬件通信接口。 若要控制外围设备永久连接到的串行端口，可以设计一个自定义串行控制器驱动程序，将其用于替代了串行框架扩展版本 1 (SerCx) 的版本 2 (SerCx2)。 或者，若要控制传统电脑的机箱上的已命名串行端口，可以使用内置的 Serial.sys 和 Serenum.sys 驱动程序。




## <a name="in-this-section"></a>本部分中的内容


-   [串行控制器驱动程序概述](serial-drivers-overview.md)
-   [使用串行框架扩展版本 2 (SerCx2)](using-version-2-of-the-serial-framework-extension.md)
-   [使用 Serial.sys 和 Serenum.sys](using-serial-sys-and-serenum-sys.md)

 

 




