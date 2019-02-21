---
Description: Property Deletion
title: 属性删除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9c98d137279b62ebdd8a212fe437495f5d08437
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520074"
---
# <a name="property-deletion"></a>属性删除


在 Windows 便携式设备 (WPD) 应用程序调用**IPortableDeviceProperties::Delete**方法，此方法，反过来，触发调用**WpdObjectProperties::OnDelete**中的方法示例驱动程序。 此方法可以删除任何示例驱动程序中的对象属性，因为只需返回 E\_ACCESSDENIED。

```ManagedCPlusPlus
HRESULT WpdObjectProperties::OnDeleteProperties(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT hr = E_ACCESSDENIED;

    UNREFERENCED_PARAMETER(pParams);
    UNREFERENCED_PARAMETER(pResults);

    // This driver has no properties which can be deleted.

    return hr;
}
```

 

 




