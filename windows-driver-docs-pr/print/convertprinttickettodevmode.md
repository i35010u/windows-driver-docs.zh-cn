---
title: ConvertPrintTicketToDevMode 概述
description: 介绍应用程序的已传递打印票证中的 IPrintOemPrintTicketProvider：： ConvertPrintTicketToDevMode 方法使用情况。
ms.assetid: dd77d79e-e274-47c3-9bfd-95054bc9f23d
keywords:
- ConvertPrintTicketToDevMode
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b875e708473c6e2db86711b3af70fdec409f7d4c
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802455"
---
# <a name="convertprinttickettodevmode-overview"></a>ConvertPrintTicketToDevMode 概述


Unidrv 和 PScript5 打印驱动程序通过使用在应用程序调用 ConvertPrintTicketToDevMode 中传递的打印票证中的信息，填充它们支持的 [**DEVMODEW**](https://docs.microsoft.com/windows/win32/api/wingdi/ns-wingdi-devmodew) 结构的公共和私有部分。 对于安装的每个打印驱动程序插件，都将调用 [**IPrintOemPrintTicketProvider：： ConvertPrintTicketToDevMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemprintticketprovider-convertprinttickettodevmode) 方法。

下图显示了当驱动程序调用**ConvertPrintTicketToDevMode**时，对**IPrintOemPrintTicketProvider：： ConvertPrintTicketToDevMode**的调用的顺序。

![说明 convertprinttickettodevmode 调用序列的关系图](images/ptpcpt2dm-uml.gif)





