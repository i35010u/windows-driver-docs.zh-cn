---
title: 打印驱动程序插件支持
description: 打印驱动程序插件支持
ms.assetid: fa072fc9-66da-46c2-a270-6f604860aaff
keywords:
- 打印功能 WDK，插件
- IPrintOemPrintTicketProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4edb3b4df5a265e22c8a97f07da02336b20ef474
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576530"
---
# <a name="print-driver-plug-in-support"></a>打印驱动程序插件支持


打印驱动程序的管理单元提供的基于微型驱动程序的打印驱动程序的其他或已修改功能必须支持[IPrintOemPrintTicketProvider 接口](https://msdn.microsoft.com/library/windows/hardware/ff553174)提供完成和支持中的正确打印功能Unidrv 或基于 PScript5 的打印驱动程序。 如果插件支持**IPrintOemPrintTicketProvider**，插件将获得编辑 PrintTicket 文档和修改配置用户界面 (UI) 的能力。 但是，支持此接口还需要多得多的开发工作比只需编辑 GPD 或 PPD 文件。

不支持的插件**IPrintOemPrintTicketProvider**接口仅限于其现有[ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)支持，一些函数，该插件提供了可能不会包含 PrintTicket 或 PrintCapabilities 文档中。

 

 




