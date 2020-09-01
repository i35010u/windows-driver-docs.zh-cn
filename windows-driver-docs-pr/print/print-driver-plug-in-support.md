---
title: 打印驱动程序插件支持
description: 打印驱动程序插件支持
ms.assetid: fa072fc9-66da-46c2-a270-6f604860aaff
keywords:
- 打印功能 WDK，插件
- IPrintOemPrintTicketProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 349917e6168397579ea14f7dfcd17c0a8ea3a060
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214206"
---
# <a name="print-driver-plug-in-support"></a>打印驱动程序插件支持


为基于微型驱动程序的打印驱动程序提供附加或修改功能的打印驱动程序插件必须支持 [IPrintOemPrintTicketProvider 接口](/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintoemprintticketprovider) ，以便在 Unidrv 或 PScript5 的打印驱动程序中提供完整且正确的打印功能支持。 如果插件支持 **IPrintOemPrintTicketProvider**，则该插件将获得编辑 PrintTicket 文档和)  (UI 修改配置用户界面的功能。 但对此接口的支持还需要比编辑 GPD 或 PPD 文件要大得多的开发工作。

不支持 **IPrintOemPrintTicketProvider** 接口的插件仅限于其现有的 [**DEVMODEW**](/windows/win32/api/wingdi/ns-wingdi-devmodew) 支持，因此插件提供的某些功能可能不会包含在 PrintTicket 或 PrintCapabilities 文档中。

 

