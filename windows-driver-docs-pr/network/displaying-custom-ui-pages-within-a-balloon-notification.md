---
title: 在气球通知中显示自定义 UI 页
description: 在气球通知中显示自定义 UI 页
ms.assetid: 5ed2ba59-88ae-4379-b729-1d741b30a7a0
keywords:
- 自定义 UI WDK 本机 802.11 IHV UI 扩展 DLL，气球状通知
- 气球状通知 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 208e131c18a2a59d7cdcf2c4e2d3e3778ebff1ce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386564"
---
# <a name="displaying-custom-ui-pages-within-a-balloon-notification"></a>在气球通知中显示自定义 UI 页




 

如果调用本机 802.11 IHV 扩展 DLL [ **Dot11ExtSendUIRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_ui_request)若要显示自定义用户界面 (UI)，操作系统将显示可单击气球状通知通过 UI 如果无线 LAN (WLAN) 适配器已连接到无线网络。 在这种情况下，自定义 UI 的请求显示为气球状通知：

-   本机 802.11 IHV 扩展 DLL 后，将调用[ **Dot11ExtPostAssociateCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)才能成功完成后关联操作。

-   操作系统将调用 DLL 的前[ *Dot11ExtIhvAdapterReset* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_adapter_reset) IHV 处理程序函数来重置 WLAN 连接。

本机 802.11 IHV 扩展 DLL 如何请求的自定义 UI 显示的详细信息，请参阅[请求的自定义 UI 显示](requesting-the-display-of-a-custom-ui.md)。

在处理作为气球状通知的自定义 UI 请求时，操作系统执行以下操作。

1.  调用本机 802.11 IHV 扩展 DLL [ *Dot11ExtIhvIsUIRequestPending* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_is_ui_request_pending) IHV 处理程序函数来确定是否仍然 UI 请求挂起。 操作系统指定使用传递到的全局唯一标识符 (GUID) 的用户界面请求[ **Dot11ExtSendUIRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_ui_request)本机 802.11 IHV 扩展 dll。

2.  如果[ *Dot11ExtIhvIsUIRequestPending* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_is_ui_request_pending)返回**TRUE**对于指定的 UI 请求，操作系统将调用本机 802.11 IHV UI 扩展 DLL 的[**IDot11ExtUI::GetDot11ExtUIBalloonText** ](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/ff553771(v=vs.85))方法。 通过此方法，该 DLL 返回包含要在气球状通知中显示的本地化的文本的字符串缓冲区。

3.  显示包含本地化的文本的气球状通知。

4.  如果最终用户单击气球状通知，操作系统将启动受支持的自定义 UI 的请求**IWizardExtension** COM 接口。 当调用[ **Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_ui_request)，本机 802.11 IHV 扩展 DLL 的指定类标识符 (CLSID) **IWizardExtension**实现中的本机 802.11 IHV UI 扩展 DLL。

    当操作系统将调用**IWizardExtension::AddPages**方法，本机 802.11 IHV UI 扩展 DLL 返回一个表示自定义 UI 页面 PROPSHEETPAGE 结构的句柄数组。

    有关详细信息**IWizardExtension** COM 接口，请参阅[IWizardExtension COM 接口](https://go.microsoft.com/fwlink/p/?linkid=56607)。 有关 PROPSHEETPAGE 结构的详细信息，请参阅 Microsoft Windows SDK 中的文档。

5.  通过本机 802.11 IHV UI 扩展 DLL 由指定的 UI 页面中导航**IWizardSite** COM 接口。 有关此接口的详细信息，请参阅[IWizardSite COM 接口](https://go.microsoft.com/fwlink/p/?linkid=56608)。

本机 802.11 IHV UI 扩展 DLL 时显示自定义 UI，则可读取或写入特定于上下文的数据通过[IPropertyBag COM 接口](https://go.microsoft.com/fwlink/p/?linkid=56610)。 有关此过程的详细信息，请参阅[访问配置文件和上下文数据](accessing-profile-and-context-data.md)。 本机 802.11 IHV UI 扩展 DLL 的自定义 UI 显示已完成后，可以通过调用到本机 802.11 IHV 扩展 DLL 返回用户输入的响应数据**WlanSendUIResponse** 。 DLL 将传递的 guid 的 UI 请求，以及一个指针，到包含响应数据的缓冲区。

本机 802.11 IHV UI 扩展 DLLcalls 后**WlanSendUIResponse**，操作系统将调用本机 802.11 IHV 扩展 DLL [ *Dot11ExtIhvProcessUIResponse* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_process_ui_response)为转发自定义 UI 的响应数据的 IHV 处理程序函数。

有关详细信息**WlanSendUIResponse** API，请参阅 Windows SDK 中的文档。

 

 





