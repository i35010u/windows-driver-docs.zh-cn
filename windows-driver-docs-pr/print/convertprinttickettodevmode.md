---
title: ConvertPrintTicketToDevMode 概述
description: 介绍 IPrintOemPrintTicketProvider::ConvertPrintTicketToDevMode 方法从应用程序传递的打印票证的使用情况。
ms.assetid: dd77d79e-e274-47c3-9bfd-95054bc9f23d
keywords:
- ConvertPrintTicketToDevMode
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d3b3ce6e3e4fa0ac7392810fb31ef7e5942f9ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568507"
---
# <a name="convertprinttickettodevmode-overview"></a>ConvertPrintTicketToDevMode 概述


Unidrv 和打印驱动程序中的公共和私有部分填充的 PScript5 [ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)它们支持通过使用来自传入应用程序的打印票证信息的结构调用到 ConvertPrintTicketToDevMode。 [ **IPrintOemPrintTicketProvider::ConvertPrintTicketToDevMode** ](https://msdn.microsoft.com/library/windows/hardware/ff553167)为每个打印驱动程序插件已安装的调用方法。

下图显示了为调用的顺序**IPrintOemPrintTicketProvider::ConvertPrintTicketToDevMode**当驱动程序调用**ConvertPrintTicketToDevMode**。

![说明调用序列 convertprinttickettodevmode 的关系图](images/ptpcpt2dm-uml.gif)





