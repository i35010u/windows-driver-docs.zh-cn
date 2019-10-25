---
title: 在网络连接向导中显示自定义 UI 页
description: 在网络连接向导中显示自定义 UI 页
ms.assetid: 102f142a-91d1-4b55-a111-15a297c03e23
keywords:
- 自定义 UI WDK 本机 802.11 IHV UI 扩展 DLL，网络连接向导
- 网络连接向导 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97c9f3e183fdfb1f356625d978b6c787d5e20478
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834825"
---
# <a name="displaying-custom-ui-pages-within-the-network-connection-wizard"></a>在网络连接向导中显示自定义 UI 页




 

当通过以下任一方式发出 UI 请求时，本机 802.11 IHV UI 扩展 DLL 支持的自定义用户界面（UI）可以在操作系统的网络连接向导中显示：

-   对[**Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request)的调用，由本机 802.11 IHV 扩展 DLL 发出。 有关此过程的详细信息，请参阅[请求显示自定义 UI](requesting-the-display-of-a-custom-ui.md)。

-   对操作系统所做的本机 802.11 IHV 扩展 DLL 的**Dot11ExtQueryUIRequest** IHV 处理程序功能的调用。 有关此过程的详细信息，请参阅[查询是否显示自定义 UI](querying-for-the-display-of-a-custom-ui.md)。

如果无线 LAN （WLAN）适配器尝试连接到无线网络，则操作系统会在网络连接向导中显示自定义 UI。 在这种情况下，自定义 UI 的请求会在该时间段内显示为气球通知：

-   操作系统调用本机 802.11 IHV 扩展 DLL 的[*Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate) IHV 处理程序函数来启动与无线网络的预关联操作。

-   在本机 802.11 IHV 扩展 DLL 调用[**Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)之前，可以成功完成关联后操作。

在网络连接向导中插入自定义 UI 请求时，操作系统执行以下操作：

1.  调用本机 802.11 IHV 扩展 DLL 的[*Dot11ExtIhvIsUIRequestPending*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_is_ui_request_pending) IHV 处理程序函数来确定 UI 请求是否仍处于挂起状态。 操作系统使用由本机 802.11 IHV 扩展 DLL 传递到[**Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request)的全局唯一标识符（GUID）来指定 UI 请求。

2.  如果对于指定的 UI 请求， [*Dot11ExtIhvIsUIRequestPending*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_is_ui_request_pending)返回**TRUE** ，则操作系统将实例化请求的**IWizardExtension** COM 接口，并将其绑定到网络连接向导的当前 UI 流。 在调用[**Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request)时，NATIVE 802.11 IHV extension Dll 在本机 802.11 Ihv UI 扩展 dll 中指定**IWizardExtension**实现的类标识符（CLSID）。

    操作系统还会调用**IWizardExtension：： AddPages**方法，通过该方法，本机 802.11 IHV UI 扩展 DLL 返回表示自定义 UI 页面的 PROPSHEETPAGE 结构的句柄数组。

    有关**IWizardExtension** com 接口的详细信息，请参阅[IWizardExtension com interface](https://go.microsoft.com/fwlink/p/?linkid=56607)。

3.  通过**IWizardSite** COM 接口，在由本机 802.11 IHV UI 扩展 DLL 控制的 ui 页面上导航。 有关此接口的详细信息，请参阅[IWIZARDSITE COM interface](https://go.microsoft.com/fwlink/p/?linkid=56608)。

显示自定义 UI 时，本机 802.11 IHV UI 扩展 DLL 可以通过[IPROPERTYBAG COM 接口](https://go.microsoft.com/fwlink/p/?linkid=56610)读取或写入特定于上下文的数据。 有关此过程的详细信息，请参阅[访问配置文件和上下文数据](accessing-profile-and-context-data.md)。

显示自定义 UI 后，本机 802.11 IHV UI 扩展 DLL 可通过调用**WlanSendUIResponse**将用户输入的响应数据返回到本机 802.11 IHV 扩展 dll。 DLL 传入 UI 请求的 GUID，以及指向包含响应数据的缓冲区的指针。

在本机 802.11 IHV UI 扩展 DLL 调用**WlanSendUIResponse**后，操作系统将调用本机 802.11 IHV 扩展 Dll 的[*Dot11ExtIhvProcessUIResponse*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_process_ui_response) IHV 处理程序函数来转发自定义 UI 的响应数据。

有关**WlanSendUIResponse** API 的详细信息，请参阅 Microsoft Windows SDK 中的文档。

 

 





