---
title: 控制 GUID 文件
description: 控制 GUID 文件
keywords:
- 控制 Guid WDK
- ctl 文件
- ctl 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: becdbcf267f3a04bc1b840246ab95cc27f66e3e2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801853"
---
# <a name="control-guid-file"></a>控制 GUID 文件

## <span id="ddk_control_guid_file_tools"></span><span id="DDK_CONTROL_GUID_FILE_TOOLS"></span>

*控件 guid 文件* ( 扩展名) 是一个文本文件，该文件指定跟踪提供程序的 [控件 GUID](control-guid.md)和 GUID 的友好名称，格式为：

```
ControlGUID GUIDFriendlyName
```

跟踪提供程序的开发人员通常会提供此文件。 但是，如果您具有跟踪提供程序的源代码，则可以找到 GUID 和 GUID 友好名称，并创建控件 GUID 文件。

在源代码中，查找 [WPP \_ 控件 \_ guid](/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85)) 宏的定义。 在下面的示例中，GUID 值和 GUID 友好名称以粗体显示。

```C
#define WPP_CONTROL_GUIDS \
    WPP_DEFINE_CONTROL_GUID(GUIDFriendlyName, (ControlGUID),  \
        WPP_DEFINE_BIT(NameOfTraceFlag1)  \
        WPP_DEFINE_BIT(NameOfTraceFlag2)  \
        .............................   \
        .............................   \
        WPP_DEFINE_BIT(NameOfTraceFlag31) )
```
