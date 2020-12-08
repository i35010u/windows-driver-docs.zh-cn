---
title: 优化 WPP 宏在跟踪之前生成的条件检查
description: 是否可以优化 WPP 宏在跟踪之前生成的条件检查
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b269d2a9b73341591ba3620b81ff2c6232fcd6bc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791575"
---
# <a name="can-i-optimize-the-conditional-checks-that-the-wpp-macros-produce-before-the-tracing"></a>是否可以优化 WPP 宏在跟踪之前生成的条件检查？


可以移除 WPP INIT 跟踪的条件检查 \_ ， \_ 使其不会通过 wpp 宏调用。 仅当在 \_ \_ [跟踪提供程序](trace-provider.md)的源代码（如内核模式驱动程序或用户模式应用程序）内进行任何跟踪尝试之前，才可以执行此操作。

**重要提示**  如果在对象构造函数或宏中进行了跟踪，则不应删除此项检查。 否则，在跟踪提供程序中可能会发生访问冲突。


在您的源代码中包括 [跟踪消息标头 ( tmh) 文件](trace-message-header-file.md) 之前，请添加以下定义以禁用 WPP INIT 跟踪的条件检查 \_ \_ ：

```
#define WPP_CHECK_INIT
```

 

 





