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
ms.openlocfilehash: b4ca9eb2324f763f721a9f4881aaeff7540f2909
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835402"
---
# <a name="accessing-profile-and-context-data"></a>访问配置文件和上下文数据




 

本机 802.11 IHV UI 扩展 DLL 支持的自定义用户界面（UI）可以通过以下两种方式之一来显示：

-   对由本机 802.11 IHV 扩展 DLL 发出的[**Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request)的调用。 有关此过程的详细信息，请参阅[请求显示自定义 UI](requesting-the-display-of-a-custom-ui.md)。

-   对操作系统所做的本机 802.11 IHV 扩展 DLL 的*Dot11ExtQueryUIRequest* IHV 处理程序功能的调用。 有关此过程的详细信息，请参阅[查询是否显示自定义 UI](querying-for-the-display-of-a-custom-ui.md)。

无论 UI 请求是通过气球通知还是通过操作系统的网络连接向导显示，本机 802.11 IHV UI 扩展 DLL 都可以访问以下数据：

<a href="" id="network-connection-profile-data"></a>**网络连接配置文件数据**  
如果在网络连接向导中显示自定义用户界面，则本机 802.11 IHV UI 扩展 DLL 可以访问当前网络连接配置文件中由 IHV 定义的部分。 此数据的格式为由 &lt;IHV&gt; &lt;/IHV&gt; XML 标记限定的 XML 片段。 这些标记中的 XML 数据特定于 IHV 的实现，对操作系统不透明。

对于名为**IHV\_配置文件\_数据**的属性，通过[IPropertyBag COM 接口](https://go.microsoft.com/fwlink/p/?linkid=56610)的**读取**和**写入**方法访问配置文件数据。

<a href="" id="context-data"></a>**上下文数据**  
本机 802.11 IHV 扩展 DLL 通过[**DOT11EXT\_IHV\_UI\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_ui_request)结构来指定自定义 UI，该 ui 作为参数在[**Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request)和[*Dot11ExtIhvQueryUIRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_query_ui_request)中传递。函数. 在 DOT11EXT\_IHV\_UI\_请求结构中，IHV 可以提供特定于自定义 UI 的**pvUIRequest**成员）上下文数据。 通常，IHV 用自定义 UI 的默认设置来设置此数据的格式。

对于名为**IHV\_通知\_数据**的属性，可以通过[IPropertyBag COM 接口](https://go.microsoft.com/fwlink/p/?linkid=56610)的**读取**和**写入**方法访问配置文件数据。

本机 802.11 IHV UI 扩展 DLL 通过[**IObjectWithSite：： SetSite**](https://docs.microsoft.com/windows/desktop/api/ocidl/nf-ocidl-iobjectwithsite-setsite)方法返回的*IUnknown*指针访问[IPropertyBag COM 接口](https://go.microsoft.com/fwlink/p/?linkid=56610)。 有关详细信息，请参阅[**IObjectWithSite**](https://docs.microsoft.com/windows/desktop/api/ocidl/nn-ocidl-iobjectwithsite)。

作为 IPropertyBag COM 接口的替代方法，本机 802.11 IHV UI 扩展 DLL 可通过[**GetProp**](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-getpropa) Win32 访问**IHV\_配置文件\_数据**和**ihv\_通知\_数据**属性才能. 在这种情况下，DLL 必须使用父窗口的句柄，如以下示例中所示：

```C++
LPWSTR lpszBuffer = (LPWSTR) GetProp(GetParent(hwndDlg), L"IHV_PROFILE_DATA");
```

 

 





