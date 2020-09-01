---
title: ConvertPrintTicketToDevMode 概述
description: 介绍应用程序的已传递打印票证中的 IPrintOemPrintTicketProvider：： ConvertPrintTicketToDevMode 方法使用情况。
ms.assetid: dd77d79e-e274-47c3-9bfd-95054bc9f23d
keywords:
- ConvertPrintTicketToDevMode
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da44c186313c233856eacbbb5f7d3a9e8730e4b6
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214945"
---
# <a name="convertprinttickettodevmode-overview"></a>ConvertPrintTicketToDevMode 概述


Unidrv 和 PScript5 打印驱动程序通过使用在应用程序调用 ConvertPrintTicketToDevMode 中传递的打印票证中的信息，填充它们支持的 [**DEVMODEW**](/windows/win32/api/wingdi/ns-wingdi-devmodew) 结构的公共和私有部分。 对于安装的每个打印驱动程序插件，都将调用 [**IPrintOemPrintTicketProvider：： ConvertPrintTicketToDevMode**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemprintticketprovider-convertprinttickettodevmode) 方法。

下图显示了当驱动程序调用**ConvertPrintTicketToDevMode**时，对**IPrintOemPrintTicketProvider：： ConvertPrintTicketToDevMode**的调用的顺序。

![说明 convertprinttickettodevmode 调用序列的关系图](images/ptpcpt2dm-uml.gif)