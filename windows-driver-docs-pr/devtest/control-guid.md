---
title: 控制 GUID
description: 控制 GUID
ms.assetid: a85a5e1a-c4c1-40d4-a0ef-d8e552590f03
keywords:
- 控制 Guid WDK
- Guid WDK 软件跟踪
- 标识符 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24b9b442acc4074e75ba3db0528c6554e7fc8739
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383985"
---
# <a name="control-guid"></a>控制 GUID

## <span id="ddk_control_guid_tools"></span><span id="DDK_CONTROL_GUID_TOOLS"></span>

每个 [跟踪提供程序](trace-provider.md) 都定义了一个用于唯一标识提供程序的 *控件 GUID* 。 此 GUID 用于通过 [Windows (ETW) 的事件跟踪 ](event-tracing-for-windows--etw-.md)启用或禁用跟踪提供程序。

控件 GUID 显示在已检测跟踪提供程序的源代码文件的 [WPP \_ 控件 \_ guid](/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85)) 宏中。

```C
#define WPP_CONTROL_GUIDS \
    WPP_DEFINE_CONTROL_GUID(GUIDFriendlyName, (ControlGUID),  \
        WPP_DEFINE_BIT(NameOfTraceFlag1)  \
        WPP_DEFINE_BIT(NameOfTraceFlag2)  \
        .............................   \
        .............................   \
        WPP_DEFINE_BIT(NameOfTraceFlag31) )
```

[Tracepdb](tracepdb.md) 创建一个 [跟踪 (MOF) 文件](trace-managed-object-format--mof--file.md) ，其中包含 PDB 文件中表示的每个跟踪提供程序的控件 GUID 和跟踪级别。 MOF 文件的名称为跟踪提供程序的模块名称。 如果使用 **-c** 选项，Tracepdb 还可以生成 TMC 文件。

由于控件 GUID 向 ETW 标识跟踪提供程序，因此可以使用控件 GUID 来定义和重新定义 [跟踪提供程序](trace-provider.md)的范围。 例如，多个驱动程序可以是单个跟踪提供程序的一部分，方法是指定相同的控件 GUID。 或者，单个驱动程序可以通过在 [WPP \_ 控件 \_ guid](/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85)) 宏的每个实例中指定不同的控件 guid 来包含多个跟踪提供程序。