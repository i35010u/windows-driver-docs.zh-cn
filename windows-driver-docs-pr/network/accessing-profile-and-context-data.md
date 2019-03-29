---
title: 访问配置文件和上下文数据
description: 访问配置文件和上下文数据
ms.assetid: 88463b20-e61b-4258-b5ff-9b6880c1d0f6
keywords:
- 自定义 UI WDK 本机 802.11 IHV UI 扩展 DLL，配置文件数据
- 自定义 UI WDK 本机 802.11 IHV UI 扩展 DLL，上下文数据
- 上下文数据 WDK 网络
- 配置文件数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9ff345d7d316dd51c071449acaaaf7d5a2b5d32
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565284"
---
# <a name="accessing-profile-and-context-data"></a>访问配置文件和上下文数据




 

可以通过显示自定义用户界面 (UI) 支持的本机 802.11 IHV UI 扩展 DLL:

-   调用[ **Dot11ExtSendUIRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff547567)所做的本机 802.11 IHV 扩展 DLL。 有关此过程的详细信息，请参阅[请求的自定义用户界面显示](requesting-the-display-of-a-custom-ui.md)。

-   本机 802.11 IHV 扩展 DLL 的调用*Dot11ExtQueryUIRequest* IHV 处理程序函数所做的操作系统。 有关此过程的详细信息，请参阅[查询的自定义用户界面显示](querying-for-the-display-of-a-custom-ui.md)。

无论是否通过气球状通知或操作系统的网络连接向导显示 UI 请求，本机 802.11 IHV UI 扩展 DLL 可以访问以下数据：

<a href="" id="network-connection-profile-data"></a>**网络连接配置文件数据**  
如果网络连接向导中显示自定义 UI，则本机 802.11 IHV UI 扩展 DLL 可以访问当前的网络连接配置文件的 IHV 定义部分。 此数据将格式化为 XML 片段受&lt;IHV&gt; &lt;/IHV&gt; XML 标记。 在此标记中的 XML 数据是特定于 IHV 的实现，并对操作系统是不透明。

对配置文件数据的访问是通过**读**并**编写**方法[IPropertyBag COM 接口](https://go.microsoft.com/fwlink/p/?linkid=56610)属性名为**IHV\_配置文件\_数据**。

<a href="" id="context-data"></a>**上下文数据**  
本机 802.11 IHV 扩展 DLL 指定通过自定义 UI [ **DOT11EXT\_IHV\_UI\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff547637)结构，它作为两者中的自变量传递[ **Dot11ExtSendUIRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff547567)并[ *Dot11ExtIhvQueryUIRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff547507)函数。 在 DOT11EXT\_IHV\_UI\_IHV 可以提供请求结构 (通过**pvUIRequest**成员) 的上下文数据的自定义 ui。 通常，IHV 格式化此数据使用自定义 UI 的默认设置。

对配置文件数据的访问是通过**读**并**编写**方法[IPropertyBag COM 接口](https://go.microsoft.com/fwlink/p/?linkid=56610)属性名为**IHV\_通知\_数据**。

访问本机 802.11 IHV UI 扩展 DLL [IPropertyBag COM 接口](https://go.microsoft.com/fwlink/p/?linkid=56610)通过*IUnknown*返回通过指针[ **IObjectWithSite::SetSite** ](https://msdn.microsoft.com/library/windows/desktop/ms683869)方法。 有关详细信息，请参阅[ **IObjectWithSite**](https://msdn.microsoft.com/library/windows/desktop/ms693765)。

作为 IPropertyBag COM 接口的替代方法，可以访问本机 802.11 IHV UI 扩展 DLL **IHV\_配置文件\_数据**并**IHV\_通知\_数据**属性流过[ **GetProp** ](https://msdn.microsoft.com/library/windows/desktop/ms633564) Win32 函数。 在此情况下，DLL 必须使用父窗口的句柄，在下面的示例所示：

```
LPWSTR lpszBuffer = (LPWSTR) GetProp(GetParent(hwndDlg), L"IHV_PROFILE_DATA");
```

 

 





