---
title: 打印驱动程序插件支持
description: 打印驱动程序插件支持
ms.assetid: fa072fc9-66da-46c2-a270-6f604860aaff
keywords:
- 打印功能 WDK，插件
- IPrintOemPrintTicketProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 380f79f6f43ad1b369ef15574678c53155fcd2ee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354923"
---
# <a name="print-driver-plug-in-support"></a>打印驱动程序插件支持


打印驱动程序的管理单元提供的基于微型驱动程序的打印驱动程序的其他或已修改功能必须支持[IPrintOemPrintTicketProvider 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintoemprintticketprovider)提供完成和支持中的正确打印功能Unidrv 或基于 PScript5 的打印驱动程序。 如果插件支持**IPrintOemPrintTicketProvider**，插件将获得编辑 PrintTicket 文档和修改配置用户界面 (UI) 的能力。 但是，支持此接口还需要多得多的开发工作比只需编辑 GPD 或 PPD 文件。

不支持的插件**IPrintOemPrintTicketProvider**接口仅限于其现有[ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)支持，一些函数，该插件提供了可能不会包含 PrintTicket 或 PrintCapabilities 文档中。

 

 




