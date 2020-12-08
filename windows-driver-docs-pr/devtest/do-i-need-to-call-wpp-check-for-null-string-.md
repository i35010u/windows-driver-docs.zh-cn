---
title: 是否需要调用 WPP_CHECK_FOR_NULL_STRING
description: 是否需要调用 WPP_CHECK_FOR_NULL_STRING
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6cd895146dffdaebe93b34c8dd491a6132379cae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839009"
---
# <a name="do-i-need-to-call-wpp_check_for_null_string"></a>是否需要为 \_ 空字符串调用 WPP \_ 检查 \_ \_ ？


从 Windows 7 版本的 Windows 驱动程序工具包开始 (WDK) ，跟踪组件会自动检查传入到跟踪函数的参数中是否存在 **NULL** 字符串。 因此，无需调用 WPP \_ 检查来 \_ \_ \_ 验证每个参数，以防止 **空** 字符串导致异常。

如果使用 Windows 7 和更高版本的 WDK 生成 [跟踪提供程序](trace-provider.md) (如驱动程序或应用程序) ，则可以 \_ \_ \_ \_ 从源代码中删除空字符串宏的 WPP 检查。

 

 





