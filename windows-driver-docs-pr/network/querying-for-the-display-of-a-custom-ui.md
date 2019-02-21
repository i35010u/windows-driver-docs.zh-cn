---
title: 查询自定义 UI 的显示器
description: 查询自定义 UI 的显示器
ms.assetid: 89f39281-db97-4cbe-8753-43ab30d840c8
keywords:
- 自定义 UI WDK 本机 802.11 IHV UI 扩展 DLL，查询
- 查询自定义用户界面显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f359fb087120412a9bbdd99fc6ed99cfb39d51b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541918"
---
# <a name="querying-for-the-display-of-a-custom-ui"></a>查询自定义 UI 的显示器




 

操作系统可以查询本机的 802.11 IHV 扩展 DLL，若要确定 DLL 是否具有用于显示的自定义 UI。 每当无线 LAN (WLAN) 适配器将转换为 WLAN 的网络连接过程中的以下阶段之一，操作系统将查询该 DLL。

<a href="" id="pre-association-------"></a>**预关联**   
连接阶段之前 IHV 扩展 DLL 启动预关联操作。 有关预关联操作的详细信息，请参阅[预关联操作](pre-association-operations.md)。

<a href="" id="post-association-------"></a>**后期关联**   
IHV 扩展 DLL 之后连接阶段完成后关联操作。 有关后关联操作的详细信息，请参阅[后期关联操作](post-association-operations.md)。

操作系统将调用本机 802.11 IHV 扩展 DLL [ *Dot11ExtIhvQueryUIRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff547507) IHV 处理程序函数查询是否可以显示自定义 UI。 操作系统将通过在连接过程的当前阶段传递*connectionPhase*参数。 如果必须显示自定义 UI，返回该 DLL [ **DOT11EXT\_IHV\_UI\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff547637)结构通过 p *pIhvUIRequest*参数。

通过[ **DOT11EXT\_IHV\_UI\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff547637)结构，本机 802.11 IHV 扩展 DLL 指定通过以下数据的自定义 UI。

-   用户会话标识符 (ID)，用于标识特定的用户上下文。

-   全局唯一 ID (GUID)，用于标识特定的用户界面请求。

-   类 ID (CLSID) 的**IWizardExtension**在本机 802.11 IHV UI 扩展 DLL 中实现的 COM 接口。 CLSID 用于请求特定的自定义 UI 支持的 DLL。

    有关详细信息**IWizardExtension** COM 接口，请参阅[IWizardExtension COM 接口](https://go.microsoft.com/fwlink/p/?linkid=56607)。

-   包含将由独立硬件供应商 (IHV) 定义并由指定处理的专有格式的数据的缓冲区**IWizardExtension** COM 接口。 例如，缓冲区可能包含自定义用户界面中显示的默认值。

自定义 UI 将显示为一组标准的网络连接 UI 中的向导页。 有关此过程的详细信息，请参阅[网络连接向导中显示自定义 UI 页面](displaying-custom-ui-pages-within-the-network-connection-wizard.md)。

 

 





