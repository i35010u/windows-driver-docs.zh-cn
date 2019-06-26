---
title: 注册的设备接口到达和删除通知
description: 本主题介绍如何用户模式应用程序或驱动程序注册的设备接口到达和删除设备的通知。
ms.assetid: 665E7881-F49C-4FC1-971C-1762B7D0C26E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a99928673cc2d9fa92228d0be366854b1dc2631c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387324"
---
# <a name="registering-for-notification-of-device-interface-arrival-and-device-removal"></a>注册获取设备接口到达和设备删除通知


本主题介绍如何用户模式应用程序或驱动程序注册的设备接口到达和删除设备的通知。

通常，用户模式组件会调用[ **CM_Register_Notification** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification)以查找设备接口，然后发送到接口的 I/O 请求。 若要执行此操作，该组件注册两个**CM_NOTIFY_FILTER_TYPE_DEVICEINTERFACE**并**CM_NOTIFY_FILTER_TYPE_DEVICEHANDLE**，设备接口到达和设备删除的通知分别。 调用的序列可能如下所示。

**注册的设备接口到达和设备删除通知**

1. 调用[ **CM_Register_Notification** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification)与**CM_NOTIFY_FILTER_TYPE_DEVICEINTERFACE**以注册设备接口到达通知。 当在指定类中的未来接口，则系统会通知你的组件。
2. 因为你想要将 I/O 发送到可能已的接口会显示在系统上，调用[ **CM_Get_Device_Interface_List** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_interface_lista)或[ **SetupDiGetClassDevs**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)来检索现有接口的列表。
   **请注意**接口到达之间步骤 1 和步骤 2 时，如果接口是两次列出，从步骤 1 和步骤 2 中的接口列表中的注册。

     

3. 找到你所需的接口，之后，立即调用[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)打开设备的句柄。
4. 已成功在步骤 3 中创建设备句柄之后, 调用[ **CM_Register_Notification** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification)第二次。 这一次，注册类型的通知**CM_NOTIFY_FILTER_TYPE_DEVICEHANDLE**，并提供新设备句柄作为要为其接收通知的句柄。 由接口表示设备何时收到查询中删除请求，则系统会通知你的组件。

5. 使用此表，因为实现你的设备句柄通知回调。

   <div class="mx-tableFixed">
   <table>
   <colgroup>
   <col width="50%" />
   <col width="50%" />
   </colgroup>
   <thead>
   <tr class="header">
   <th align="left">操作值回调接收</th>
   <th align="left">在组件应执行的操作</th>
   </tr>
   </thead>
   <tbody>
   <tr class="odd">
   <td align="left"><strong>CM_NOTIFY_ACTION_DEVICEQUERYREMOVE</strong></td>
   <td align="left"><p>调用<a href="https://docs.microsoft.com/windows/desktop/api/handleapi/nf-handleapi-closehandle" data-raw-source="[CloseHandle](https://docs.microsoft.com/windows/desktop/api/handleapi/nf-handleapi-closehandle)">CloseHandle</a>关闭设备句柄。 如果不这样做，开放句柄将阻止此设备的查询删除成功。</p></td>
   </tr>
   <tr class="even">
   <td align="left"><strong>CM_NOTIFY_ACTION_DEVICEQUERYREMOVEFAILED</strong></td>
   <td align="left"><p>查询删除失败，因此仍然有效，设备和它的接口。 若要继续将 I/O 发送到接口，请打开它的新句柄。</p>
   <p>首先，通过调用取消注册旧句柄的通知<a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification" data-raw-source="[&lt;strong&gt;CM_Unregister_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)"> <strong>CM_Unregister_Notification</strong></a>。 因为不能调用时，必须执行此延迟例程从操作<strong>CM_Unregister_Notification</strong>从通知回调通知句柄，您的注册。  请参阅<strong>备注</strong>一部分<a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification" data-raw-source="[&lt;strong&gt;CM_Unregister_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)"> <strong>CM_Unregister_Notification</strong> </a>有关详细信息。</p>
   <p>然后，任一继续在延迟的例程中，或在通知回调中，调用返回<a href="https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea" data-raw-source="[&lt;strong&gt;CreateFile&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)"> <strong>CreateFile</strong> </a>若要创建新的句柄。 然后调用<a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification" data-raw-source="[&lt;strong&gt;CM_Register_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification)"> <strong>CM_Register_Notification</strong> </a>具有新的句柄并<strong>CM_NOTIFY_FILTER_TYPE_DEVICEHANDLE</strong>。</p>
   <p>请注意，是否你注册正处于被的设备上的通知查询删除后<strong>CM_NOTIFY_ACTION_DEVICEQUERYREMOVE</strong>已发送通知，则可能会收到<strong>CM_NOTIFY_ACTION_DEVICEQUERYREMOVEFAILED</strong>不包含第一个接收通知<strong>CM_NOTIFY_ACTION_DEVICEQUERYREMOVE</strong>通知。</p></td>
   </tr>
   <tr class="odd">
   <td align="left"><strong>CM_NOTIFY_ACTION_DEVICEREMOVEPENDING</strong></td>
   <td align="left"><p>调用<a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification" data-raw-source="[&lt;strong&gt;CM_Unregister_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)"> <strong>CM_Unregister_Notification</strong> </a>取消注册你的句柄的通知。 从延迟例程，必须执行此操作。  请参阅<strong>备注</strong>一部分<a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification" data-raw-source="[&lt;strong&gt;CM_Unregister_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)"> <strong>CM_Unregister_Notification</strong> </a>有关详细信息。  如果您仍然可以在设备的打开句柄，则调用<a href="https://docs.microsoft.com/windows/desktop/api/handleapi/nf-handleapi-closehandle" data-raw-source="[&lt;strong&gt;CloseHandle&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/handleapi/nf-handleapi-closehandle)"> <strong>CloseHandle</strong> </a>关闭设备句柄。</p></td>
   </tr>
   <tr class="even">
   <td align="left"><strong>CM_NOTIFY_ACTION_DEVICEREMOVECOMPLETE</strong></td>
   <td align="left"><p>调用<a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification" data-raw-source="[&lt;strong&gt;CM_Unregister_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)"> <strong>CM_Unregister_Notification</strong> </a>取消注册你的句柄的通知。 从延迟例程，必须执行此操作。  请参阅<strong>备注</strong>一部分<a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification" data-raw-source="[&lt;strong&gt;CM_Unregister_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)"> <strong>CM_Unregister_Notification</strong> </a>有关详细信息。  如果您仍然可以在设备的打开句柄，则调用<a href="https://docs.microsoft.com/windows/desktop/api/handleapi/nf-handleapi-closehandle" data-raw-source="[&lt;strong&gt;CloseHandle&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/handleapi/nf-handleapi-closehandle)"> <strong>CloseHandle</strong> </a>关闭设备句柄。</p></td>
   </tr>
   </tbody>
   </table>
   </div>
     

6. 与设备完成后，调用[ **CM_Unregister_Notification** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)取消注册步骤 1 中注册的接口通知回调。

如果您按照此过程在 UMDF 2 驱动程序，请参阅[使用设备接口](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-device-interfaces)有关代码示例。 UMDF 2 驱动程序可能在驱动程序的执行步骤 1-4 [ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调例程和步骤 6 中的一个驱动程序的设备删除回调例程。

## <a name="related-topics"></a>相关主题


[**CM_Register_Notification**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification)

[**CM_Unregister_Notification**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)

[使用设备接口](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-device-interfaces)

 

 






