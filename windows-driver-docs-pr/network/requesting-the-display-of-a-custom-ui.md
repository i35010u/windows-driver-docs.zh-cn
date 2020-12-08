---
title: 请求显示自定义 UI
description: 请求显示自定义 UI
keywords:
- 自定义 UI WDK 本机 802.11 IHV UI 扩展 DLL，请求显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f321a23c515974110c96759d020b2a619ac4541
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820009"
---
# <a name="requesting-the-display-of-a-custom-ui"></a>请求显示自定义 UI




 

本机 802.11 IHV 扩展 DLL 可以通过本机 802.11 IHV UI 扩展 DLL 请求 (UI) 中显示自定义用户界面。 例如，IHV 扩展 DLL 可能会请求向显示自定义 UI：

-   在无线局域网 (WLAN) 关联操作期间，通知最终用户。

-   当 WLAN 适配器与 WLAN 网络解除关联时，通知最终用户。

-   向最终用户通知 WLAN 网络身份验证的结果。

若要启动自定义 UI 或显示通知，本机 802.11 IHV 扩展 DLL 将调用 [**Dot11ExtSendUIRequest**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request) ，并通过此函数的 *pIhvUIRequest* 参数将指针传递到 [**DOT11EXT \_ IHV \_ UI \_ 请求**](/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_ui_request)结构。

通过 [**DOT11EXT \_ IHV \_ UI \_ 请求**](/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_ui_request) 结构，本机 802.11 ihv 扩展 DLL 通过以下数据指定自定义 UI：

-   用户会话标识符 (ID) ，用于标识特定用户上下文。

-   全局唯一 ID (GUID) ，用于标识特定 UI 请求。

-   类 ID (在本机 802.11 IHV UI 扩展 DLL 中实现的 **IWizardExtension** COM 接口的 CLSID) 。 CLSID 用于请求 DLL 支持的特定自定义 UI。

    有关 **IWizardExtension** com 接口的详细信息，请参阅 [IWizardExtension com interface](/windows/win32/api/shobjidl/nn-shobjidl-iwizardextension)。

-   包含由独立硬件供应商 (IHV 定义的专有格式的数据的缓冲区) 并由指定的 **IWizardExtension** COM 接口处理。 例如，缓冲区可能包含自定义 UI 中显示的默认值。

根据用户会话 ID 的 WLAN 连接状态，自定义 UI 请求将显示为以下内容之一：

-   如果适配器已连接到 WLAN 网络，请求会显示为通过可单击的气球通知启动的独立 UI。 有关此过程的详细信息，请参阅 [显示气球通知](displaying-custom-ui-pages-within-a-balloon-notification.md)。

-   如果适配器正在连接到 WLAN 网络，请求将显示为标准网络连接用户界面中的一组向导页面。 有关此过程的详细信息，请参阅在 [网络连接向导中显示自定义 UI 页面](displaying-custom-ui-pages-within-the-network-connection-wizard.md)。

 

 
