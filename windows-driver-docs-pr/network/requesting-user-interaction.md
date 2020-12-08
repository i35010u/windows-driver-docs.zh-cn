---
title: 请求用户交互
description: 请求用户交互
keywords:
- 用户交互 WDK 本机 802.11 IHV 扩展 DLL
- 请求用户交互 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98abb846c15d85bbc01859ff341ab6c1b888d23a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791375"
---
# <a name="requesting-user-interaction"></a>请求用户交互




 

在调用 [*Dot11ExtIhvInitAdapter*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_adapter)之后的任何时候，IHV 扩展 DLL 都可以通过调用 [**Dot11ExtSendUIRequest**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request) 函数请求与用户交互。 操作系统将所有用户交互请求转发到 IHV UI 扩展 DLL，该 DLL 将处理请求，并向用户显示相应的用户界面 (UI) 页面。

请求完成后，操作系统将调用 [*Dot11ExtIhvProcessUIResponse*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_process_ui_response) 函数，以便从 IHV UI 扩展 DLL 转发用于用户交互的结果。 有关 IHV UI 扩展 DLL 的详细信息，请参阅 [本机 802.11 IHV Ui 扩展 dll](native-802-11-ihv-ui-extensions-dll2.md)。

例如，对于以下任何情况，IHV 扩展 DLL 都可以请求用户交互。

-   通知用户有关前或后关联操作的阶段。

-   提示用户输入其凭据，以便在之后的关联操作期间进行身份验证。

如果调用 [**Dot11ExtSendUIRequest**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request) 函数，则 IHV 扩展 DLL 会将指向 [**DOT11EXT \_ IHV \_ UI \_ 请求**](/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_ui_request) 结构的指针传递到 *pIhvUIRequest* 参数。 DOT11EXT \_ IHV \_ UI \_ 请求结构指定请求，例如全局唯一 ID (GUID) ，它标识 UI 请求以及将处理此请求的目标 UI 页的 COM 类 id (CLSID) 。

当 IHV UI 扩展 DLL 完成用户通知后，操作系统将调用 [*Dot11ExtIhvProcessUIResponse*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_process_ui_response) 函数。 如果用户已通过通知进入了任何数据，操作系统会将指向包含数据的缓冲区的指针传递到 *pvResponseBuffer* 参数。

操作系统可能会定期查询挂起通知请求的状态。 在这种情况下，操作系统将调用 [*Dot11ExtIhvIsUIRequestPending*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_is_ui_request_pending) ，并将 UI 请求的 GUID 传递给 *guidUIRequest* 参数。

调用 [**Dot11ExtSendUIRequest**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request)时，IHV 扩展 DLL 必须遵循这些准则。

-   IHV 扩展 DLL 不需要序列化对 [**Dot11ExtSendUIRequest**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request)的调用。 DLL 可随时有多个挂起的 UI 请求。

-   仅当为 GUID 调用了 [*Dot11ExtIhvProcessUIResponse*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_process_ui_response) 时，才会完成特定 GUID 的 UI 请求。 在这种情况下，在调用 *Dot11ExtIhvProcessUIResponse* 之前，IHV 扩展 DLL 不得为 UI 请求释放所有已分配的资源。

-   调用 [*Dot11ExtIhvAdapterReset*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_adapter_reset) 或 [*Dot11ExtIhvDeinitAdapter*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter) 时，将取消所有挂起的 UI 请求。 当调用 [*Dot11ExtIhvProcessSessionChange*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_process_session_change) 时，如果将 *uEventType* 参数设置为 WTS 会话注销，则还会取消所有挂起的 UI 请求 \_ \_ 。

    在这些情况下，IHV 扩展 DLL 必须释放所有已分配的资源，以便为每个挂起的 UI 请求。

每当基本服务集上的连接状态发生更改时，操作系统就会启动用户交互， (BSS) 网络。 在这种情况下，操作系统将调用 [*Dot11ExtIhvQueryUIRequest*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_query_ui_request) 函数。 IHV 扩展 DLL 分配一个缓冲区，并将其格式化为 [**DOT11EXT \_ IHV \_ UI \_ 请求**](/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_ui_request) 结构。 DLL 将 DOT11EXT \_ IHV \_ UI 请求结构的成员设置 \_ 为引用适用于连接状态更改的 UI 页。 操作系统负责显示 UI 页。

**注意** IHV 扩展必须通过 [**Dot11ExtAllocateBuffer**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_allocate_buffer)分配包含 [**DOT11EXT \_ IHV \_ UI \_ 请求**](/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_ui_request)结构的缓冲区。 在从 [*Dot11ExtIhvQueryUIRequest*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_query_ui_request)返回后，DLL 不得释放缓冲区。

 

 

 
