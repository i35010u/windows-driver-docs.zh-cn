---
title: 打印驱动程序插件支持
description: 打印驱动程序插件支持
ms.assetid: fa072fc9-66da-46c2-a270-6f604860aaff
keywords:
- 打印功能 WDK，插件
- IPrintOemPrintTicketProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4c085949574449f17458345695eb44f1b3c3e63
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802549"
---
# <a name="print-driver-plug-in-support"></a>打印驱动程序插件支持


为基于微型驱动程序的打印驱动程序提供附加或修改功能的打印驱动程序插件必须支持 [IPrintOemPrintTicketProvider 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintoemprintticketprovider) ，以便在 Unidrv 或 PScript5 的打印驱动程序中提供完整且正确的打印功能支持。 如果插件支持 **IPrintOemPrintTicketProvider**，则该插件将获得编辑 PrintTicket 文档和)  (UI 修改配置用户界面的功能。 但对此接口的支持还需要比编辑 GPD 或 PPD 文件要大得多的开发工作。

不支持 **IPrintOemPrintTicketProvider** 接口的插件仅限于其现有的 [**DEVMODEW**](https://docs.microsoft.com/windows/win32/api/wingdi/ns-wingdi-devmodew) 支持，因此插件提供的某些功能可能不会包含在 PrintTicket 或 PrintCapabilities 文档中。

 

 




