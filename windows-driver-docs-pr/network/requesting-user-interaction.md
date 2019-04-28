---
title: 请求用户交互
description: 请求用户交互
ms.assetid: 888faeb0-1984-4b0f-b955-2772a6bd86f7
keywords:
- 用户交互 WDK 本机 802.11 IHV 扩展 DLL
- 请求用户交互 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2fe595483b2b03c5e16354a0963cc68aea85b80
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349394"
---
# <a name="requesting-user-interaction"></a>请求用户交互




 

在调用任何时候[ *Dot11ExtIhvInitAdapter*](https://msdn.microsoft.com/library/windows/hardware/ff547469)，IHV 扩展 DLL 可通过调用来请求与用户交互[ **Dot11ExtSendUIRequest**](https://msdn.microsoft.com/library/windows/hardware/ff547567)函数。 操作系统将所有用户交互请求都转发到 IHV UI 扩展 DLL，它将处理该请求并向用户显示相应的用户界面 (UI) 页。

请求已完成时，操作系统将调用[ *Dot11ExtIhvProcessUIResponse* ](https://msdn.microsoft.com/library/windows/hardware/ff547504)函数以将结果转发从 IHV UI 扩展 DLL，为用户交互。 IHV UI 扩展 DLL 的详细信息，请参阅[本机 802.11 IHV UI 扩展 DLL](native-802-11-ihv-ui-extensions-dll2.md)。

例如，IHV 扩展 DLL 可以请求的以下任何用户交互。

-   通知用户有关前或后关联的操作的阶段。

-   提示用户进行身份验证后关联操作过程中输入其凭据。

当调用[ **Dot11ExtSendUIRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff547567)函数，IHV 扩展 DLL 将传递一个指向[ **DOT11EXT\_IHV\_UI\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff547637)结构*pIhvUIRequest*参数。 DOT11EXT\_IHV\_UI\_请求结构指定的请求，例如全局唯一 ID (GUID)，它标识 UI 请求，以及 COM 类 ID (CLSID) 将处理此请求的目标 UI 页。

用户通知完成后 IHV UI 扩展 DLL，操作系统将调用[ *Dot11ExtIhvProcessUIResponse* ](https://msdn.microsoft.com/library/windows/hardware/ff547504)函数。 如果用户输入的任何数据通过通知，操作系统会将指针传递到缓冲区，其中包含的数据，为*pvResponseBuffer*参数。

操作系统可能会定期查询挂起的通知请求的状态。 在此情况下，操作系统将调用[ *Dot11ExtIhvIsUIRequestPending* ](https://msdn.microsoft.com/library/windows/hardware/ff547479) ，并将传递到 UI 请求的 GUID *guidUIRequest*参数。

调用时[ **Dot11ExtSendUIRequest**](https://msdn.microsoft.com/library/windows/hardware/ff547567)，IHV 扩展 DLL 必须遵循这些准则。

-   IHV 扩展 DLL 不需要序列化到调用[ **Dot11ExtSendUIRequest**](https://msdn.microsoft.com/library/windows/hardware/ff547567)。 该 DLL 可以有多个挂起的用户界面请求在任何时间。

-   特定 GUID 在 UI 请求完成时，才[ *Dot11ExtIhvProcessUIResponse* ](https://msdn.microsoft.com/library/windows/hardware/ff547504)称为该 GUID。 在此情况下，IHV 扩展 DLL 必须释放任何已分配的资源，直到 UI 请求*Dot11ExtIhvProcessUIResponse*调用。

-   所有挂起的用户界面取消请求时[ *Dot11ExtIhvAdapterReset* ](https://msdn.microsoft.com/library/windows/hardware/ff547434)或[ *Dot11ExtIhvDeinitAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff547452)调用。 请求将同时取消所有挂起的 UI 每当[ *Dot11ExtIhvProcessSessionChange* ](https://msdn.microsoft.com/library/windows/hardware/ff547501)使用调用*uEventType*参数设置为 WTS\_会话\_注销。

    在这些情况下，IHV 扩展 DLL 必须释放所有已分配的资源，为每个挂起的用户界面请求。

操作系统可以启动用户交互本身，每当在基本服务的连接状态更改设置 (BSS) 网络。 在此情况下，操作系统将调用[ *Dot11ExtIhvQueryUIRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff547507)函数。 IHV 扩展 DLL 分配缓冲区，并将其作为格式化[ **DOT11EXT\_IHV\_UI\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff547637)结构。 DLL 设置的成员的 DOT11EXT\_IHV\_UI\_请求结构来引用 UI 页上，适合于当前连接状态更改。 操作系统负责显示 UI 页。

**请注意**  IHV 扩展必须分配包含缓冲区[ **DOT11EXT\_IHV\_UI\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff547637)结构通过[ **Dot11ExtAllocateBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff547419)。 DLL 必须从返回后不释放缓冲区[ *Dot11ExtIhvQueryUIRequest*](https://msdn.microsoft.com/library/windows/hardware/ff547507)。

 

 

 





