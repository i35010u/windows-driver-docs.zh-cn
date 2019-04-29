---
title: 在网络连接向导中显示自定义 UI 页
description: 在网络连接向导中显示自定义 UI 页
ms.assetid: 102f142a-91d1-4b55-a111-15a297c03e23
keywords:
- 自定义 UI WDK 本机 802.11 IHV UI 扩展 DLL，网络连接向导
- 网络连接向导 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71b3a0d2d8c408567fe0b734dbc49f1178a5f3db
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379561"
---
# <a name="displaying-custom-ui-pages-within-the-network-connection-wizard"></a>在网络连接向导中显示自定义 UI 页




 

通过进行 UI 的请求时，支持的本机 802.11 IHV UI 扩展 DLL 的自定义用户界面 (UI) 可以显示操作系统的网络连接向导中：

-   调用[ **Dot11ExtSendUIRequest**](https://msdn.microsoft.com/library/windows/hardware/ff547567)、 本机 802.11 IHV 扩展 DLL 由发出。 有关此过程的详细信息，请参阅[请求的自定义用户界面显示](requesting-the-display-of-a-custom-ui.md)。

-   本机 802.11 IHV 扩展 DLL 的调用**Dot11ExtQueryUIRequest** IHV 处理程序函数，所做的操作系统。 有关此过程的详细信息，请参阅[查询的自定义用户界面显示](querying-for-the-display-of-a-custom-ui.md)。

如果无线 LAN (WLAN) 适配器尝试连接到无线网络，操作系统会显示网络连接向导中的自定义 UI。 在此情况下，自定义 UI 的请求将显示为时间段内的气球状通知：

-   操作系统将调用本机 802.11 IHV 扩展 DLL 的后[ *Dot11ExtIhvPerformPreAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547499) IHV 处理程序函数以启动无线网络使用预关联操作。

-   本机 802.11 IHV 扩展 DLL 调用之前[ **Dot11ExtPostAssociateCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff547530)才能成功完成后关联操作。

在插入自定义 UI 请求网络连接向导中的，操作系统执行以下任务：

1.  调用本机 802.11 IHV 扩展 DLL [ *Dot11ExtIhvIsUIRequestPending* ](https://msdn.microsoft.com/library/windows/hardware/ff547479) IHV 处理程序函数来确定是否仍然 UI 请求挂起。 操作系统指定使用传递到的全局唯一标识符 (GUID) 的用户界面请求[ **Dot11ExtSendUIRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff547567)本机 802.11 IHV 扩展 dll。

2.  如果[ *Dot11ExtIhvIsUIRequestPending* ](https://msdn.microsoft.com/library/windows/hardware/ff547479)返回**TRUE**对于指定的 UI 请求，操作系统将实例化请求**IWizardExtension** COM 接口和绑定到的当前 UI 流的网络连接向导。 当调用[ **Dot11ExtSendUIRequest**](https://msdn.microsoft.com/library/windows/hardware/ff547567)，本机 802.11 IHV 扩展 DLL 的指定类标识符 (CLSID) **IWizardExtension**实现中的本机 802.11 IHV UI 扩展 DLL。

    操作系统还会调用**IWizardExtension::AddPages**方法，通过该本机 802.11 IHV UI 扩展 DLL 返回一个表示自定义 UI 页面 PROPSHEETPAGE 结构的句柄数组。

    有关详细信息**IWizardExtension** COM 接口，请参阅[IWizardExtension COM 接口](https://go.microsoft.com/fwlink/p/?linkid=56607)。

3.  通过本机 802.11 IHV UI 扩展 DLL 由控制导航的 UI 页面**IWizardSite** COM 接口。 有关此接口的详细信息，请参阅[IWizardSite COM 接口](https://go.microsoft.com/fwlink/p/?linkid=56608)。

本机 802.11 IHV UI 扩展 DLL 时显示自定义 UI，则可读取或写入特定于上下文的数据通过[IPropertyBag COM 接口](https://go.microsoft.com/fwlink/p/?linkid=56610)。 有关此过程的详细信息，请参阅[访问配置文件和上下文数据](accessing-profile-and-context-data.md)。

本机 802.11 IHV UI 扩展 DLL 将显示自定义用户界面后，可以通过调用到本机 802.11 IHV 扩展 DLL 返回用户输入的响应数据**WlanSendUIResponse**。 DLL 将传递的 guid 的 UI 请求，以及一个指针，到包含响应数据的缓冲区。

本机 802.11 IHV UI 扩展 DLL 后，将调用**WlanSendUIResponse**，操作系统将调用本机 802.11 IHV 扩展 DLL [ *Dot11ExtIhvProcessUIResponse* ](https://msdn.microsoft.com/library/windows/hardware/ff547504)为转发自定义 UI 的响应数据的 IHV 处理程序函数。

有关详细信息**WlanSendUIResponse** API，请参阅 Microsoft Windows SDK 中的文档。

 

 





