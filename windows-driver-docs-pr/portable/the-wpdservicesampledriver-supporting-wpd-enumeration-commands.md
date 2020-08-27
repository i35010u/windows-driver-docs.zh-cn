---
description: 支持 (WpdServiceSampleDriver) 的枚举命令
title: 支持 (WpdServiceSampleDriver) 的枚举命令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0aaabc8351844d8ce6488ee5c71aa5fb56ca424e
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969540"
---
# <a name="support-for-enumeration-commands-wpdservicesampledriver"></a>支持 (WpdServiceSampleDriver) 的枚举命令


示例驱动程序支持三个枚举命令。 这些命令最初由 **WpdObjectEnumerator：:D ispatchmessage** 方法进行处理，该方法反过来会调用相应的命令处理程序。 **DispatchMessage**方法和单独的处理程序都位于*WpdObjectEnum*文件中。

每个枚举请求与一个枚举上下文相关联，该枚举上下文标识给定应用程序接收的访问范围。 例如，调用 **IPortableDevice：： open** 的应用程序具有设备范围的访问权限并接收层次结构中的所有对象，而调用 **IPortableDeviceService：： open** 的应用程序具有服务级别访问权限，并且仅接收服务对象层次结构中的设备对象、服务对象和所有子级。

下表显示了每个受支持的枚举命令，以及在处理给定命令时 **DispatchMessage** 调用的处理程序的名称。 当应用程序调用 **IPortableDeviceContent** 或 **IEnumPortableDeviceObjectIDs** 接口中的几种方法之一时，将发出这些命令。

| Command                                        | Handler     | 说明                                                                |
|------------------------------------------------|-------------|----------------------------------------------------------------------------|
| WPD \_ 命令 \_ 对象 \_ 枚举 \_ 开始 \_ 查找 | OnStartFind | 创建新的枚举上下文并将其存储在客户端上下文映射中。 |
| WPD \_ 命令 \_ 对象 \_ 枚举 \_ 查找 \_ 下一个  | OnFindNext  | 返回所请求的对象的对象标识符。                     |
| WPD \_ 命令 \_ 对象 \_ 枚举 \_ 结束 \_ 查找   | OnEndFind   | 枚举完成后，执行必要的清理。               |

 

对于示例驱动程序，WPD \_ 命令 \_ 对象 \_ 枚举 \_ 结束查找处理程序的完整代码与 \_ WpdHellowWorldDriver 示例中的代码几乎完全相同。 但是，我们修改了 WPD \_ 命令 \_ 对象 \_ 枚举 \_ 开始 \_ 查找和 WPD 对象枚举的部分代码， \_ \_ \_ \_ 以支持服务级别访问。

## <a name="span-idwpd_command_object_enumeration_start_findspanspan-idwpd_command_object_enumeration_start_findspanwpd_command_object_enumeration_start_find"></a><span id="WPD_COMMAND_OBJECT_ENUMERATION_START_FIND"></span><span id="wpd_command_object_enumeration_start_find"></span>WPD \_ 命令 \_ 对象 \_ 枚举 \_ 开始 \_ 查找


驱动程序调用 **WpdObjectEnumerator：： OnStartFind** 处理程序来响应 WPD \_ 命令 \_ 对象枚举 " \_ \_ 开始查找" \_ 命令。 然后，处理程序将创建、初始化新的枚举上下文并将其添加到客户端上下文映射。

对于示例驱动程序，每个客户端枚举请求都与一个枚举上下文相关联，并且此上下文标识该客户端的访问作用域。

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

有关访问作用域及其用途的详细信息，请参阅 [支持属性命令](the-wpdservicesampledriver-supporting-wpd-property-commands.md) 主题。

## <a name="span-idwpd_object_enumeration_find_nextspanspan-idwpd_object_enumeration_find_nextspanwpd_object_enumeration_find_next"></a><span id="WPD_OBJECT_ENUMERATION_FIND_NEXT"></span><span id="wpd_object_enumeration_find_next"></span>WPD \_ 对象 \_ 枚举 \_ 查找 \_ 下一个


驱动程序调用 **WpdObjectEnumerator：： OnFindNext** 处理程序来响应 WPD \_ 命令 \_ 对象 \_ 枚举 \_ 查找 \_ 下一个命令。 然后，处理程序将调用 **FakeDevice：： findnext** 方法，而此方法又调用 **FakeContent：： findnext** 方法。

下面的代码示例演示了调用**FakeDevice：： FindNext**方法的**OnFindNext**处理程序：

```ManagedCPlusPlus
    if ((hr == S_OK) && (pEnumeratorContext != NULL))
    {
        hr = m_pDevice->FindNext(dwNumObjectsRequested, pEnumeratorContext, pObjectIDCollection, &dwNumObjectsEnumerated);
        CHECK_HR(hr, "Failed to get the next object");
    }
```

下面的代码示例演示了调用**FakeContent：： findnext**方法的**FakeDevice：： findnext**方法：

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

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdServiceSampleDriver](the-wpdservicesampledriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





