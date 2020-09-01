---
title: 添加组件
description: 添加组件
ms.assetid: f8177904-77a2-4d1a-8c72-0b47a100bc37
keywords:
- 通知对象 WDK 网络，添加组件
- 网络通知对象 WDK，添加组件
- 添加网络组件
- 网络组件添加 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f675cede3b77ef458c11c93d17e5f6e9191513f1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210797"
---
# <a name="adding-a-component"></a>添加组件





当子系统添加网络组件时，网络配置子系统可以通知通知对象。 初始化 notify 对象之后，子系统将调用 notify 对象的 [**INetCfgComponentNotifyGlobal：： GetSupportedNotifications**](/previous-versions/windows/hardware/network/ff547734(v=vs.85)) 方法来检索该对象所需的通知类型。 如果通知对象指定了在添加网络组件时需要通知，则子系统将调用 notify 对象的 [**INetCfgComponentNotifyGlobal：： SysNotifyComponent**](/previous-versions/windows/hardware/network/ff547736(v=vs.85)) 方法并传递 NCN ADD， \_ 以通知通知对象子系统安装了网络组件。 如果拥有通知对象的组件应绑定到指定的组件，则通知对象应执行操作以促进绑定。 例如，下面的代码演示如果指定组件是必需的物理网卡，则 notify 对象如何将其组件绑定到指定组件。

```cpp
HRESULT CSample::SysNotifyComponent(DWORD dwChangeFlag,
        INetCfgComponent* pnccItem)
{
    HRESULT hr = S_OK;
    INetCfgComponentBindings *pncfgcompbind;
    // Retrieve bindings for the notify object's component (m_pncc)
    hr = m_pncc->QueryInterface(IID_INetCfgComponentBindings, 
                                (LPVOID*)&pncfgcompbind);
    // Determine if notification is about adding a component
    if (SUCCEEDED(hr) && (NCN_ADD & dwChangeFlag)) {
        // Retrieve the characteristics of the added component
        DWORD dwcc;
        hr = pnccItem->GetCharacteristics(&dwcc);
        // Determine if the added component is a physical adapter
        if (SUCCEEDED(hr) && (dwcc & NCF_PHYSICAL)) {
            // Determine the component's ID
            LPWSTR pszwInfId;
            hr = pnccItem->GetId(&pszwInfId);
            if (SUCCEEDED(hr)) {
                // Compare the component's ID to the required ID
                // and if they are the same perform the binding.
                static const TCHAR c_szCompId[] = TEXT("BINDTO_NIC");
                if (!_tcsicmp(pszwInfId, c_szCompId)) {
                    hr = pncfgcompbind->BindTo(pnccItem);
                }
            }
        }
    }
    return hr;
}
```

 

