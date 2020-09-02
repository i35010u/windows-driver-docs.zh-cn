---
title: 在哪里放置
description: 在哪里放置
ms.assetid: 5d8a2bb7-efe1-4cf2-9424-b63d4f17805e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e999fe43fb26eb61fe0c228493e1cbc9f416b8f
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383203"
---
# <a name="where-do-i-put-the-include-statement-for-the-trace-message-header-file"></a>在哪里放置 \# 跟踪消息头文件的 include 语句？


[跟踪消息标头文件](trace-message-header-file.md)的** \# Include**语句必须在[wpp \_ 控件 \_ guid](/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))宏的定义之后和任何 WPP 宏调用之前出现在源文件中。

如果使用的是项目范围的标头文件，请在项目范围标头文件的** \# include**语句后面放置跟踪消息头文件的** \# include**语句。

 

