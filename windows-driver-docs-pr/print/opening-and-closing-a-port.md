---
title: 打开和关闭端口
description: 打开和关闭端口
ms.assetid: 8bfdb3af-51d4-4252-ae1c-7910f973f5f6
keywords:
- 打印监视器 WDK，端口管理
- 端口管理 WDK 打印，打开端口
- 打开打印端口
- 端口管理 WDK 打印，结束端口
- 关闭打印端口
- OpenPort
- OpenPortEx
- ClosePort
- 打印后台处理程序打开和关闭端口 WDK
- 打印后台处理程序打开和关闭端口 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb3f7e5a8687bf04fb00bf84b69972cee670eade
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339881"
---
# <a name="opening-and-closing-a-port"></a>打开和关闭端口





已添加了一个端口，如中所述后[添加一个端口](adding-a-port.md)，后台处理程序可以打开它通过调用相应的语言监视器[ **OpenPortEx** ](https://msdn.microsoft.com/library/windows/hardware/ff559596)函数。

使用的语言监视器**OpenPortEx**函数创建并返回端口句柄。 通常情况下，语言监视器调用其关联的端口监视器[ **OpenPort** ](https://msdn.microsoft.com/library/windows/hardware/ff559593)函数，并监视从端口监视器获取句柄的只是返回的语言**OpenPort**.

如果语言监视器不是与端口相关联，后台处理程序会调用端口监视器**OpenPort**直接函数。

后台处理程序不允许到端口一次启用多个路径。 因此，之后该维度被称为**OpenPortEx** (或**OpenPort**) 在特定监视器中，它不会尝试在关闭之前再次打开相同的端口。

打开端口后，后台处理程序可以调用其他函数来打印作业，如中所述[打印打印作业](printing-a-print-job.md)，作为输入参数中使用的端口句柄。 以便打开端口后，后台处理程序可以将多个打印作业发送关闭端口之前，应编写一个监视器。

如果没有打印队列都与一个端口，如果必须通过不同的语言监视器发送作业或系统关闭时，后台处理程序将关闭端口。 若要关闭一个端口，后台处理程序调用的语言监视器[ **ClosePort** ](https://msdn.microsoft.com/library/windows/hardware/ff545975)函数。 函数不会打开该端口时创建的句柄无效。 一种语言通常监视调用**ClosePort**由其关联的端口监视器定义的函数。

如果语言监视器不是与端口相关联，后台处理程序会调用端口监视器**ClosePort**直接函数。

 

 




