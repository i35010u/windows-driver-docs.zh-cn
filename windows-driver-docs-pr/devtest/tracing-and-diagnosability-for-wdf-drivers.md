---
title: 跟踪和 WDF 驱动程序的诊断能力
description: 本白皮书讨论如何实现 Windows Driver Foundation (WDF) 驱动程序中使用 Windows 软件跟踪预处理器 (WPP) 的事件跟踪。
ms.assetid: C89A218F-3E73-4D3E-8F53-5D52E97711EF
ms.date: 07/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ccf50f665a9025c01bfbc5f9cb3657a578c0110
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540460"
---
# <a name="tracing-and-diagnosability-for-wdf-drivers"></a>跟踪和 WDF 驱动程序的诊断能力


**上次更新时间：**

-   2008 年 10 月 19日日

**适用于：**

-   Windows Server 2008
-   Windows Vista
-   Windows Server 2003
-   Windows XP
-   Windows 2000

本白皮书讨论如何实现 Windows Driver Foundation (WDF) 驱动程序中使用 Windows 软件跟踪预处理器 (WPP) 的事件跟踪。

文件名：WPP\_intro.docx

169 KB

Microsoft Word 文件

[获取 Office 文件查看器](http://www.microsoft.com/download/office.aspx)

[![单击此处下载](./images/download.png)](http://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/WPP_intro.docx)

驱动程序软件跟踪通常基于对事件跟踪 Windows (ETW)，内核级别的设备，记录的内核模式和用户模式进程的跟踪消息。 ETW 可以是使用有点复杂，因为大多数驱动程序开发人员使用的 Windows 软件跟踪预处理器 (WPP)，从而简化和增强检测 ETW 跟踪的驱动程序的过程。

## <a name="in-this-white-paper"></a>在本白皮书：

-   WPP 软件跟踪基础知识
-   跟踪消息函数和宏
-   在驱动程序支持软件跟踪
-   适用于软件跟踪工具
-   如何运行软件跟踪会话

 

 





