---
title: 打印后台处理程序体系结构
description: 打印后台处理程序体系结构
ms.assetid: 712da599-29cb-4df9-9627-49907f0aa500
keywords:
- 后台处理程序体系结构 WDK 打印
- 打印后台处理程序体系结构 WDK
- 作业 WDK 打印、 打印后台处理程序
- 打印作业 WDK、 打印后台处理程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bf65d0edf49f9f3ffe0df4441e58915ada3f1ed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565686"
---
# <a name="print-spooler-architecture"></a>打印后台处理程序体系结构





Microsoft Windows 2000 和更高版本的打印后台处理程序是组成一组 Microsoft 提供和可选供应商提供组件，与职责包括：

-   确定本地或网络中是否应处理打印作业。

-   接受通过 GDI，结合使用的打印机驱动程序，在特定类型的打印机上的输出创建数据流。

-   （如果已启用后台处理） 进行后台打印到文件的数据。

-   选择逻辑打印机队列中的第一个可用的物理打印机。

-   从进行后台处理格式转换数据流 (如*增强型图元文件 (EMF)*) 可以发送到打印机硬件的格式 (如*打印机控制语言 (PCL)*)。

-   将数据流发送到打印机硬件。

-   维护的基于注册表的数据库[后台处理程序组件](spooler-components.md)并[打印机纸张规格](printer-forms-support.md)。

-   (Windows Vista)呈现而不是打印服务器上的客户端计算机上的打印作业。 [客户端呈现](client-side-rendering.md)简化了打印服务器工作负荷，是透明的打印驱动程序，Windows Vista 中默认情况下启用。

-   对于 Windows 7，打印驱动程序可以运行的单独进程中从后台处理程序。 此功能被称为[打印机驱动程序隔离](printer-configuration.md)。

 

 




