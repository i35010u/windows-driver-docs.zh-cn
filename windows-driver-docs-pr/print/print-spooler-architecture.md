---
title: 打印后台处理程序体系结构
description: 打印后台处理程序体系结构
keywords:
- 后台处理程序体系结构 WDK 打印
- 打印后台处理程序体系结构 WDK
- 作业 WDK 打印，打印后台打印
- 打印作业 WDK，打印后台打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb4a16a61953786d7dd35b4fb6609a4e8c56c4a7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807457"
---
# <a name="print-spooler-architecture"></a>打印后台处理程序体系结构





Microsoft Windows 2000 和更高版本打印后台处理程序由一组由 Microsoft 提供的可选供应商提供的组件组成，责任包括：

-   确定打印作业是否应在本地处理或跨网络处理。

-   接受由 GDI 创建的数据流，并将其与打印机驱动程序一起用于特定类型打印机上的输出。

-   如果) 启用了假脱机，则将数据缓冲到文件 (。

-   选择逻辑打印机队列中第一个可用的物理打印机。

-   将数据流转换为假脱机格式 (例如，将 *(EMF) 的增强型图元文件*) 为可发送到打印机硬件的格式 (例如 *打印机控制语言 (PCL)*) 。

-   将数据流发送到打印机硬件。

-   为 [后台处理程序组件](spooler-components.md) 和 [打印机窗体](printer-forms-support.md)维护基于注册表的数据库。

-    (Windows Vista) 在客户端计算机上而不是打印服务器上呈现打印作业。 [客户端呈现](client-side-rendering.md) 使打印服务器工作负荷变得透明，对打印驱动程序是透明的，并且在 Windows Vista 中默认启用。

-   对于 Windows 7，打印驱动程序可在独立于后台处理程序的进程中运行。 此功能称为 [打印机驱动程序隔离](printer-configuration.md)。

 

 




