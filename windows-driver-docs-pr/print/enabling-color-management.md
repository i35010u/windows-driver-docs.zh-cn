---
title: 启用颜色管理
description: 启用颜色管理
keywords:
- 颜色管理 WDK 打印，启用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4996f429deb22fa5c2ff340bcf20cae55029671
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797139"
---
# <a name="enabling-color-management"></a>启用颜色管理





应用程序或打印机驱动程序可以启用颜色管理。 应用程序可以通过以下两种方法之一启用颜色管理：

-   调用 **SetICMMode** (在 Microsoft Windows SDK 文档) 中介绍，并 \_ 在上指定 ICM。

    此方法可实现系统控制的颜色管理。

-   在调用 **CreateDC** 创建打印作业时指定 [**DEVMODEW**](/windows/win32/api/wingdi/ns-wingdi-devmodew)结构，并 \_ \_ \_ 在 DEVMODE 结构的 **DMICMMETHOD** 成员中设置 DMICMMETHOD 系统、DMICMMETHOD 驱动程序或 DMICMMETHOD 设备。

    此方法允许应用程序选择系统控制的、驱动程序控制的或设备控制的颜色管理 (，前提是) 支持指定的控件类型。

打印机驱动程序可以通过 \_ \_ \_ 在驱动程序的默认 DEVMODE 结构的 **DMICMMETHOD** 成员中设置 DMICMMETHOD 系统、DMICMMETHOD DRIVER 或 DMICMMETHOD 设备来启用颜色管理。  (如果为 **CreateDC** 提供 DEVMODE 结构，应用程序可以重写默认设置。 此外，驱动程序负责在执行驱动程序的 [**DrvDocumentPropertySheets**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentpropertysheets) 函数期间存储用户的颜色管理选择。 ) 

 

