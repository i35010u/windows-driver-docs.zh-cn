---
description: 属性删除
title: 属性删除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7eadc16240814d461d258ebf7d163ccfa980cb29
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969584"
---
# <a name="property-deletion"></a>属性删除


当 (WPD) 应用程序的 Windows 便携式设备调用 **IPortableDeviceProperties：:D e) ** 方法时，此方法反过来会触发对示例驱动程序中的 **WpdObjectProperties：： OnDelete** 方法的调用。 由于示例驱动程序中不能删除任何对象属性，因此此方法只返回 E \_ ACCESSDENIED。

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

 

 




