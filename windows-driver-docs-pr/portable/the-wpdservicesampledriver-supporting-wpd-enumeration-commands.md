---
Description: 对枚举命令 (WpdServiceSampleDriver) 的支持
title: 对枚举命令 (WpdServiceSampleDriver) 的支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ee7271f82d41f60408f886682f1b2484adde82f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370481"
---
# <a name="support-for-enumeration-commands-wpdservicesampledriver"></a>对枚举命令 (WpdServiceSampleDriver) 的支持


示例驱动程序支持三个枚举命令。 这些命令处理最初由**WpdObjectEnumerator::DispatchMessage**方法，反过来，将调用相应的命令处理程序。 **DispatchMessage**方法和单个处理程序全部位于*WpdObjectEnum.cpp*文件。

枚举的每个请求都与枚举上下文中，它标识给定应用程序收到的访问作用域关联。 例如，调用的应用程序**IPortableDevice::Open**具有设备级访问权限，并接收在层次结构，同时调用的应用程序中的所有对象**IPortableDeviceService::Open**具有服务级别的访问权限，并仅接收设备对象、 服务对象和服务对象层次结构中的所有子级。

下表显示每个受支持的枚举命令，以及处理程序的名称， **DispatchMessage**处理给定的命令时调用。 当应用程序调用中的几种方法之一发布这些命令后**IPortableDeviceContent**或**IEnumPortableDeviceObjectIDs**接口。

| Command                                        | 处理程序     | 描述                                                                |
|------------------------------------------------|-------------|----------------------------------------------------------------------------|
| WPD\_命令\_对象\_枚举\_启动\_查找 | OnStartFind | 创建新的枚举上下文并将其存储在客户端上下文映射。 |
| WPD\_命令\_对象\_枚举\_查找\_下一步  | OnFindNext  | 返回所请求的对象的对象标识符。                     |
| WPD\_命令\_对象\_枚举\_最终\_查找   | OnEndFind   | 枚举完成时执行必要的清理。               |

 

示例驱动程序的代码保持不变以 WPD\_命令\_对象\_枚举\_最终\_查找处理程序是与 WpdHellowWorldDriver 示例中找到的代码几乎完全相同。 但是，我们修改了一部分代码为 WPD\_命令\_对象\_枚举\_启动\_查找和 WPD\_对象\_枚举\_查找\_下一个处理程序以支持服务级别的访问权限。

## <a name="span-idwpdcommandobjectenumerationstartfindspanspan-idwpdcommandobjectenumerationstartfindspanwpdcommandobjectenumerationstartfind"></a><span id="WPD_COMMAND_OBJECT_ENUMERATION_START_FIND"></span><span id="wpd_command_object_enumeration_start_find"></span>WPD\_命令\_对象\_枚举\_启动\_查找


驱动程序调用**WpdObjectEnumerator::OnStartFind**处理程序以响应 WPD\_命令\_对象\_枚举\_启动\_查找命令。 处理程序，反过来，创建、 初始化，并将新的枚举上下文添加到客户端上下文映射。

对于示例驱动程序，每个客户端枚举请求与枚举上下文中，相关联，并且此上下文中标识该客户端的访问作用域。

```ManagedCPlusPlus
        if (pEnumeratorContext != NULL)
        {
            ACCESS_SCOPE Scope = m_pDevice->GetAccessScope(pParams);
            m_pDevice->InitializeEnumerationContext(Scope, wszParentID, pEnumeratorContext);

            // Add the enumeration context to the client context map.  This calls AddRef() on pEnumeratorContext
            hr = pContextMap->Add(pEnumeratorContext, strEnumContext);
            CHECK_HR(hr, "Failed to add the enumeration context");
        }
```

有关访问作用域和它的用途的详细信息，请参阅[支持属性命令](the-wpdservicesampledriver-supporting-wpd-property-commands.md)主题。

## <a name="span-idwpdobjectenumerationfindnextspanspan-idwpdobjectenumerationfindnextspanwpdobjectenumerationfindnext"></a><span id="WPD_OBJECT_ENUMERATION_FIND_NEXT"></span><span id="wpd_object_enumeration_find_next"></span>WPD\_对象\_枚举\_查找\_下一步


驱动程序调用**WpdObjectEnumerator::OnFindNext**处理程序以响应 WPD\_命令\_对象\_枚举\_查找\_接下来命令。 该处理程序，反过来，调用**FakeDevice::FindNext**方法，而此方法又调用**FakeContent::FindNext**方法。

下面的代码示例演示**OnFindNext**处理程序调用**FakeDevice::FindNext**方法：

```ManagedCPlusPlus
    if ((hr == S_OK) && (pEnumeratorContext != NULL))
    {
        hr = m_pDevice->FindNext(dwNumObjectsRequested, pEnumeratorContext, pObjectIDCollection, &dwNumObjectsEnumerated);
        CHECK_HR(hr, "Failed to get the next object");
    }
```

下面的代码示例演示**FakeDevice::FindNext**方法调用**FakeContent::FindNext**方法：

```ManagedCPlusPlus
                    FakeContent* pChild = NULL;
                    if (pContent->FindNext(pEnumContext->m_Scope, dwStartIndex, &pChild))
                    {
                        hr = AddStringValueToPropVariantCollection(pObjectIDCollection, pChild->ObjectID);
                        CHECK_HR(hr, "Failed to add object [%ws]", pChild->ObjectID);

                        if (hr == S_OK)
                        {
                            // Update the number of children we are returning for this enumeration call
                            dwStartIndex++;
                            NumObjectsEnumerated++;
                        }
                    }
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[The WpdServiceSampleDriver](the-wpdservicesampledriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





