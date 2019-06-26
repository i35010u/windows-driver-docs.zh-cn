---
title: 控制 GUID 文件
description: 控制 GUID 文件
ms.assetid: cf5dd9bf-c9db-4324-abd3-ee0e1b15e14d
keywords:
- 控件 Guid WDK
- .ctl 文件
- ctl 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db5c212feb92780f3a19423fc0c53067965d8c58
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371589"
---
# <a name="control-guid-file"></a>控制 GUID 文件

## <span id="ddk_control_guid_file_tools"></span><span id="DDK_CONTROL_GUID_FILE_TOOLS"></span>

*控制 GUID 文件*（.ctl 扩展名） 是指定一个文本文件[控制 GUID](control-guid.md)的跟踪提供程序和格式的 GUID 的友好名称：

```
ControlGUID GUIDFriendlyName
```

跟踪提供程序的开发人员通常提供此文件。 但是，如果必须跟踪提供程序的源代码，可以查找 GUID 和 GUID 友好名称，并创建控制 GUID 文件。

在源代码中，找到的定义[WPP\_控制\_GUID](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))宏。 中所示的 GUID 值和 GUID 的友好名称下面的示例中以粗体显示。

```C
#define WPP_CONTROL_GUIDS \
    WPP_DEFINE_CONTROL_GUID(GUIDFriendlyName, (ControlGUID),  \
        WPP_DEFINE_BIT(NameOfTraceFlag1)  \
        WPP_DEFINE_BIT(NameOfTraceFlag2)  \
        .............................   \
        .............................   \
        WPP_DEFINE_BIT(NameOfTraceFlag31) )
```
