---
title: 打印驱动程序插件支持
description: 打印驱动程序插件支持
ms.assetid: fa072fc9-66da-46c2-a270-6f604860aaff
keywords:
- 打印功能 WDK，插件
- IPrintOemPrintTicketProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf3864edb10125695e96dc9ea357f77e295af646
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842346"
---
# <a name="print-driver-plug-in-support"></a>打印驱动程序插件支持


为基于微型驱动程序的打印驱动程序提供附加或修改功能的打印驱动程序插件必须支持[IPrintOemPrintTicketProvider 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintoemprintticketprovider)，以便在 Unidrv 或基于 PScript5 的打印驱动程序。 如果插件支持**IPrintOemPrintTicketProvider**，则该插件将获得编辑 PrintTicket 文档和修改配置用户界面（UI）的功能。 但对此接口的支持还需要比编辑 GPD 或 PPD 文件要大得多的开发工作。

不支持**IPrintOemPrintTicketProvider**接口的插件仅限于其现有的[**DEVMODEW**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)支持，因此插件提供的某些功能可能不会包含在 PrintTicket 或 PrintCapabilities 文档中。

 

 




