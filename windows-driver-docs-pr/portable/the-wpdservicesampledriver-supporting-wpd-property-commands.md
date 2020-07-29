---
Description: 通过属性命令使用作用域访问（WpdServiceSampleDriver）
title: 通过属性命令使用作用域访问（WpdServiceSampleDriver）
ms.date: 07/27/2020
ms.localizationpriority: medium
ms.openlocfilehash: e77c4b744bf0c61ede97742fdd55573bd8ffc3e3
ms.sourcegitcommit: 9102e34c3322d8697dbb6f9a1d78879147a73373
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264440"
---
# <a name="using-scope-access-with-property-commands-wpdservicesampledriver"></a>通过属性命令使用作用域访问（WpdServiceSampleDriver）


示例驱动程序支持六个属性命令。 这些命令最初由**WpdObjectProperties：:D ispatchmessage**方法进行处理，该方法反过来会调用相应的命令处理程序。 **DispatchMessage**方法和单独的处理程序都位于*WpdObjectProperties 文件*中。

下表描述了每个受支持的属性命令，以及在处理给定命令时**DispatchMessage**调用的处理程序的名称。

| 命令                                           | Handler                  | 说明                                                                                                   |
|---------------------------------------------------|--------------------------|---------------------------------------------------------------------------------------------------------------|
| \_支持 WPD \_ 命令 \_ 对象 \_ 属性 \_  | OnGetSupportedProperties | 返回给定对象的属性键的数组。                                                       |
| WPD \_ 命令 \_ 对象 \_ 属性 \_ GET             | OnGetPropertyValues      | 返回属性值的集合，这些属性值对应于提供给驱动程序的属性键。 |
| WPD \_ 命令 \_ 对象 \_ 属性 \_ 获取 \_ 全部        | OnGetAllProperties       | 返回给定对象的所有属性值。                                                           |
| WPD \_ 命令 \_ 对象 \_ 属性 \_ 集             | OnSetPropertyValues      | 在设备上设置指定的属性值。                                                              |
| WPD \_ 命令 \_ 对象 \_ 属性 \_ 获取 \_ 属性 | OnGetPropertyAttributes  | 返回给定对象的一个或多个属性的特性集合。                              |
| WPD \_ 命令 \_ 对象 \_ 属性 \_ 删除          | OnDeleteProperties       | 删除由指定的属性键标识的属性。                                        |



## <a name="span-idusing_access_scope_when_setting_and_retrieving_properties_spanspan-idusing_access_scope_when_setting_and_retrieving_properties_spanspan-idusing_access_scope_when_setting_and_retrieving_properties_spanusing-access-scope-when-setting-and-retrieving-properties"></a><span id="Using_Access_Scope_when_Setting_and_Retrieving_Properties_"></span><span id="using_access_scope_when_setting_and_retrieving_properties_"></span><span id="USING_ACCESS_SCOPE_WHEN_SETTING_AND_RETRIEVING_PROPERTIES_"></span>设置和检索属性时使用访问作用域


在 WpdServiceSampleDriver 中的六个属性处理程序中找到的代码与 WpdHelloWorld 驱动程序中的代码几乎完全相同。 例外情况是*服务级别访问作用域*，这是 Windows 7 的新概念。

使用服务级别访问作用域，驱动程序可以将枚举限制为仅限在给定父服务下找到的那些对象。 当驱动程序支持访问作用域并且应用程序调用**IPortableDeviceService：： Open**方法（通过传递给定服务的即插即用标识符）时，应用程序只能访问该服务的设备、给定的服务和子对象。 访问作用域实现可能因驱动程序而异。 WpdServiceSampleDriver 通过使用位掩码定义两个基本级别的作用域、设备级别（限制性较低）和服务级别（限制性更强）来显示这一概念。 下面的代码示例显示了这些级别之间的差异：

```ManagedCPlusPlus
// Access Scope is a bit mask, where each bit enables access to a particular scope
// for example, contacts service is bit 1.   
// The next scope, if any, will be in bit 2
// Full device access is a combination of all, requires all bits to be set
typedef enum tagACCESS_SCOPE
{
    CONTACTS_SERVICE_ACCESS = 1,
    FULL_DEVICE_ACCESS = 0xFFFFFFFF
}ACCESS_SCOPE;
```

当驱动程序用伪对象填充枚举树时，将用适当的范围初始化每个内容对象的**FakeContent：： RequiredScope**成员。 例如，可以将联系人对象初始化为仅限联系服务级别访问。

```ManagedCPlusPlus
class FakeContactContent : public FakeContent
{
public:
    FakeContactContent()
    {
        Format              = WPD_OBJECT_FORMAT_ABSTRACT_CONTACT;
        ContentType         = WPD_CONTENT_TYPE_CONTACT;
        RequiredScope       = CONTACTS_SERVICE_ACCESS;
    ...
    }
  ...
}
```

以下来自**OnGetSupportedProperties**处理程序函数的代码示例演示如何使用访问作用域来确保返回了正确的属性键：

```ManagedCPlusPlus
    // Add supported property keys for the specified object to the collection
    if (hr == S_OK)
    {
        ACCESS_SCOPE Scope = m_pDevice->GetAccessScope(pParams);
        hr = m_pDevice->GetSupportedProperties(Scope, wszObjectID, pKeys);
        CHECK_HR(hr, "Failed to add supported property keys for object '%ws'", wszObjectID);
    }
```

上一示例中的代码调用**FakeDevice：： GetSupportedProperties**方法，该方法在文件*FakeDevice*中找到。

```ManagedCPlusPlus
HRESULT FakeDevice::GetSupportedProperties(
            ACCESS_SCOPE                  Scope,
    __in    LPCWSTR                       wszObjectID,
    __out   IPortableDeviceKeyCollection* pKeys)
{
    HRESULT      hr       = S_OK;
    FakeContent* pContent = NULL;

    if ((wszObjectID == NULL) ||
        (pKeys       == NULL))
    {
        hr = E_POINTER;
        CHECK_HR(hr, "Cannot have NULL parameter");
        return hr;
    }

    hr = GetContent(Scope, wszObjectID, &pContent);
    CHECK_HR(hr, "Failed to get content '%ws'", wszObjectID);

    if (hr == S_OK)
    {
        hr = pContent->GetSupportedProperties(pKeys);
        CHECK_HR(hr, "Failed to get supported properties for '%ws'", wszObjectID);
    }

    return hr;
}
```

此方法首先尝试检索给定对象的内容。 然后，如果该方法可以检索内容，则检索请求的属性键。**FakeContent：： GetContent**检查作用域，并在应用程序提供限制性较低的访问范围（如设备范围访问）时拒绝访问。

```ManagedCPlusPlus
HRESULT FakeContent::GetContent(
            ACCESS_SCOPE   Scope,
    __in    LPCWSTR        wszObjectID,
    __out   FakeContent**  ppContent)
{
    HRESULT hr = HRESULT_FROM_WIN32(ERROR_NOT_FOUND);

    if (CanAccess(Scope))
    {
    // Within access scope, proceed . . .
    }
    else
    {
        hr = E_ACCESSDENIED;
        CHECK_HR(hr, "GetContent: '%ws' was found but falls outside scope", wszObjectID);
    }

    return hr;
} 

bool FakeContent::CanAccess(
    ACCESS_SCOPE Scope)
{
    return ((Scope & RequiredScope) == RequiredScope);
}
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)









