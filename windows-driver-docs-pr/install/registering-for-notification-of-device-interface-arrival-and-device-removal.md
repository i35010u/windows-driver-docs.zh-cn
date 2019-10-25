---
title: 注册以获取设备接口到达和删除通知
description: 本主题介绍用户模式应用程序或驱动程序如何注册设备接口到达和设备删除的通知。
ms.assetid: 665E7881-F49C-4FC1-971C-1762B7D0C26E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7becd74e01b988f941195b180388d54589e91373
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837367"
---
# <a name="registering-for-notification-of-device-interface-arrival-and-device-removal"></a>注册获取设备接口到达和设备删除通知


本主题介绍用户模式应用程序或驱动程序如何注册设备接口到达和设备删除的通知。

通常，用户模式组件会调用[**CM_Register_Notification**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification)来查找设备接口，然后将 i/o 请求发送到接口。 为此，组件将注册**CM_NOTIFY_FILTER_TYPE_DEVICEINTERFACE**和**CM_NOTIFY_FILTER_TYPE_DEVICEHANDLE**，以便分别通知设备接口到达和设备删除。 调用序列可能如下所示。

**注册获取设备接口到达和设备删除通知**

1. 通过**CM_NOTIFY_FILTER_TYPE_DEVICEINTERFACE**调用[**CM_Register_Notification**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification)注册设备接口到达通知。 当指定类中的未来接口到达时，系统将通知你的组件。
2. 由于你想要向其发送 i/o 的接口可能已经存在于系统上，因此调用[**CM_Get_Device_Interface_List**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_interface_lista)或[**SetupDiGetClassDevs**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)来检索现有接口的列表。
   **注意** 如果接口到达步骤1和步骤2之间，接口将列出两次，从步骤1中的注册和步骤2中的接口列表。

     

3. 找到所需的接口后，调用[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)打开设备的句柄。
4. 在步骤3中成功创建设备句柄之后，请再次调用[**CM_Register_Notification**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification) 。 这一次，注册**CM_NOTIFY_FILTER_TYPE_DEVICEHANDLE**类型的通知，并提供新设备句柄作为接收通知的句柄。 当接口表示的设备接收查询删除请求时，系统会通知你的组件。

5. 实现设备句柄通知回调时，请使用此表。

   <div class="mx-tableFixed">
   <table>
   <colgroup>
   <col width="50%" />
   <col width="50%" />
   </colgroup>
   <thead>
   <tr class="header">
   <th align="left">回调接收的操作值</th>
   <th align="left">组件应执行的操作</th>
   </tr>
   </thead>
   <tbody>
   <tr class="odd">
   <td align="left"><strong>CM_NOTIFY_ACTION_DEVICEQUERYREMOVE</strong></td>
   <td align="left"><p>调用<a href="https://docs.microsoft.com/windows/desktop/api/handleapi/nf-handleapi-closehandle" data-raw-source="[CloseHandle](https://docs.microsoft.com/windows/desktop/api/handleapi/nf-handleapi-closehandle)">CloseHandle</a>关闭设备句柄。 如果未执行此操作，打开的句柄会阻止查询删除此设备。</p></td>
   </tr>
   <tr class="even">
   <td align="left"><strong>CM_NOTIFY_ACTION_DEVICEQUERYREMOVEFAILED</strong></td>
   <td align="left"><p>查询删除失败，因此设备及其接口仍然有效。 若要继续向接口发送 i/o，请打开该接口的新句柄。</p>
   <p>首先，通过调用<a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification" data-raw-source="[&lt;strong&gt;CM_Unregister_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)"><strong>CM_Unregister_Notification</strong></a>注销旧句柄的通知。 您必须从延迟的例程执行此操作，因为您无法从注册的通知句柄的通知回调调用<strong>CM_Unregister_Notification</strong> 。  有关详细信息，请参阅<a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification" data-raw-source="[&lt;strong&gt;CM_Unregister_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)"><strong>CM_Unregister_Notification</strong></a>的 "<strong>备注</strong>" 部分。</p>
   <p>然后，在延迟例程中继续，或在通知回调中返回<a href="https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea" data-raw-source="[&lt;strong&gt;CreateFile&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)"><strong>CreateFile</strong></a>以创建新句柄。 然后，用新的句柄和<strong>CM_NOTIFY_FILTER_TYPE_DEVICEHANDLE</strong>调用<a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification" data-raw-source="[&lt;strong&gt;CM_Register_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification)"><strong>CM_Register_Notification</strong></a> 。</p>
   <p>请注意，如果在发送<strong>CM_NOTIFY_ACTION_DEVICEQUERYREMOVE</strong>通知后，在正在删除查询的设备上注册通知，可能会收到<strong>CM_NOTIFY_ACTION_DEVICEQUERYREMOVEFAILED</strong>通知，而不首先接收<strong>CM_NOTIFY_ACTION_DEVICEQUERYREMOVE</strong>通知。</p></td>
   </tr>
   <tr class="odd">
   <td align="left"><strong>CM_NOTIFY_ACTION_DEVICEREMOVEPENDING</strong></td>
   <td align="left"><p>调用<a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification" data-raw-source="[&lt;strong&gt;CM_Unregister_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)"><strong>CM_Unregister_Notification</strong></a>为句柄注销通知。 必须从延迟例程执行此操作。  有关详细信息，请参阅<a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification" data-raw-source="[&lt;strong&gt;CM_Unregister_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)"><strong>CM_Unregister_Notification</strong></a>的 "<strong>备注</strong>" 部分。  如果仍有设备的打开句柄，请调用<a href="https://docs.microsoft.com/windows/desktop/api/handleapi/nf-handleapi-closehandle" data-raw-source="[&lt;strong&gt;CloseHandle&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/handleapi/nf-handleapi-closehandle)"><strong>CloseHandle</strong></a>关闭设备句柄。</p></td>
   </tr>
   <tr class="even">
   <td align="left"><strong>CM_NOTIFY_ACTION_DEVICEREMOVECOMPLETE</strong></td>
   <td align="left"><p>调用<a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification" data-raw-source="[&lt;strong&gt;CM_Unregister_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)"><strong>CM_Unregister_Notification</strong></a>为句柄注销通知。 必须从延迟例程执行此操作。  有关详细信息，请参阅<a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification" data-raw-source="[&lt;strong&gt;CM_Unregister_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)"><strong>CM_Unregister_Notification</strong></a>的 "<strong>备注</strong>" 部分。  如果仍有设备的打开句柄，请调用<a href="https://docs.microsoft.com/windows/desktop/api/handleapi/nf-handleapi-closehandle" data-raw-source="[&lt;strong&gt;CloseHandle&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/handleapi/nf-handleapi-closehandle)"><strong>CloseHandle</strong></a>关闭设备句柄。</p></td>
   </tr>
   </tbody>
   </table>
   </div>
     

6. 完成设备后，调用[**CM_Unregister_Notification**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)注销在步骤1中注册的接口通知回调。

如果在 UMDF 2 驱动程序中遵循此过程，请参阅[使用设备接口](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-device-interfaces)获取代码示例。 UMDF 2 驱动程序可以在驱动程序的[*EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调例程中执行步骤1-4，并在驱动程序的设备删除回调例程之一中执行步骤6。

## <a name="related-topics"></a>相关主题


[**CM_Register_Notification**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification)

[**CM_Unregister_Notification**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)

[使用设备接口](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-device-interfaces)

 

 






