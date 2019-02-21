---
title: WPP 宏生成之前跟踪的优化条件检查
description: 可以优化 WPP 宏生成之前跟踪的条件检查
ms.assetid: 0d0ad0de-561f-4480-be91-2304242fee91
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4c50510ed28c00d9f32c5abe80e6aace29c2ddc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540860"
---
# <a name="can-i-optimize-the-conditional-checks-that-the-wpp-macros-produce-before-the-tracing"></a>可以优化 WPP 宏生成之前跟踪的条件检查？


您可以删除的条件检查 WPP\_INIT\_跟踪，以便它不通过 WPP 宏调用。 您可以执行此仅当 WPP\_INIT\_之前的源代码中进行的任何尝试跟踪调用跟踪你[跟踪提供程序](trace-provider.md)，如内核模式驱动程序或用户模式应用程序。

**重要**  在对象构造函数或宏中进行跟踪，不应删除此检查。 否则，无法跟踪提供程序中发生访问冲突。

 

包括之前[跟踪消息标头 (.tmh) 文件](trace-message-header-file.md)在源代码中添加以下定义，以禁用 WPP 条件检查\_INIT\_跟踪：

```
#define WPP_CHECK_INIT
```

 

 





