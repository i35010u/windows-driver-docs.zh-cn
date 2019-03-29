---
title: 更改 WIA 项树状结构
description: 更改 WIA 项树状结构
ms.assetid: fa6c9d25-4435-43ee-a262-9e267b9a0a69
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f7fd29bf0cc83d36923e35c094a7218f5f88b89
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568442"
---
# <a name="changing-the-wia-item-tree-structure"></a>更改 WIA 项树状结构





WIA 微型驱动程序能够在任何时候更改 WIA 项树状结构。 微型驱动程序对 WIA 项树进行了更改，微型驱动程序必须通知 WIA 服务。 WIA 服务然后会通知所有连接的 WIA 应用程序。 收到通知后，WIA 应用程序必须枚举 WIA 项树，以确定的任何更改的结果。

微型驱动程序使用 WIA 服务实用工具函数[ **wiasQueueEvent**](https://msdn.microsoft.com/library/windows/hardware/ff549296)，以传递到 WIA 服务的树状结构中的更改。 WIA 微型驱动程序可以排入队列中未报告的那些事件[ **IWiaMiniDrv::drvGetCapabilities**](https://msdn.microsoft.com/library/windows/hardware/ff543977)。 有关报告 WIA 事件的详细信息，请参阅[事件报告](event-reporting.md)。

### <a name="explanation-of-the-iwiaminidrvdrvdeleteitem-implementation"></a>IWiaMiniDrv::drvDeleteItem 实现的说明

WIA 服务调用[ **IWiaMiniDrv::drvDeleteItem** ](https://msdn.microsoft.com/library/windows/hardware/ff543961)方法时 WIA 应用程序调用**IWiaItem::DeleteItem** （在 Microsoft Windows 中所述的方法SDK 文档） 删除 WIA 项。

WIA 服务将验证下述软件，再调用此方法：

-   项不是根项。

-   该项是没有任何子级。

-   项的访问权限允许删除。

因为 WIA 服务将验证这些条件，则没有必要这样做 WIA 驱动程序。

下面的代码示例演示的实现**IWiaMiniDrv::drvDeleteItem**:

```cpp
HRESULT _stdcall CWIADevice::drvDeleteItem(BYTE *pWiasContext,
                                           LONG lFlags,
                                           LONG *plDevErrVal)
{
    //
    // If the caller did not pass in the correct parameters,
    // then fail the call with E_INVALIDARG.
    //

    if ((!pWiasContext) || (!plDevErrVal))
    {
        return E_INVALIDARG;
    }

    *plDevErrVal = 0;

    HRESULT hr = S_OK;

    //
    // Two pieces of information are needed to queue an event:
    // 1. Full item name
    // 2. Device ID (passed in from drvInitializeWia,
    //    or read from the ROOT item's property set)
    //

    BSTR bstrFullItemName = NULL;
    hr = wiasReadPropStr(pWiasContext,
                         WIA_IPA_FULL_ITEM_NAME,
                         &bstrFullItemName,NULL,TRUE);
    if (hr == S_OK)
    {
        hr = HARDWARE_DELETE_DATA_FOR_ITEM();
        if (hr == S_OK)
        {
            //
            // Use m_bstrDeviceID cached from the
            // drvInitializeWia method call.
            //

            hr = wiasQueueEvent(m_bstrDeviceID,
                                &WIA_EVENT_ITEM_DELETED,
                                bstrFullItemName);
        }

        //
        // Free item's full item name, read above.
        //

        if (bstrFullItemName)
        {
            SysFreeString(bstrFullItemName);
            bstrFullItemName = NULL;
        }
    }

    //
    // Returning S_OK will instruct the WIA service to remove the WIA
    // item from the item tree. The WIA minidriver should only remove
    // any associated data corresponding to the target item.
    //

    return hr;
}
```

 

 




