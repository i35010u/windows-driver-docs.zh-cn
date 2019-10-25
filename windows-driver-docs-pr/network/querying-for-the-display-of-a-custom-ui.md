---
title: 查询自定义 UI 的显示
description: 查询自定义 UI 的显示
ms.assetid: 89f39281-db97-4cbe-8753-43ab30d840c8
keywords:
- 自定义 UI WDK 本机 802.11 IHV UI 扩展 DLL，查询
- 查询自定义 UI 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88a378faf4569b5a49fb76c9603522632c0eaf86
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844889"
---
# <a name="querying-for-the-display-of-a-custom-ui"></a>查询自定义 UI 的显示




 

操作系统可以查询本机 802.11 IHV 扩展 DLL，以确定 DLL 是否有要显示的自定义 UI。 每当无线 LAN （WLAN）适配器转换到 WLAN 网络连接过程中的以下阶段之一时，操作系统就会查询 DLL。

<a href="" id="pre-association-------"></a>**预先关联**   
IHV 扩展 DLL 启动前关联操作之前的连接阶段。 有关预关联操作的详细信息，请参阅[预关联](pre-association-operations.md)操作。

<a href="" id="post-association-------"></a>**后关联**   
IHV 扩展 DLL 完成后关联操作的连接阶段。 有关后处理后操作的详细信息，请参阅[之后的关联操作](post-association-operations.md)。

操作系统调用本机 802.11 IHV 扩展 DLL 的[*Dot11ExtIhvQueryUIRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_query_ui_request) IHV 处理程序函数来查询是否可以显示自定义 UI。 操作系统通过*connectionPhase*参数传递连接进程的当前阶段。 如果必须显示自定义 UI，则 DLL 通过 p *pIhvUIRequest*参数[ **\_IHV\_UI\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_ui_request)结构。

通过[**DOT11EXT\_ihv\_UI\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_ui_request)结构，本机 802.11 IHV 扩展 DLL 通过以下数据指定自定义 UI。

-   用于标识特定用户上下文的用户会话标识符（ID）。

-   全局唯一 ID （GUID），用于标识特定的 UI 请求。

-   在本机 802.11 IHV UI 扩展 DLL 中实现的**IWizardExtension** COM 接口的类 ID （CLSID）。 CLSID 用于请求 DLL 支持的特定自定义 UI。

    有关**IWizardExtension** com 接口的详细信息，请参阅[IWizardExtension com interface](https://go.microsoft.com/fwlink/p/?linkid=56607)。

-   一个缓冲区，其中包含由独立硬件供应商（IHV）定义并由指定的**IWizardExtension** COM 接口处理的专有格式的数据。 例如，缓冲区可能包含自定义 UI 中显示的默认值。

自定义 UI 将在标准网络连接 UI 中显示为一组向导页面。 有关此过程的详细信息，请参阅在[网络连接向导中显示自定义 UI 页面](displaying-custom-ui-pages-within-the-network-connection-wizard.md)。

 

 





