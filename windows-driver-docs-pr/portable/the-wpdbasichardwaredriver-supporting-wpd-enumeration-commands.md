---
description: 支持 (WpdBasicHardwareDriverSample) 的枚举命令
title: 支持 (WpdBasicHardwareDriverSample) 的枚举命令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1dbd863c66b5781be004536f093bd93b10277c0c
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969446"
---
# <a name="support-for-enumeration-commands-wpdbasichardwaredriversample"></a>支持 (WpdBasicHardwareDriverSample) 的枚举命令


示例驱动程序支持三个枚举命令。 这些命令最初由 **WpdObjectEnumerator：:D ispatchmessage** 方法进行处理，该方法反过来会调用相应的命令处理程序。 **DispatchMessage**方法和单独的处理程序都位于*WpdObjectEnum*文件中。

下表中的信息显示每个受支持的属性命令，以及在处理给定命令时 **DispatchMessage** 调用的处理程序的名称。 当应用程序调用 **IPortableDeviceContent** 或 **IEnumPortableDeviceObjectIDs** 接口中的几种方法之一时，将发出这些命令。

| Command                                        | Handler     | 说明                                                                |
|------------------------------------------------|-------------|----------------------------------------------------------------------------|
| WPD \_ 命令 \_ 对象 \_ 枚举 \_ 开始 \_ 查找 | OnStartFind | 创建新的枚举上下文并将其存储在客户端上下文映射中。 |
| WPD \_ 命令 \_ 对象 \_ 枚举 \_ 查找 \_ 下一个  | OnFindNext  | 返回所请求的对象的对象标识符。                     |
| WPD \_ 命令 \_ 对象 \_ 枚举 \_ 结束 \_ 查找   | OnEndFind   | 在枚举结束时执行必要的清理。            |

 

对于示例驱动程序，WPD 命令对象枚举的代码保持不变， \_ \_ \_ \_ 查找 \_ NEXT 和 WPD \_ 命令 \_ 对象 \_ 枚举 \_ 结束 \_ 查找处理程序。 但是，为 WPD \_ 命令 \_ 对象 \_ 枚举 \_ 开始 \_ 查找处理程序修改了部分代码。

## <a name="span-idwpd_command_object_enumeration_start_findspanspan-idwpd_command_object_enumeration_start_findspanwpd_command_object_enumeration_start_find"></a><span id="WPD_COMMAND_OBJECT_ENUMERATION_START_FIND"></span><span id="wpd_command_object_enumeration_start_find"></span>WPD \_ 命令 \_ 对象 \_ 枚举 \_ 开始 \_ 查找


驱动程序调用 **WpdObjectEnumerator：： OnStartFind** 处理程序来响应 WPD \_ 命令 \_ 对象枚举 " \_ \_ 开始查找" \_ 命令。 然后，处理程序将创建、初始化新的枚举上下文并将其添加到客户端上下文映射。 对于示例驱动程序，修改了从**OnStartFind**处理程序中调用的**InitializeEnumerationContext** helper 函数。

对 **OnStartFind** 处理程序和 **InitializeEnumerationContext** helper 函数所做的修改包括删除对不再受支持的对象 (存储、文件夹和文件对象的支持) 并添加对传感器对象的支持。 下面是 **InitalizeEnumerationContext** helper 函数的代码：

```cpp
VOID WpdObjectEnumerator::InitializeEnumerationContext(
    WpdObjectEnumeratorContext* pEnumeratorContext,
    CAtlStringW                 strParentObjectID)
{
    if (pEnumeratorContext == NULL)
    {
        return;
    }

    // Initialize the enumeration context with the parent object identifier
    pEnumeratorContext->m_strParentObjectID = strParentObjectID;

    // Our sample driver has a very simple object structure where we know
    // how many children are under each parent.
    // The eumeration context is initialized below with this information.
    if (strParentObjectID.CompareNoCase(L"") == 0)
    {
        // Clients passing an 'empty' string for the parent are asking for the
        // 'DEVICE' object.  We should return 1 child in this case.
        pEnumeratorContext->m_TotalChildren = 1;
    }
    else if (strParentObjectID.CompareNoCase(WPD_DEVICE_OBJECT_ID) == 0)
    {
        // The device object contains 1 child (the sensor object).
        pEnumeratorContext->m_TotalChildren = 1;
    }
    // If the sensor objects have children, add them here...
    else 
    {
        // The sensor object contains 0 children.
        pEnumeratorContext->m_TotalChildren = 0;
    }
}
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





