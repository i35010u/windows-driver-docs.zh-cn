---
title: 检索网络配置接口指针
description: 检索网络配置接口指针
keywords:
- 通知对象 WDK 网络，接口指针
- 网络通知对象 WDK，接口指针
- 网络配置接口指针 WDK
- 接口指针 WDK 网络
- 指针 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d7fc1919c30c057851cd28dd566903ce1a696c9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817081"
---
# <a name="retrieving-network-configuration-interface-pointers"></a>检索网络配置接口指针





当网络配置子系统初始化 notify 对象的实例（如 [创建和初始化 Notify 对象的实例](creating-and-initializing-an-instance-of-a-notify-object.md)中所述）时，对象将接收 [**INetCfgComponent**](/previous-versions/windows/hardware/network/ff547715(v=vs.85)) 和 [**INetCfg**](/previous-versions/windows/hardware/network/ff547694(v=vs.85)) 接口指针。 **INetCfgComponent** 指向通知对象的组件接口，对象可使用该接口访问和控制组件。 **INetCfg** 指向根网络配置接口，通知对象可使用该接口访问网络配置的所有方面。 下面的代码使用这些 **INetCfgComponent** 和 **INetCfg** 接口指针检索 notify 对象可能需要的其他网络配置接口。

```C++
// Using the notify object's component interface that the notify 
// object received:
INetCfgComponent *pncfgcompThis, *pncfgcompUp, *pncfgcompLow;
INetCfgComponentBindings *pncfgcompbind;
IEnumNetCfgBindingPath *penumncfgbindpath;
INetCfgBindingPath *pncfgbindpath;
IEnumNetCfgBindingInterface *penumncfgbindintrfc;
INetCfgBindingInterface *pncfgbindintrfc;
HRESULT hr;
DWORD dwFlags;  // EBP_ABOVE or EBP_BELOW
ULONG celt, celtFetched; // Number of requested and returned elements

// Retrieve a pointer to INetCfgComponentBindings to control and 
// retrieve information about bindings for the component.
hr = pncfgcompThis->QueryInterface(IID_INetCfgComponentBindings, 
                                  (LPVOID*)&pncfgcompbind);
// Retrieve a pointer to IEnumNetCfgBindingPath to enumerate binding 
// paths for the component.
hr = pncfgcompbind->EnumBindingPaths(dwFlags, &penumncfgbindpath);
// Retrieve a pointer to INetCfgBindingPath that points to one or more 
// binding paths for the component.
hr = penumncfgbindpath->Next(celt, &pncfgbindpath, &celtFetched);
// Retrieve a pointer to IEnumNetCfgBindingInterface to enumerate 
// the collection of binding interfaces for the binding path.
hr = pncfgbindpath->EnumBindingInterfaces(&penumncfgbindintrfc);
// Retrieve a pointer to INetCfgBindingInterface that points to one or 
// more binding interfaces for the binding path.
hr = penumncfgbindintrfc->Next(celt, &pncfgbindintrfc, &celtFetched);
// Retrieve pointers to INetCfgComponent for network components 
// above and below the binding interface.
hr = pcfgbindintrfc->GetUpperComponent(&pncfgcompUp);
hr = pcfgbindintrfc->GetLowerComponent(&pncfgcompLow);

// Using the root network configuration interface that the notify 
// object received:
INetCfg *pnetcfg;
INetCfgLock *pncfglock;
INetCfgClass *pncfgclass;
INetCfgComponent *pncfgcompOther, *pncfgcompInstall;
INetCfgClassSetup *pncfgclsSetup
GUID *pguidClass; // For example, set to GUID_DEVCLASS_NETTRANS
IEnumNetCfgComponent *penumncfgcomp;
HWND hwndParent; // Handle to Window for selecting.
OBO_TOKEN *pOboToken; // Another component or the user installs.
DWORD dwSetupFlags, dwUpgradeFromBuildNo;
 
// Retrieve a pointer to INetCfgLock to obtain a lock on network 
// configuration.
hr = pnetcfg->QueryInterface(IID_INetCfgLock, (LPVOID*)&pncfglock);
// Retrieve a pointer to INetCfgComponent for a specific component.
hr = pnetcfg->FindComponent(TEXT("MS_TCPIP"), &pncfgcompOther);
// Retrieve a pointer to IEnumNetCfgComponent to enumerate 
// the collection of a particular type of component.
hr = pnetcfg->EnumComponents(pguidClass, &penumncfgcomp);
// Retrieve a pointer to INetCfgClass for a specific class of 
// component.
hr = pnetcfg->QueryNetCfgClass(pguidClass, IID_INetCfgClass, 
                              (LPVOID*)&pncfgclass);
// Retrieve a pointer to INetCfgComponent for a specific component.
hr = pncfgclass->FindComponent(TEXT("MS_TCPIP"), &pncfgcompOther);
// Retrieve a pointer to IEnumNetCfgComponent to enumerate 
// the collection of a particular type of component.
hr = pncfgclass->EnumComponents(&penumncfgcomp);
// Retrieve a pointer to INetCfgComponent that points to one or 
// more components for the particular type of component.
hr = penumncfgcomp->Next(celt, &pncfgcompOther, &celtFetched);
// Retrieve a pointer to INetCfgClassSetup that enables installation 
// or removal of a particular type of component.
hr = pncfgclass->QueryInterface(IID_INetCfgClassSetup, 
                               (LPVOID*)&pncfgclsSetup);
// Retrieve a pointer to INetCfgComponent for an installed component.
hr = pncfgclsSetup->SelectAndInstall(hwndParent, pOboToken,
                                     &pncfgcompInstall);
// Retrieve a pointer to INetCfgComponent for an installed component.
hr = pncfgclsSetup->Install(TEXT("MS_TCPIP"), pOboToken, dwSetupFlags, 
                           dwUpgradeFromBuildNo, TEXT("AnswerFile"), 
                    TEXT("AnswerFileSections"), &pncfgcompInstall);
```

 

