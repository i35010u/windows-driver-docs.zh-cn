---
Description: 对属性命令 (WpdBasicHardwareDriverSample) 的支持
title: 对属性命令 (WpdBasicHardwareDriverSample) 的支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd89ce3ce9653958bf77bc3c2c0d8d6f45c897ad
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349690"
---
# <a name="support-for-property-commands-wpdbasichardwaredriversample"></a>对属性命令 (WpdBasicHardwareDriverSample) 的支持


示例驱动程序支持六个属性命令。 这些命令处理最初由**WpdObjectProperties::DispatchMessage**方法，反过来，将调用相应的命令处理程序。 **DispatchMessage**方法和单个处理程序全部位于*WpdObjectProperties.cpp 文件*。

下表描述了每个受支持的属性的命令，以及处理程序的名称， **DispatchMessage**处理给定的命令时调用。

| Command                                           | 处理程序                  | 描述                                                                                                   |
|---------------------------------------------------|--------------------------|---------------------------------------------------------------------------------------------------------------|
| WPD\_命令\_对象\_属性\_获取\_支持  | OnGetSupportedProperties | 返回给定对象的属性键的数组。                                                       |
| WPD\_命令\_对象\_属性\_获取             | OnGetPropertyValues      | 返回提供给该驱动程序的属性键相对应的属性值的集合。 |
| WPD\_命令\_对象\_属性\_获取\_所有        | OnGetAllProperties       | 返回给定对象的所有属性值。                                                           |
| WPD\_命令\_对象\_属性\_设置             | OnSetPropertyValues      | 在设备上设置指定的属性值。                                                              |
| WPD\_命令\_对象\_属性\_获取\_属性 | OnGetPropertyAttributes  | 返回给定对象上的一个或多个属性的特性的集合。                              |
| WPD\_命令\_对象\_属性\_删除          | OnDeleteProperties       | 删除由给定的属性键标识的属性。                                        |



## <a name="span-idusingaccessscopewhensettingandretrievingpropertiesspanspan-idusingaccessscopewhensettingandretrievingpropertiesspanspan-idusingaccessscopewhensettingandretrievingpropertiesspanusing-access-scope-when-setting-and-retrieving-properties"></a><span id="Using_Access_Scope_when_Setting_and_Retrieving_Properties_"></span><span id="using_access_scope_when_setting_and_retrieving_properties_"></span><span id="USING_ACCESS_SCOPE_WHEN_SETTING_AND_RETRIEVING_PROPERTIES_"></span>使用访问作用域时设置和检索属性


在中 WpdServiceSampleDriver 的六个属性处理程序中找到的代码是 WpdHelloWorld 驱动程序中找到的代码几乎完全相同。 例外情况是*服务级别的访问作用域*，这是适用于 Windows 7 的新概念。

服务级别的访问作用域启用驱动程序来限制为仅在给定的父服务下找到这些对象的枚举。 当驱动程序支持访问作用域和应用程序调用**IPortableDeviceService::Open**方法 （通过传递给定服务的即插标识符），该应用程序只能访问该设备，在给定的服务和该服务的子对象。 访问作用域实现可能会有所不同，具体取决于驱动程序。 WpdServiceSampleDriver 显示通过使用一个位掩码来定义两个基本级别的作用域，设备级别 （限制较少），这一概念和服务级别 （限制性更强）。 下面的代码示例显示了这些级别之间的差异：

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

当驱动程序使用填充虚设对象枚举树**FakeContent::RequiredScope**内容的每个对象的成员初始化与相应的作用域。 例如，联系人对象可以经过初始化才能被限制为仅联系人服务级别的访问。

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

下面的代码示例摘自**OnGetSupportedProperties**处理程序函数演示如何访问作用域已使用以确保返回了正确的属性键：

```ManagedCPlusPlus
    // Add supported property keys for the specified object to the collection
    if (hr == S_OK)
    {
        ACCESS_SCOPE Scope = m_pDevice->GetAccessScope(pParams);
        hr = m_pDevice->GetSupportedProperties(Scope, wszObjectID, pKeys);
        CHECK_HR(hr, "Failed to add supported property keys for object '%ws'", wszObjectID);
    }
```

先前的示例调用中的代码**FakeDevice::GetSupportedProperties**方法，在文件中找到*FakeDevice.cpp*。

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

此方法首先尝试检索给定对象的内容。 然后，如果该方法是能够检索的内容，它将检索请求的属性键。**FakeContent::GetContent**检查作用域，并拒绝访问，如果应用程序提供了限制性较弱的访问作用域 （如设备级访问权限）。

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

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)









