---
title: 打印功能体系结构
description: 打印功能体系结构
keywords:
- 打印功能 WDK，体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac86008c9e4cfd1ba61cc3723fc46060e66b10d9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807515"
---
# <a name="print-capabilities-architecture"></a>打印功能体系结构


PrintCapabilities 对象由打印驱动程序的 [IPrintTicketProvider 接口](/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))实现的 [**IPrintTicketProvider：： GetPrintCapabilities**](/previous-versions/windows/hardware/drivers/ff554365(v=vs.85))方法返回。 除了 [**DrvDeviceCapabilities**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicecapabilities) 函数外，XPSDrv 打印驱动程序必须实现 IPrintTicketProvider 接口。

您可以修改旧的基于 GDI 的打印驱动程序，以便直接提供 PrintCapabilities 文档，但这不是必需的。 Windows Vista 打印子系统为基于 GDI 的驱动程序创建一个 XML PrintCapabilities 文档，该文档不会添加返回一个的功能。 但是，Windows Vista 打印子系统创建的 PrintCapabilities 文档仅包含 Microsoft Win32 函数 **DeviceCapabilities** 支持的有限参数集。 要使基于 GDI 的打印驱动程序提供打印机特性和功能的完整列表，它必须包含对 [IPrintTicketProvider 接口](/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))的支持。

以下列表和关系图说明了不同类型的打印驱动程序如何支持打印功能技术：

<a href="" id="unidrv-or-pscript5-print-driver"></a>Unidrv 或 PScript5 打印驱动程序  
在 Windows Vista 中， [IPrintTicketProvider 接口](/previous-versions/windows/hardware/drivers/ff554375(v=vs.85)) 已添加到通用 (Unidrv) 和 PostScript (PScript5) 打印驱动程序。

<a href="" id="unidrv-or-pscript5-print-driver-plug-in"></a>Unidrv 或 PScript5 打印驱动程序插件  
具有自定义功能的 Unidrv 和 Pscript5 打印驱动程序要求插件添加或删除功能并返回准确的 PrintCapabilities 文档。 Unidrv 和 PScript5 打印驱动程序的自定义功能插件必须支持 [IPrintOemPrintTicketProvider 接口](/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintoemprintticketprovider)。

<a href="" id="-monolithic-gdi-based-and-xpsdrv-print-drivers"></a> 单一的基于 GDI 的和 XPSDrv 打印驱动程序  
XPSDrv 打印驱动程序必须支持 [IPrintTicketProvider 接口](/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))。 基于 GDI 的单一打印驱动程序必须支持 IPrintTicketProvider 接口，以返回 Win32 函数 **DeviceCapabilities** 不提供的打印机功能和功能。

![说明打印驱动程序中支持的打印功能的关系图](images/ptpcarch1.gif)

 

