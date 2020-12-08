---
title: ACPI IPMI 操作区域
description: ACPI IPMI 操作区域
keywords:
- 电源计量和预算 WDK，ACPI IPMI 操作区域
- ACPI IPMI 操作区域 WDK 电源计量器
- IPMI WDK 电源指示器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff88e98216915eb80230318d2baace3b709e3974
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812473"
---
# <a name="acpi-ipmi-operation-region"></a>ACPI IPMI 操作区域


许多系统使用智能平台管理接口 (IPMI) 与服务处理器或基板管理控制器进行通信 (BMC) 。

从 Windows 7 和 Windows Server 2008 R2 开始，操作系统为 IPMI 访问服务处理器或 Bmc 提供了标准化的 ACPI IPMI 操作区域。 这使得设备能够通过 ACPI 计算机语言 (AML) 访问 IPMI 数据，并允许硬件平台使用其 ACPI 固件发出 IPMI 请求。

操作系统提供支持 ACPI IPMI 操作区域的 IPMI 驱动程序。 驱动程序服务 IPMI 请求，必须使用键盘控制器样式 (KCS) 协议。

有关详细信息，请参阅 [IPMI 版本2.0 规范](https://go.microsoft.com/fwlink/p/?linkid=69485)。

 

 




