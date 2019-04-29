---
Description: 对枚举命令 (WpdBasicHardwareDriverSample) 的支持
title: 对枚举命令 (WpdBasicHardwareDriverSample) 的支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5074671e507c94df29c2009e1f0fea38b13fd81
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387299"
---
# <a name="support-for-enumeration-commands-wpdbasichardwaredriversample"></a>对枚举命令 (WpdBasicHardwareDriverSample) 的支持


示例驱动程序支持三个枚举命令。 这些命令处理最初由**WpdObjectEnumerator::DispatchMessage**方法，反过来，将调用相应的命令处理程序。 **DispatchMessage**方法和单个处理程序全部位于*WpdObjectEnum.cpp*文件。

下表中的信息显示每个受支持的属性的命令，以及处理程序的名称， **DispatchMessage**处理给定的命令时调用。 当应用程序调用中的几种方法之一发布这些命令后**IPortableDeviceContent**或**IEnumPortableDeviceObjectIDs**接口。

| Command                                        | 处理程序     | 描述                                                                |
|------------------------------------------------|-------------|----------------------------------------------------------------------------|
| WPD\_命令\_对象\_枚举\_启动\_查找 | OnStartFind | 创建新的枚举上下文并将其存储在客户端上下文映射。 |
| WPD\_命令\_对象\_枚举\_查找\_下一步  | OnFindNext  | 返回所请求的对象的对象标识符。                     |
| WPD\_命令\_对象\_枚举\_最终\_查找   | OnEndFind   | 执行必要的枚举结束时清除。            |

 

示例驱动程序，该代码将保持不变的 WPD\_命令\_对象\_枚举\_查找\_下一步，WPD\_命令\_对象\_枚举\_最终\_查找处理程序。 但是，该代码部分已修改为 WPD\_命令\_对象\_枚举\_启动\_查找处理程序。

## <a name="span-idwpdcommandobjectenumerationstartfindspanspan-idwpdcommandobjectenumerationstartfindspanwpdcommandobjectenumerationstartfind"></a><span id="WPD_COMMAND_OBJECT_ENUMERATION_START_FIND"></span><span id="wpd_command_object_enumeration_start_find"></span>WPD\_命令\_对象\_枚举\_启动\_查找


驱动程序调用**WpdObjectEnumerator::OnStartFind**处理程序以响应 WPD\_命令\_对象\_枚举\_启动\_查找命令。 处理程序，反过来，创建、 初始化，并将新的枚举上下文添加到客户端上下文映射。 对于示例驱动程序， **InitializeEnumerationContext**调用中的帮助程序函数**OnStartFind**处理程序的修改。

对同时修改**OnStartFind**处理程序和**InitializeEnumerationContext**帮助程序函数包括删除针对不再支持的对象的支持 （存储、 文件夹和的文件对象） 并添加对传感器对象的支持。 以下是有关代码**InitalizeEnumerationContext**帮助程序函数：

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

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





