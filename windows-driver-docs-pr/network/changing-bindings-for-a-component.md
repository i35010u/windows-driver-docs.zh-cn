---
title: 更改组件的绑定
description: 更改组件的绑定
ms.assetid: 2e59a160-d8d9-4739-a8fa-919760f8eb05
keywords:
- 通知对象 WDK 网络绑定的更改
- 网络通知对象 WDK，绑定的更改
- 绑定更改 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a224e33b0e7742cb6b97d650acc181696170852
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382780"
---
# <a name="changing-bindings-for-a-component"></a>更改组件的绑定





网络配置子系统始终影响通知对象的网络组件绑定中的更改通知的通知对象。 子系统调用通知对象的[ **INetCfgComponentNotifyBinding::NotifyBindingPath** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547731(v=vs.85))方法，并将传递一个值，指定并提供了一个指向**INetCfgBindingPath**绑定路径更改中涉及的接口。 如果子系统通过 NCN\_禁用禁用与特定的网络卡的通知对象的网络组件共享的绑定路径，请使用另一个网卡通知对象激活绑定中的以下代码所示。

```C++
HRESULT CSample::NotifyBindingPath(DWORD dwChangeFlag,
        INetCfgBindingPath* pncbp1)
{
    INetCfgComponent *pnccLow;
    INetCfgComponentBindings *pncbind;
    IEnumNetCfgBindingPath *penumncbp;
    INetCfgBindingPath *pncbp2;
    IEnumNetCfgBindingInterface *penumncbi;
    INetCfgBindingInterface *pncbi;
    DWORD dwFlags = EBP_BELOW;
    ULONG celt = 1; // Request one enumeration element. 
    HRESULT hr = S_OK;
    // Retrieve bindings for the notify object's component (m_pncc)
    hr = m_pncc->QueryInterface(IID_INetCfgComponentBindings, 
                                (LPVOID*)&pncbind);
    // Determine if notification is about disabling a binding path.
    if (SUCCEEDED(hr) && (NCN_DISABLE & dwChangeFlag)) {
        // Retrieve enumerator for binding paths for the component.
        hr = pncbind->EnumBindingPaths(dwFlags, &penumncbp);
        // Reset the sequence and retrieve a binding path.
        hr = penumncbp->Reset();
        hr = penumncbp->Next(celt, &pncbp2, NULL);
        // Ensure the binding path is different.
        do {
            if (pncbp1 != pncbp2) break;
   hr = penumncbp->Skip(celt); // skip one element
            hr = penumncbp->Next(celt, &pncbp2, NULL);
        } while (SUCCEEDED(hr));
        if (SUCCEEDED(hr) {
            // Retrieve enumerator for interfaces of the binding path.
            hr = pncbp2->EnumBindingInterfaces(&penumncbi);
            // Retrieve a binding interface for the binding path.
            hr = penumncbi->Next(celt, &pncbi, NULL);
            // Retrieve the lower network component.
            hr = pncbi->GetLowerComponent(&pnccLow);
            // If the component is a physical network card and binding 
            // is currently disabled, enable binding.
            DWORD dwcc;
            hr = pnccLow->GetCharacteristics(&dwcc);
            if (SUCCEEDED(hr) && (dwcc & NCF_PHYSICAL)) {
                hr = pncbp2->IsEnabled(); // S_FALSE for disabled
                if (hr == S_FALSE)  hr = pncbp2->Enable(TRUE);
            }
        }
        else return hr;
    }
    return hr;
}
```

 

 





