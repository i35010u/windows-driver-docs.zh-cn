---
title: 打开和关闭端口
description: 打开和关闭端口
ms.assetid: 8bfdb3af-51d4-4252-ae1c-7910f973f5f6
keywords:
- 打印监视器 WDK，端口管理
- 端口管理 WDK 打印，打开端口
- 打开打印端口
- 端口管理 WDK 打印，关闭端口
- 关闭打印端口
- OpenPort
- OpenPortEx
- ClosePort
- 后台处理程序打开和关闭端口 WDK 打印
- 打印后台处理程序打开和关闭端口 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6eaa0f72b8f575a9255ec0b91f0a6ced2ad3f7d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213649"
---
# <a name="opening-and-closing-a-port"></a>打开和关闭端口





添加端口后，如 [添加端口](adding-a-port.md)中所述，后台处理程序可以通过调用相应的语言监视器的 [**OpenPortEx**](/previous-versions/ff559596(v=vs.85)) 函数来打开该端口。

语言监视器使用 **OpenPortEx** 函数来创建和返回端口句柄。 通常，语言监视器调用其关联的端口监视器的 [**OpenPort**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-openport) 函数，而 language 监视器只返回从端口监视器的 **OpenPort**获取的句柄。

如果没有与某个端口关联的语言监视器，则后台处理程序会直接调用端口监视器的 **OpenPort** 函数。

后台处理程序不允许一次启用端口的多个路径。 因此，在特定监视器中调用了 **OpenPortEx** (或 **OpenPort**) 后，在关闭它之前，它不会尝试再次打开相同的端口。

打开端口后，后台处理程序可以调用其他函数来打印作业，如 [打印打印作业](printing-a-print-job.md)中所述，使用端口句柄作为输入参数。 应该写入监视器，以便在打开端口之后，后台处理程序可以在关闭端口前发送多个打印作业。

如果必须通过不同的语言监视器发送作业，则后台处理程序会关闭端口，如果不存在与端口关联的打印队列，或当系统关闭时。 若要关闭某个端口，后台处理程序将调用语言监视器的 [**ClosePort**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-closeport) 函数。 函数使打开端口时创建的句柄无效。 语言监视器通常会调用由其关联的端口监视器定义的 **ClosePort** 函数。

如果没有与某个端口关联的语言监视器，则后台处理程序会直接调用端口监视器的 **ClosePort** 函数。

 

