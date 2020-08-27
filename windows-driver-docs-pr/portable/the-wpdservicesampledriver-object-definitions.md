---
description: 定义服务对象
title: 定义服务对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ff3a18ac4c185d4f21ccf1030a1268ab66461cc
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969476"
---
# <a name="defining-the-service-objects"></a>定义服务对象


在 WPD 中，设备上的逻辑实体称为对象。 对象可以表示设备的信息性部分或功能部分。 任何对象都具有一个或多个属性。 可以将属性视为对象描述元数据。 例如，示例驱动程序上的 "联系人" 服务对象支持名称属性，该属性指定服务的友好名称。

WpdHelloWorldDriver 支持下表中显示的对象。

| 对象  | 说明                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| 设备  | 包含描述属性（如固件版本、模型和友好名称）的根对象。 |
| 存储 | 一个对象，该对象公开存储容量等属性、文件系统类型和可用字节数。         |
| 文件夹  | 公开属性（如文件夹名称）的对象。                                                             |
| 文件    | 一个对象，该对象公开文件名称和实际文件内容等属性。                                      |

 

与 WpdHelloWorldDriver 类似，WpdServiceSampleDriver 继续支持存储对象。 但是，由于该示例不支持文件夹或文件 (为简单起见) ，因此删除了这些对象并将其替换为对应于联系人的单个对象。 下表列出了新的驱动程序支持的对象。

| 对象   | 说明                                                                                                            |
|----------|------------------------------------------------------------------------------------------------------------------------|
| 设备   | 包含描述属性（如固件版本、模型和友好名称）的根对象。      |
| 存储  | 一个对象，该对象公开存储容量等属性、文件系统类型和可用字节数。              |
| 联系人 | 一个服务对象，其中包含对象标识符等属性、永久性唯一 ID (PUID) 、名称等。 |

 

在 WPD 中，对象由字符串标识。 设备对象的字符串标识符是在 *Portabledevice* 头文件中定义的：

```cpp
#define WPD_DEVICE_OBJECT_ID  L"DEVICE"
```

存储对象的字符串标识符是在 *FakeStorage* 头文件中定义的：

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

联系人对象的字符串标识符是在 *FakeContactsServiceContent* 头文件中定义的：

```cpp
#define CONTACTS_SERVICE_OBJECT_ID                        L"789DEF"
#define CONTACTS_SERVICE_PERSISTENT_UNIQUE_ID             L"{95A95EA9-9904-430E-8FF6-70851F208478}"
#define CONTACTS_SERVICE_OBJECT_NAME_VALUE                L"Contacts"
#define CONTACTS_SERVICE_HUMAN_READABLE_NAME              L"Hello World Phone Contacts"
#define CONTACTS_SERVICE_PREFERRED_FORMAT                 WPD_OBJECT_FORMAT_ABSTRACT_CONTACT
#define CONTACTS_SERVICE_VERSION                          L"1.0"

#define NUM_CONTACT_OBJECTS                               10
```

这些对象标识符常量会传递到源模块中处理 (*FakeDevice*) 的函数对象检索的方法。 下面的 **FakeDevice：： GetFunctionalObjects** 方法摘录演示了如何使用 CONTACTS \_ 服务 \_ 对象 \_ ID 生成支持的功能对象集合， (服务 \_ 联系人在 *ContactsDeviceService* 头文件中定义，并表示服务对象) 的功能类别：

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

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdServiceSampleDriver 示例](the-wpdservicesampledriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





