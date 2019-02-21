---
Description: Object Enumeration
title: 对象枚举
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50cde952ffda2599aff596fc54510cadcd353d91
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555367"
---
# <a name="object-enumeration"></a>对象枚举


*WpdObjectEnum.cpp*并*WpdObjectEnum.h*文件包含枚举设备支持的对象的成员函数。

当基于 Windows 的应用程序调用**IPortableDeviceContent::EnumObject**或的两种方法之一**IEnumPortableDeviceObjectIDs**接口，此调用，反过来，触发一个三个命令中的处理程序**WpdObjectEnumerator**类。 下表列出了应用程序的方法的映射**WpdObjectEnumerator**驱动程序的方法。

|                                           |                                         |
|-------------------------------------------|-----------------------------------------|
| **IPortableDeviceContent 方法**         | **WpdObjectEnumerator 命令处理程序** |
| **IPortableDeviceContent::EnumObjects**   | **OnStartFind**                         |
| **IEnumPortableDeviceObjectIDs::Next**    | **OnFindNext**                          |
| **IEnumPortableDeviceObjectIDs::Release** | **OnEndFind**                           |

 

**WpdObjectEnumerator**由调用命令处理程序**WpdObjectEnumerator::DispatchWpdMessage**方法。 以下内容摘自示例驱动程序包含的代码**WpdObjectEnumerator::DispatchWpdMessage。**

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

 

 




