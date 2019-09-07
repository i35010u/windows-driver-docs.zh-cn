---
Description: 属性删除
title: 属性删除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9c98d137279b62ebdd8a212fe437495f5d08437
ms.sourcegitcommit: dff3834724bd5204c4a47204540fe8125dd37b20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2019
ms.locfileid: "70750012"
---
# <a name="property-deletion"></a>属性删除


当 Windows 便携设备（WPD）应用程序调用**IPortableDeviceProperties：:D e)** 方法时，此方法将触发对示例驱动程序中的**WpdObjectProperties：： OnDelete**方法的调用。 由于示例驱动程序中不能删除任何对象属性，因此此方法只返回 E\_ACCESSDENIED。

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

 

 




