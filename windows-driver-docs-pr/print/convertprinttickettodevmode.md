---
title: ConvertPrintTicketToDevMode 概述
description: 介绍 IPrintOemPrintTicketProvider::ConvertPrintTicketToDevMode 方法从应用程序传递的打印票证的使用情况。
ms.assetid: dd77d79e-e274-47c3-9bfd-95054bc9f23d
keywords:
- ConvertPrintTicketToDevMode
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1be0b61b03044ff5e24f193f1844db38f4abdc6a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372473"
---
# <a name="convertprinttickettodevmode-overview"></a>ConvertPrintTicketToDevMode 概述


Unidrv 和打印驱动程序中的公共和私有部分填充的 PScript5 [ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)它们支持通过使用来自传入应用程序的打印票证信息的结构调用到 ConvertPrintTicketToDevMode。 [ **IPrintOemPrintTicketProvider::ConvertPrintTicketToDevMode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemprintticketprovider-convertprinttickettodevmode)为每个打印驱动程序插件已安装的调用方法。

下图显示了为调用的顺序**IPrintOemPrintTicketProvider::ConvertPrintTicketToDevMode**当驱动程序调用**ConvertPrintTicketToDevMode**。

![说明调用序列 convertprinttickettodevmode 的关系图](images/ptpcpt2dm-uml.gif)





