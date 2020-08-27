---
description: 对象枚举
title: 对象枚举
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3119d586e9b8e677a8d08e08c5720de4979f00d7
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969586"
---
# <a name="object-enumeration"></a>对象枚举


*WpdObjectEnum*和*WpdObjectEnum*文件包含枚举设备支持的对象的成员函数。

当基于 Windows 的应用程序调用**IPortableDeviceContent：： EnumObject** 或 **IEnumPortableDeviceObjectIDs** 接口的两种方法之一时，此调用反过来会触发 **WpdObjectEnumerator** 类中三个命令处理程序之一。 下表标识了应用程序方法到 **WpdObjectEnumerator** 驱动程序方法的映射。

IPortableDeviceContent 方法 * * * * *： **WpdObjectEnumerator 命令处理程序**

IPortableDeviceContent：： EnumObjects * * * *： **OnStartFind**

IEnumPortableDeviceObjectIDs：： Next * * * *： **OnFindNext**

IEnumPortableDeviceObjectIDs：： Release * * * *： **OnEndFind**


 

**WpdObjectEnumerator**命令处理程序由**WpdObjectEnumerator：:D ispatchwpdmessage**方法调用。 以下摘自示例驱动程序的代码包含**WpdObjectEnumerator：:D ispatchwpdmessage**的代码。

```ManagedCPlusPlus
HRESULT WpdObjectEnumerator::DispatchWpdMessage(const PROPERTYKEY&     Command,
                                                IPortableDeviceValues* pParams,
                                                IPortableDeviceValues* pResults)
{
    HRESULT hr = S_OK;

    if (hr == S_OK)
    {
        if (Command.fmtid != WPD_CATEGORY_OBJECT_ENUMERATION)
        {
            hr = E_INVALIDARG;
            CHECK_HR(hr, "This object does not support this command category %ws",CComBSTR(Command.fmtid));
        }
    }

    if (hr == S_OK)
    {
        if (Command.pid == WPD_COMMAND_OBJECT_ENUMERATION_START_FIND.pid)
        {
            hr = OnStartFind(pParams, pResults);
            CHECK_HR(hr, "Failed to begin enumeration");
        }
        else if (Command.pid == WPD_COMMAND_OBJECT_ENUMERATION_FIND_NEXT.pid)
        {
            hr = OnFindNext(pParams, pResults);
            if(FAILED(hr))
            {
                CHECK_HR(hr, "Failed to find next object");
            }
        }
        else if (Command.pid == WPD_COMMAND_OBJECT_ENUMERATION_END_FIND.pid)
        {
            hr = OnEndFind(pParams, pResults);
            CHECK_HR(hr, "Failed to end enumeration");
        }
        else
        {
            hr = E_NOTIMPL;
            CHECK_HR(hr, "This object does not support this command id %d", Command.pid);
        }
    }

    return hr;
}
```

 

 




