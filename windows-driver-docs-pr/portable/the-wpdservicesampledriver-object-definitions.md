---
Description: 定义服务对象
title: 定义服务对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 965836fb50baeb873f8f5edee9be2c618fc5cdcd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370631"
---
# <a name="defining-the-service-objects"></a>定义服务对象


WPD，在设备上的逻辑实体都称为对象。 对象可以表示设备的信息性消息或功能的部分。 任何对象都具有一个或多个属性。 您可以将属性作为对象说明元数据。 例如，联系人服务对象上的示例驱动程序支持指定服务的友好名称的名称属性。

WpdHelloWorldDriver 支持下表中所示的对象。

| Object  | 描述                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| 设备  | 包含描述性属性，如固件版本、 型号和友好名称的根对象。 |
| 存储 | 一个对象，公开属性，如存储容量、 文件系统类型和可用的字节数。         |
| 文件夹  | 一个对象，公开属性，如文件夹名称。                                                             |
| 文件    | 一个对象，公开属性，如文件名称和实际的文件内容。                                      |

 

类似于 WpdHelloWorldDriver，WpdServiceSampleDriver 继续以支持存储对象。 但是，因为该示例不支持文件夹或文件 （为简单起见），我们删除这些对象，并且它们替换为对应于联系人的单个对象。 下表列出了新的驱动程序支持的对象。

| Object   | 描述                                                                                                            |
|----------|------------------------------------------------------------------------------------------------------------------------|
| 设备   | 包含描述性属性，如固件版本、 型号和友好名称的根对象。      |
| 存储  | 一个对象，公开属性，如存储容量、 文件系统类型和可用的字节数。              |
| 联系人 | 包含属性，如对象标识符、 永久唯一 ID (PUID)、 名称和等等的服务对象。 |

 

在 WPD，对象标识的字符串。 中定义的设备对象的字符串标识符*Portabledevice.h*标头文件：

```cpp
#define WPD_DEVICE_OBJECT_ID  L"DEVICE"
```

在中定义的存储对象的字符串标识符*FakeStorage.h*标头文件：

```cpp
#define STORAGE_OBJECT_ID                                 L"123ABC"
#define STORAGE_CAPACITY_VALUE                            1024 * 1024
#define STORAGE_FREE_SPACE_IN_BYTES_VALUE                 STORAGE_CAPACITY_VALUE
#define STORAGE_SERIAL_NUMBER_VALUE                       L"98765432109876-54321098765432"
#define STORAGE_OBJECT_NAME_VALUE                         L"Internal Memory"
#define STORAGE_FILE_SYSTEM_TYPE_VALUE                    L"FAT32"
#define STORAGE_DESCRIPTION_VALUE                         L"Phone Memory Storage System"
#define STORAGE_CONTAINER_FUNCTIONAL_OBJECT_ID            WPD_DEVICE_OBJECT_ID
#define STORAGE_TYPE                                      WPD_STORAGE_TYPE_FIXED_ROM
```

在中定义的联系人对象的字符串标识符*FakeContactsServiceContent.h*标头文件：

```cpp
#define CONTACTS_SERVICE_OBJECT_ID                        L"789DEF"
#define CONTACTS_SERVICE_PERSISTENT_UNIQUE_ID             L"{95A95EA9-9904-430E-8FF6-70851F208478}"
#define CONTACTS_SERVICE_OBJECT_NAME_VALUE                L"Contacts"
#define CONTACTS_SERVICE_HUMAN_READABLE_NAME              L"Hello World Phone Contacts"
#define CONTACTS_SERVICE_PREFERRED_FORMAT                 WPD_OBJECT_FORMAT_ABSTRACT_CONTACT
#define CONTACTS_SERVICE_VERSION                          L"1.0"

#define NUM_CONTACT_OBJECTS                               10
```

这些对象标识符常量传递给处理功能对象检索的源模块中的方法 (*FakeDevice.cpp*)。 中的以下节选**FakeDevice::GetFunctionalObjects**方法演示了如何使用联系人\_服务\_对象\_支持功能的对象 （ID 生成的集合服务\_中定义联系人*ContactsDeviceService.h*标头文件，代表功能类别的服务对象):

```cpp
    // Add CONTACTS_SERVICE_OBJECT_ID to the functional object identifiers collection
    if (hr == S_OK)
    {
        if ((guidFunctionalCategory  == SERVICE_Contacts) ||
            (guidFunctionalCategory  == WPD_FUNCTIONAL_CATEGORY_ALL))
        {
            pv.vt       = VT_LPWSTR;
            pv.pwszVal  = CONTACTS_SERVICE_OBJECT_ID;
            hr = pFunctionalObjects->Add(&pv);
            CHECK_HR(hr, "Failed to add contacts service object ID");
        }
    }
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdServiceSampleDriver 示例](the-wpdservicesampledriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





