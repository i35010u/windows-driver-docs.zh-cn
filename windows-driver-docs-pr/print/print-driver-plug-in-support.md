---
title: 打印驱动程序插件支持
description: 打印驱动程序插件支持
keywords:
- 打印功能 WDK，插件
- IPrintOemPrintTicketProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2373c5730ed199ab67186b7f380c4131dc471d0e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807481"
---
# <a name="print-driver-plug-in-support"></a>打印驱动程序插件支持


为基于微型驱动程序的打印驱动程序提供附加或修改功能的打印驱动程序插件必须支持 [IPrintOemPrintTicketProvider 接口](/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintoemprintticketprovider) ，以便在 Unidrv 或 PScript5 的打印驱动程序中提供完整且正确的打印功能支持。 如果插件支持 **IPrintOemPrintTicketProvider**，则该插件将获得编辑 PrintTicket 文档和)  (UI 修改配置用户界面的功能。 但对此接口的支持还需要比编辑 GPD 或 PPD 文件要大得多的开发工作。

不支持 **IPrintOemPrintTicketProvider** 接口的插件仅限于其现有的 [**DEVMODEW**](/windows/win32/api/wingdi/ns-wingdi-devmodew) 支持，因此插件提供的某些功能可能不会包含在 PrintTicket 或 PrintCapabilities 文档中。

 

