---
title: 在其中放置
description: 在其中放置
ms.assetid: 5d8a2bb7-efe1-4cf2-9424-b63d4f17805e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e99786e33559627d9e1e8d31096eb6e25792c22
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541190"
---
# <a name="where-do-i-put-the-include-statement-for-the-trace-message-header-file"></a>在其中放置\#包括语句为跟踪消息标头文件？


**\#包括**语句[跟踪消息标头文件](trace-message-header-file.md)后的定义中必须出现在源文件中[WPP\_控件\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)宏和之前的任何 WPP 宏调用。

如果使用的项目范围标头文件，将放**\#包括**语句之后的跟踪消息标头文件**\#包括**项目范围标头的语句文件。

 

 





