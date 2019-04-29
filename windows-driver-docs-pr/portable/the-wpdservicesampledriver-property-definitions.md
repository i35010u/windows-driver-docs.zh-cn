---
Description: 定义服务属性
title: 定义服务属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf751e8e7964db8eaa19a7d680561350d305521c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370506"
---
# <a name="defining-the-service-properties"></a>定义服务属性


WPD 属性是对象说明的元数据。 本部分介绍的示例驱动程序支持的属性。 联系人服务对象支持 14 属性;而且单个联系人对象还支持 14 属性。 某些对象属性所需的驱动程序的功能，例如 WPD\_对象\_ID 和 WPD\_对象\_的永久\_UNIQUE\_id。 其他属性提供信息来描述对象，如 WPD\_联系\_显示\_联系人对象的名称。

WDK WPD 驱动程序开发人员对于包含多种工具。 这些工具之一*WpdInfo.exe*，使开发人员若要检查的对象和由给定的驱动程序公开的属性。 下图的*WpdInfo.exe*工具显示的属性驱动程序中的联系人服务对象支持：

![wpd 信息工具](images/wpd_info_service_root.png)

在上图中，最左边的列的顶部窗格中列出的驱动程序支持的对象。 中心窗格中列出了 14 联系人服务对象的驱动程序支持的属性。 在此窗格中的第一列列出属性名称、 第二列列出了该属性的值和第三个列，列出的类型，依此类推。 下部窗格显示了返回的事件的驱动程序支持的信息。

下图的*WpdInfo.exe*工具显示的属性的第一个联系人对象支持。

![wpd 信息工具](images/wpd_info_service_contact1.png)

此对象支持 14 属性。 前八个属性是常规 WPD 对象属性。 前六个属性是特定于联系人的 （名称、 移动电话号码、 电子邮件地址等）。

WPD，在由 PROPERTYKEY 数据结构表示属性。 此结构由两部分组成： 一个全局唯一标识符 (GUID) 和一个 dword 值。 GUID 会识别属性类别和 DWORD 标识该类别中的特定属性。 PROPERTYKEY 结构的详细信息，请参阅[PROPERTYKEYs 和 WPD 中的 Guid](propertykeys-and-guids-in-windows-portable-devices.md)。

在示例驱动程序，支持的联系人属性定义中的数组**PropertyAttributeInfo**结构。 此结构具有以下格式：

```cpp
typedef struct tagPropertyAttributeInfo
{
    const PROPERTYKEY*                pKey;
    VARTYPE                           Vartype;
    FakeDevicePropertyAttributesType  AttributesType;
    const LPWSTR                      wszName;
} PropertyAttributeInfo;
```

*FakeContactContent.cpp*文件定义的支持联系人的属性数组：

```cpp
const PropertyAttributeInfo g_SupportedContactProperties[] =
{
    {&WPD_OBJECT_ID,                             VT_LPWSTR, UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast,  NULL}, 
    {&WPD_OBJECT_PERSISTENT_UNIQUE_ID,           VT_LPWSTR, UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast,  NULL}, 
    {&WPD_OBJECT_PARENT_ID,                      VT_LPWSTR, UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast,  NULL}, 
    {&WPD_OBJECT_NAME,                           VT_LPWSTR, UnspecifiedForm_CanRead_CanWrite_CannotDelete_Fast,     NULL}, 
    {&WPD_OBJECT_FORMAT,                         VT_CLSID,  UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast,  NULL}, 
    {&WPD_OBJECT_CONTENT_TYPE,                   VT_CLSID,  UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast,  NULL}, 
    {&WPD_OBJECT_CAN_DELETE,                     VT_BOOL,   UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast,  NULL}, 
    {&WPD_OBJECT_CONTAINER_FUNCTIONAL_OBJECT_ID, VT_LPWSTR, UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast,  NULL}, 
    {&WPD_CONTACT_DISPLAY_NAME,                  VT_LPWSTR, UnspecifiedForm_CanRead_CanWrite_CannotDelete_Fast,     NULL},
    {&WPD_CONTACT_MOBILE_PHONE,                  VT_LPWSTR, UnspecifiedForm_CanRead_CanWrite_CannotDelete_Fast,     NULL},
    {&WPD_CONTACT_PRIMARY_EMAIL_ADDRESS,         VT_LPWSTR, UnspecifiedForm_CanRead_CanWrite_CannotDelete_Fast,     NULL},
    {&WPD_CONTACT_PRIMARY_PHONE,                 VT_LPWSTR, UnspecifiedForm_CanRead_CanWrite_CannotDelete_Fast,     NULL},
    {&WPD_CONTACT_PERSONAL_FULL_POSTAL_ADDRESS,  VT_LPWSTR, UnspecifiedForm_CanRead_CanWrite_CannotDelete_Fast,     NULL},
    {&MyContactVersionIdentifier,                VT_UI4,    UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast,  L"ContactVersionIdentifier"},
};
```

这些属性的初始化*FakeContactsServiceContent.cpp*中的模块**InitializeContent**方法，如以下示例所示：

```cpp
        if (pContact)
        {
            pContact->Name.Format(L"Contact%d", *pdwLastObjectID);
            pContact->ParentID                    = ObjectID;
            pContact->ContainerFunctionalObjectID = ObjectID;
            pContact->ObjectID.Format(L"%d", *pdwLastObjectID);
            pContact->PersistentUniqueID.Format(L"PersistentUniqueID_%ws", pContact->ObjectID);
            pContact->ParentPersistentUniqueID    = PersistentUniqueID;
            pContact->RequiredScope               = CONTACTS_SERVICE_ACCESS;

            pContact->DisplayName.Format(L"Surname%d, FirstName%d", dwContactIndex, dwContactIndex);
            pContact->MobilePhoneNumber           = L"(425) 555 0821";
            pContact->PrimaryPhoneNumber          = L"(425) 556 6010";
            pContact->PrimaryEmail.Format(L"FirstName%d@Company%d.com", dwContactIndex, dwContactIndex);
            pContact->PersonalFullPostalAddress.Format(L"One Microsoft Way, Redmond, WA 98052, USA");

            m_Children.Add(pContact);
        }
```

*FakeContactsServiceContent.cpp*文件定义了受支持的服务属性的数组：

```cpp
const PropertyAttributeInfo g_SupportedServiceProperties[] =
{
    {&WPD_OBJECT_ID,                                VT_LPWSTR,          UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, NULL},
    {&WPD_OBJECT_PERSISTENT_UNIQUE_ID,              VT_LPWSTR,          UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, NULL},
    {&WPD_OBJECT_PARENT_ID,                         VT_LPWSTR,          UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, NULL},
    {&WPD_OBJECT_NAME,                              VT_LPWSTR,          UnspecifiedForm_CanRead_CanWrite_CannotDelete_Fast,    NULL},
    {&WPD_OBJECT_FORMAT,                            VT_CLSID,           UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, NULL},
    {&WPD_OBJECT_CONTENT_TYPE,                      VT_CLSID,           UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, NULL},
    {&WPD_OBJECT_CAN_DELETE,                        VT_BOOL,            UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, NULL},
    {&WPD_OBJECT_CONTAINER_FUNCTIONAL_OBJECT_ID,    VT_LPWSTR,          UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, NULL},
    {&WPD_FUNCTIONAL_OBJECT_CATEGORY,               VT_CLSID,           UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, NULL},
    {&WPD_SERVICE_VERSION,                          VT_LPWSTR,          UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, NULL},
    {&PKEY_Services_ServiceDisplayName,             VT_LPWSTR,          UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, L"DisplayName"},
    {&PKEY_FullEnumSyncSvc_SyncFormat,              VT_CLSID,           UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, L"FullEnumSyncFormat"},
    {&PKEY_Services_ServiceIcon,                    VT_VECTOR | VT_UI1, UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, L"ServiceIcon"},
    {&PKEY_FullEnumSyncSvc_VersionProps,            VT_VECTOR | VT_UI1, UnspecifiedForm_CanRead_CannotWrite_CannotDelete_Fast, L"FullEnumVersionProps"}
};
```

设置服务属性**GetValue**同一模块中找到的方法。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[The WpdServiceSampleDriverSample](the-wpdservicesampledriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





