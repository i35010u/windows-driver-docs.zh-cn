---
title: ACPI IPMI 操作区域
description: ACPI IPMI 操作区域
ms.assetid: fb953ee1-2628-4cd1-a2d3-a725cf59cc9f
keywords:
- Power 计量和预算 WDK，ACPI IPMI 运营区域
- ACPI IPMI 运营区域 WDK 电源表
- IPMI WDK 电源表
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9439156eabf8452f21fc7aa0a26056bf439a2b85
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349263"
---
# <a name="acpi-ipmi-operation-region"></a>ACPI IPMI 操作区域


许多系统使用智能平台管理接口 (IPMI) 与服务处理器或基板管理控制器 (BMC) 进行通信。

从 Windows 7 和 Windows Server 2008 R2 开始，到服务处理器或 Bmc IPMI 访问操作系统提供标准化的 ACPI IPMI 运营区域。 这使设备可以通过访问 IPMI 数据通过 ACPI 机器语言 (AML)，并使硬件平台，通过使用其 ACPI 固件发出 IPMI 请求。

操作系统提供支持 ACPI IPMI 运营区域 IPMI 驱动程序。 该驱动程序服务必须通过使用键盘控制器样式 (KCS) 协议进行的 IPMI 请求。

有关详细信息，请参阅[IPMI 版本 2.0 规范](https://go.microsoft.com/fwlink/p/?linkid=69485)。

 

 




