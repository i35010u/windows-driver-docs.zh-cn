---
title: 在哪里放置
description: 在哪里放置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba05895541b01b6fad23a0b36ecc10ccd932d45e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810671"
---
# <a name="where-do-i-put-the-include-statement-for-the-trace-message-header-file"></a>在哪里放置 \# 跟踪消息头文件的 include 语句？


[跟踪消息标头文件](trace-message-header-file.md)的 **\# Include** 语句必须在 [wpp \_ 控件 \_ guid](/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))宏的定义之后和任何 WPP 宏调用之前出现在源文件中。

如果使用的是项目范围的标头文件，请在项目范围标头文件的 **\# include** 语句后面放置跟踪消息头文件的 **\# include** 语句。

 

