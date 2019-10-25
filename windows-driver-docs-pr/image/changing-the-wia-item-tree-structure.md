---
title: 更改 WIA 项树状结构
description: 更改 WIA 项树状结构
ms.assetid: fa6c9d25-4435-43ee-a262-9e267b9a0a69
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c05966d83ee2c27e9c2ada3d87b59992e5b24e29
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840874"
---
# <a name="changing-the-wia-item-tree-structure"></a>更改 WIA 项树状结构





WIA 微型驱动程序可以随时更改 WIA 项树结构。 当微型驱动程序对 WIA 项树进行更改时，微型驱动程序必须通知 WIA 服务。 WIA 服务随后会通知所有已连接的 WIA 应用程序。 收到通知后，WIA 应用程序必须枚举 WIA 项树来确定任何更改的结果。

微型驱动程序使用 WIA 服务实用工具函数[**wiasQueueEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasqueueevent)将树结构中的更改传达给 WIA 服务。 WIA 微型驱动程序只能将 IWiaMiniDrv 中报告的事件排队[ **：:D rvgetcapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)。 有关报告 WIA 事件的详细信息，请参阅[事件报告](event-reporting.md)。

### <a name="explanation-of-the-iwiaminidrvdrvdeleteitem-implementation"></a>IWiaMiniDrv：:d rvDeleteItem 实现的说明

当 WIA 应用程序调用**IWiaItem：:D eleteitem**方法（在 Microsoft Windows SDK 文档中进行了描述）以删除 wia 项时，wia 服务将调用[**IWiaMiniDrv：:d rvdeleteitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdeleteitem)方法。

WIA 服务在调用此方法之前将验证以下内容：

-   项不是根项。

-   该项没有子级。

-   项的访问权限允许删除。

由于 WIA 服务验证这些条件，WIA 驱动程序也不需要执行此操作。

下面的代码示例演示了 IWiaMiniDrv 的实现 **：:D rvdeleteitem**：

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

 

 




