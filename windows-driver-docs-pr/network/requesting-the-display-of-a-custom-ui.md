---
title: 请求显示自定义 UI
description: 请求显示自定义 UI
ms.assetid: 4b7366d9-e55a-4b24-b75f-a5f133b80ca7
keywords:
- 自定义 UI WDK 本机 802.11 IHV UI 扩展 DLL，请求显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a114e9b14d67c642506b1b9270da34e1039db49d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842033"
---
# <a name="requesting-the-display-of-a-custom-ui"></a>请求显示自定义 UI




 

本机 802.11 IHV 扩展 DLL 可以通过本机 802.11 IHV UI 扩展 DLL 请求显示自定义用户界面（UI）。 例如，IHV 扩展 DLL 可能会请求向显示自定义 UI：

-   在无线 LAN （WLAN）关联操作期间，在各个阶段通知最终用户。

-   当 WLAN 适配器与 WLAN 网络解除关联时，通知最终用户。

-   向最终用户通知 WLAN 网络身份验证的结果。

若要启动自定义 UI 或显示通知，本机 802.11 IHV 扩展 DLL 将调用[**Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request) ，并通过*PIhvUIRequest*将指向[**DOT11EXT\_IHV\_UI\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_ui_request)结构的指针传递到该 ui此函数的参数。

通过[**DOT11EXT\_ihv\_UI\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_ui_request)结构，本机 802.11 IHV 扩展 DLL 通过以下数据指定自定义 UI：

-   用于标识特定用户上下文的用户会话标识符（ID）。

-   全局唯一 ID （GUID），用于标识特定的 UI 请求。

-   在本机 802.11 IHV UI 扩展 DLL 中实现的**IWizardExtension** COM 接口的类 ID （CLSID）。 CLSID 用于请求 DLL 支持的特定自定义 UI。

    有关**IWizardExtension** com 接口的详细信息，请参阅[IWizardExtension com interface](https://go.microsoft.com/fwlink/p/?linkid=56607)。

-   一个缓冲区，其中包含由独立硬件供应商（IHV）定义并由指定的**IWizardExtension** COM 接口处理的专有格式的数据。 例如，缓冲区可能包含自定义 UI 中显示的默认值。

根据用户会话 ID 的 WLAN 连接状态，自定义 UI 请求将显示为以下内容之一：

-   如果适配器已连接到 WLAN 网络，请求会显示为通过可单击的气球通知启动的独立 UI。 有关此过程的详细信息，请参阅[显示气球通知](displaying-custom-ui-pages-within-a-balloon-notification.md)。

-   如果适配器正在连接到 WLAN 网络，请求将显示为标准网络连接用户界面中的一组向导页面。 有关此过程的详细信息，请参阅在[网络连接向导中显示自定义 UI 页面](displaying-custom-ui-pages-within-the-network-connection-wizard.md)。

 

 





