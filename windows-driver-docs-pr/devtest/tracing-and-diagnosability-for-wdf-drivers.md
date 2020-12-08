---
title: WDF 驱动程序的跟踪和诊断能力
description: 本文讨论了如何使用 windows 软件跟踪预处理器 (WPP) 在 Windows Driver Foundation (WDF) 驱动程序中实现事件跟踪。
ms.date: 07/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 548f66f2f59b58851f8a9de7823fbd8d79cf6e83
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838093"
---
# <a name="tracing-and-diagnosability-for-wdf-drivers"></a>WDF 驱动程序的跟踪和诊断能力


**上次更新时间：**

-   2008年10月19日

**适用于：**

-   Windows Server 2008
-   Windows Vista
-   Windows Server 2003
-   Windows XP
-   Windows 2000

本文讨论了如何使用 windows 软件跟踪预处理器 (WPP) 在 Windows Driver Foundation (WDF) 驱动程序中实现事件跟踪。

文件名： WPP \_intro.docx

169 KB

Microsoft Word 文件

[获取 Office 文件查看器](https://www.microsoft.com/download/office.aspx)

[![单击此处下载](./images/download.png)](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/WPP_intro.docx)

驱动程序的软件跟踪通常基于 Windows (ETW) 的事件跟踪，这是一种可记录内核模式和用户模式进程的跟踪消息的内核级功能。 由于 ETW 的使用可能有点复杂，因此大多数驱动程序开发人员都使用 Windows 软件跟踪预处理器 (WPP) ，这可简化和增强检测驱动程序的 ETW 跟踪过程。

## <a name="in-this-white-paper"></a>本白皮书内容：

-   WPP 软件跟踪基础知识
-   跟踪消息函数和宏
-   支持驱动程序中的软件跟踪
-   软件跟踪工具
-   如何运行软件跟踪会话

 

 





