---
title: 静态驱动程序验证程序 KMDF 函数声明
description: 静态驱动程序验证程序 KMDF 函数声明
ms.assetid: 1623f3a4-e318-41b3-bbcf-d443202f31e6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de7ad984002ae400f44c22793d64aee8930f6303
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839313"
---
# <a name="static-driver-verifier-kmdf-function-declarations"></a>静态驱动程序验证程序 KMDF 函数声明


若要启用 SDV 来验证 KMDF 驱动程序，必须使用回调函数角色类型声明每个回调函数。 回调函数角色类型在各种 WDF 标头文件中定义，并在你用 Wdf .h 头文件生成驱动程序时包括在内。 下表显示了函数角色类型及其关联的事件回调函数。

必须在回调函数定义之前声明驱动程序的回调函数。 下面的示例显示了[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数的函数角色类型声明。 在此示例中，回调函数称为*EvtDriverDeviceAdd*。

```
#include <NTDDK.h>  
#include <wdf.h>
EVT_WDF_DRIVER_DEVICE_ADD EvtDriverDeviceAdd
```

如果回调函数具有函数原型声明，则必须将函数原型替换为函数角色类型声明。 有关函数角色类型声明的详细信息，请参阅[使用函数角色类型声明](using-function-role-type-declarations.md)。

下表显示了回调函数类型及其关联的事件回调函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数角色类型</th>
<th align="left">事件回调函数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>EVT_WDF_CHILD_LIST_ADDRESS_DESCRIPTION_CLEANUP</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_address_description_cleanup" data-raw-source="[&lt;em&gt;EvtChildListAddressDescriptionCleanup&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_address_description_cleanup)"><em>EvtChildListAddressDescriptionCleanup</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_CHILD_LIST_ADDRESS_DESCRIPTION_COPY</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_address_description_copy" data-raw-source="[&lt;em&gt;EvtChildListAddressDescriptionCopy&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_address_description_copy)"><em>EvtChildListAddressDescriptionCopy</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_CHILD_LIST_ADDRESS_DESCRIPTION_DUPLICATE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_identification_description_duplicate" data-raw-source="[&lt;em&gt;EvtChildListIdentificationDescriptionDuplicate&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_identification_description_duplicate)"><em>EvtChildListIdentificationDescriptionDuplicate</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_CHILD_LIST_CREATE_DEVICE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device" data-raw-source="[&lt;em&gt;EvtChildListCreateDevice&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device)"><em>EvtChildListCreateDevice</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_CHILD_LIST_DEVICE_REENUMERATED</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_device_reenumerated" data-raw-source="[&lt;em&gt;EvtChildListDeviceReenumerated&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_device_reenumerated)"><em>EvtChildListDeviceReenumerated</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_CHILD_LIST_IDENTIFICATION_DESCRIPTION_CLEANUP</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_identification_description_cleanup" data-raw-source="[&lt;em&gt;EvtChildListIdentificationDescriptionCleanup&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_identification_description_cleanup)"><em>EvtChildListIdentificationDescriptionCleanup</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_CHILD_LIST_IDENTIFICATION_DESCRIPTION_COMPARE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_identification_description_compare" data-raw-source="[&lt;em&gt;EvtChildListIdentificationDescriptionCompare&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_identification_description_compare)"><em>EvtChildListIdentificationDescriptionCompare</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_CHILD_LIST_IDENTIFICATION_DESCRIPTION_COPY</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_identification_description_copy" data-raw-source="[&lt;em&gt;EvtChildListIdentificationDescriptionCopy&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_identification_description_copy)"><em>EvtChildListIdentificationDescriptionCopy</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_CHILD_LIST_IDENTIFICATION_DESCRIPTION_DUPLICATE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_identification_description_duplicate" data-raw-source="[&lt;em&gt;EvtChildListIdentificationDescriptionDuplicate&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_identification_description_duplicate)"><em>EvtChildListIdentificationDescriptionDuplicate</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_CHILD_LIST_SCAN_FOR_CHILDREN</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_scan_for_children" data-raw-source="[&lt;em&gt;EvtChildListScanForChildren&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_scan_for_children)"><em>EvtChildListScanForChildren</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_ARM_WAKE_FROM_S0</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0" data-raw-source="[&lt;em&gt;EvtDeviceArmWakeFromS0&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0)"><em>EvtDeviceArmWakeFromS0</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_ARM_WAKE_FROM_SX</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx" data-raw-source="[&lt;em&gt;EvtDeviceArmWakeFromSx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx)"><em>EvtDeviceArmWakeFromSx</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_CONTEXT_CLEANUP</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup" data-raw-source="[&lt;em&gt;EvtCleanupCallback&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)"><em>EvtCleanupCallback</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_CONTEXT_DESTROY</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy" data-raw-source="[&lt;em&gt;EvtDestroyCallback&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)"><em>EvtDestroyCallback</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_D0_ENTRY</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry" data-raw-source="[&lt;em&gt;EvtDeviceD0Entry&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)"><em>EvtDeviceD0Entry</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_D0_ENTRY_POST_INTERRUPTS_ENABLED</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled" data-raw-source="[&lt;em&gt;EvtDeviceD0EntryPostInterruptsEnabled&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled)"><em>EvtDeviceD0EntryPostInterruptsEnabled</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_D0_EXIT</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit" data-raw-source="[&lt;em&gt;EvtDeviceD0Exit&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)"><em>EvtDeviceD0Exit</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_D0_EXIT_PRE_INTERRUPTS_DISABLED</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled" data-raw-source="[&lt;em&gt;EvtDeviceD0ExitPreInterruptsDisabled&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled)"><em>EvtDeviceD0ExitPreInterruptsDisabled</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_DISABLE_WAKE_AT_BUS</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus" data-raw-source="[&lt;em&gt;EvtDeviceDisableWakeAtBus&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus)"><em>EvtDeviceDisableWakeAtBus</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_DISARM_WAKE_FROM_S0</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_s0" data-raw-source="[&lt;em&gt;EvtDeviceDisarmWakeFromS0&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_s0)"><em>EvtDeviceDisarmWakeFromS0</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_DISARM_WAKE_FROM_SX</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_sx" data-raw-source="[&lt;em&gt;EvtDeviceDisarmWakeFromSx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_sx)"><em>EvtDeviceDisarmWakeFromSx</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_EJECT</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_eject" data-raw-source="[&lt;em&gt;EvtDeviceEject&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_eject)"><em>EvtDeviceEject</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_ENABLE_WAKE_AT_BUS</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_enable_wake_at_bus" data-raw-source="[&lt;em&gt;EvtDeviceEnableWakeAtBus&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_enable_wake_at_bus)"><em>EvtDeviceEnableWakeAtBus</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_FILE_CREATE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create" data-raw-source="[&lt;em&gt;EvtDeviceFileCreate&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)"><em>EvtDeviceFileCreate</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_FILTER_RESOURCE_REQUIREMENTS</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements" data-raw-source="[&lt;em&gt;EvtDeviceFilterAddResourceRequirements&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)"><em>EvtDeviceFilterAddResourceRequirements</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_PNP_STATE_CHANGE_NOTIFICATION</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_pnp_state_change_notification" data-raw-source="[&lt;em&gt;EvtDevicePnpStateChange&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_pnp_state_change_notification)"><em>EvtDevicePnpStateChange</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_POWER_POLICY_STATE_CHANGE_NOTIFICATION</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_pnp_state_change_notification" data-raw-source="[&lt;em&gt;EvtDevicePnpStateChange&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_pnp_state_change_notification)"><em>EvtDevicePnpStateChange</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_POWER_STATE_CHANGE_NOTIFICATION</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_power_state_change_notification" data-raw-source="[&lt;em&gt;EvtDevicePowerStateChange&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_power_state_change_notification)"><em>EvtDevicePowerStateChange</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_PREPARE_HARDWARE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)"><em>EvtDevicePrepareHardware</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_PROCESS_QUERY_INTERFACE_REQUEST</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfqueryinterface/nc-wdfqueryinterface-evt_wdf_device_process_query_interface_request" data-raw-source="[&lt;em&gt;EvtDeviceProcessQueryInterfaceRequest&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfqueryinterface/nc-wdfqueryinterface-evt_wdf_device_process_query_interface_request)"><em>EvtDeviceProcessQueryInterfaceRequest</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_QUERY_REMOVE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_remove" data-raw-source="[&lt;em&gt;EvtDeviceQueryRemove&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_remove)"><em>EvtDeviceQueryRemove</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_QUERY_STOP</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_stop" data-raw-source="[&lt;em&gt;EvtDeviceQueryStop&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_stop)"><em>EvtDeviceQueryStop</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_RELATIONS_QUERY</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_relations_query" data-raw-source="[&lt;em&gt;EvtDeviceRelationsQuery&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_relations_query)"><em>EvtDeviceRelationsQuery</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_RELEASE_HARDWARE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware" data-raw-source="[&lt;em&gt;EvtDeviceReleaseHardware&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)"><em>EvtDeviceReleaseHardware</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_REMOVE_ADDED_RESOURCES</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources" data-raw-source="[&lt;em&gt;EvtDeviceRemoveAddedResources&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources)"><em>EvtDeviceRemoveAddedResources</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_RESOURCE_REQUIREMENTS_QUERY</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query" data-raw-source="[&lt;em&gt;EvtDeviceResourceRequirementsQuery&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query)"><em>EvtDeviceResourceRequirementsQuery</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_RESOURCES_QUERY</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resources_query" data-raw-source="[&lt;em&gt;EvtDeviceResourcesQuery&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resources_query)"><em>EvtDeviceResourcesQuery</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_SELF_MANAGED_IO_CLEANUP</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoCleanup&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup)"><em>EvtDeviceSelfManagedIoCleanup</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_SELF_MANAGED_IO_FLUSH</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoFlush&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)"><em>EvtDeviceSelfManagedIoFlush</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_SELF_MANAGED_IO_INIT</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoInit&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)"><em>EvtDeviceSelfManagedIoInit</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_SELF_MANAGED_IO_RESTART</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoRestart&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart)"><em>EvtDeviceSelfManagedIoRestart</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_SELF_MANAGED_IO_SUSPEND</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoSuspend&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)"><em>EvtDeviceSelfManagedIoSuspend</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_SET_LOCK</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_set_lock" data-raw-source="[&lt;em&gt;EvtDeviceSetLock&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_set_lock)"><em>EvtDeviceSetLock</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_SHUTDOWN_NOTIFICATION</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nc-wdfcontrol-evt_wdf_device_shutdown_notification" data-raw-source="[&lt;em&gt;EvtDeviceShutdownNotification&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nc-wdfcontrol-evt_wdf_device_shutdown_notification)"><em>EvtDeviceShutdownNotification</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_SURPRISE_REMOVAL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal" data-raw-source="[&lt;em&gt;EvtDeviceSurpriseRemoval&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)"><em>EvtDeviceSurpriseRemoval</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_USAGE_NOTIFICATION</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_usage_notification" data-raw-source="[&lt;em&gt;EvtDeviceUsageNotification&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_usage_notification)"><em>EvtDeviceUsageNotification</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_WAKE_FROM_S0_TRIGGERED</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_wake_from_s0_triggered" data-raw-source="[&lt;em&gt;EvtDeviceWakeFromS0Triggered&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_wake_from_s0_triggered)"><em>EvtDeviceWakeFromS0Triggered</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_WAKE_FROM_SX_TRIGGERED</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_wake_from_sx_triggered" data-raw-source="[&lt;em&gt;EvtDeviceWakeFromSxTriggered&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_wake_from_sx_triggered)"><em>EvtDeviceWakeFromSxTriggered</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DMA_ENABLER_DISABLE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable" data-raw-source="[&lt;em&gt;EvtDmaEnablerDisable&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable)"><em>EvtDmaEnablerDisable</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DMA_ENABLER_ENABLE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable" data-raw-source="[&lt;em&gt;EvtDmaEnablerEnable&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable)"><em>EvtDmaEnablerEnable</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DMA_ENABLER_FILL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill" data-raw-source="[&lt;em&gt;EvtDmaEnablerFill&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill)"><em>EvtDmaEnablerFill</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DMA_ENABLER_FLUSH</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush" data-raw-source="[&lt;em&gt;EvtDmaEnablerFlush&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush)"><em>EvtDmaEnablerFlush</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DMA_ENABLER_SELFMANAGED_IO_START</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStart&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start)"><em>EvtDmaEnablerSelfManagedIoStart</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DMA_ENABLER_SELFMANAGED_IO_STOP</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStop&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop)"><em>EvtDmaEnablerSelfManagedIoStop</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DPC</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc" data-raw-source="[&lt;em&gt;EvtDpcFunc&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc)"><em>EvtDpcFunc</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DRIVER_DEVICE_ADD</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add" data-raw-source="[&lt;em&gt;EvtDriverDeviceAdd&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)"><em>EvtDriverDeviceAdd</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DRIVER_UNLOAD</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload" data-raw-source="[&lt;em&gt;EvtDriverUnload&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)"><em>EvtDriverUnload</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_FILE_CLEANUP</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_cleanup" data-raw-source="[&lt;em&gt;EvtFileCleanup&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_cleanup)"><em>EvtFileCleanup</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_FILE_CLOSE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_close" data-raw-source="[&lt;em&gt;EvtFileClose&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_close)"><em>EvtFileClose</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_FILE_CONTEXT_CLEANUP_CALLBACK</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup" data-raw-source="[&lt;em&gt;EvtCleanupCallback&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)"><em>EvtCleanupCallback</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_FILE_CONTEXT_DESTROY_CALLBACK</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy" data-raw-source="[&lt;em&gt;EvtDestroyCallback&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)"><em>EvtDestroyCallback</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_INTERRUPT_DISABLE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable" data-raw-source="[&lt;em&gt;EvtInterruptDisable&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)"><em>EvtInterruptDisable</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_INTERRUPT_DPC</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc" data-raw-source="[&lt;em&gt;EvtInterruptDpc&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)"><em>EvtInterruptDpc</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_INTERRUPT_ENABLE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable" data-raw-source="[&lt;em&gt;EvtInterruptEnable&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)"><em>EvtInterruptEnable</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_INTERRUPT_ISR</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr" data-raw-source="[&lt;em&gt;EvtInterruptIsr&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)"><em>EvtInterruptIsr</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_INTERRUPT_SYNCHRONIZE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_synchronize" data-raw-source="[&lt;em&gt;EvtInterruptSynchronize&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_synchronize)"><em>EvtInterruptSynchronize</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_IN_CALLER_CONTEXT</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context" data-raw-source="[&lt;em&gt;EvtIoInCallerContext&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)"><em>EvtIoInCallerContext</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_IO_QUEUE_CONTEXT_CLEANUP_CALLBACK</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup" data-raw-source="[&lt;em&gt;EvtCleanupCallback&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)"><em>EvtCleanupCallback</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_QUEUE_CONTEXT_DESTROY_CALLBACK</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy" data-raw-source="[&lt;em&gt;EvtDestroyCallback&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)"><em>EvtDestroyCallback</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_CANCELED_ON_QUEUE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_canceled_on_queue" data-raw-source="[&lt;em&gt;EvtIoCanceledOnQueue&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_canceled_on_queue)"><em>EvtIoCanceledOnQueue</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_DEFAULT</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default" data-raw-source="[&lt;em&gt;EvtIoDefault&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)"><em>EvtIoDefault</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_DEVICE_CONTROL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)"><em>EvtIoDeviceControl</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_INTERNAL_DEVICE_CONTROL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)"><em>EvtIoInternalDeviceControl</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_READ</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"><em>EvtIoRead</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_RESUME</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume" data-raw-source="[&lt;em&gt;EvtIoResume&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume)"><em>EvtIoResume</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_STOP</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>EvtIoStop</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_WRITE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"><em>EvtIoWrite</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_IO_QUEUE_STATE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_state" data-raw-source="[&lt;em&gt;EvtIoQueueState&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_state)"><em>EvtIoQueueState</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_TARGET_QUERY_REMOVE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_query_remove" data-raw-source="[&lt;em&gt;EvtIoTargetQueryRemove&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_query_remove)"><em>EvtIoTargetQueryRemove</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_IO_TARGET_REMOVE_CANCELED</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_remove_canceled" data-raw-source="[&lt;em&gt;EvtIoTargetRemoveCanceled&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_remove_canceled)"><em>EvtIoTargetRemoveCanceled</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_TARGET_REMOVE_COMPLETE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_remove_complete" data-raw-source="[&lt;em&gt;EvtIoTargetRemoveComplete&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_remove_complete)"><em>EvtIoTargetRemoveComplete</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_OBJECT_CONTEXT_CLEANUP</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup" data-raw-source="[&lt;em&gt;EvtCleanupCallback&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)"><em>EvtCleanupCallback</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_OBJECT_CONTEXT_DESTROY</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_PROGRAM_DMA</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma" data-raw-source="[&lt;em&gt;EvtProgramDma&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)"><em>EvtProgramDma</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_REQUEST_CANCEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel" data-raw-source="[&lt;em&gt;EvtRequestCancel&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)"><em>EvtRequestCancel</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_REQUEST_COMPLETION_ROUTINE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine" data-raw-source="[&lt;em&gt;CompletionRoutine&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)"><em>CompletionRoutine</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_TIMER</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/nc-wdftimer-evt_wdf_timer" data-raw-source="[&lt;em&gt;EvtTimerFunc&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/nc-wdftimer-evt_wdf_timer)"><em>EvtTimerFunc</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_TRACE_CALLBACK</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_WMI_INSTANCE_EXECUTE_METHOD</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_execute_method" data-raw-source="[&lt;em&gt;EvtWmiInstanceExecuteMethod&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_execute_method)"><em>EvtWmiInstanceExecuteMethod</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_WMI_INSTANCE_QUERY_INSTANCE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_query_instance" data-raw-source="[&lt;em&gt;EvtWmiInstanceQueryInstance&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_query_instance)"><em>EvtWmiInstanceQueryInstance</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_WMI_INSTANCE_SET_INSTANCE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_set_instance" data-raw-source="[&lt;em&gt;EvtWmiInstanceSetInstance&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_set_instance)"><em>EvtWmiInstanceSetInstance</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_WMI_INSTANCE_SET_ITEM</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_set_item" data-raw-source="[&lt;em&gt;EvtWmiInstanceSetItem&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_set_item)"><em>EvtWmiInstanceSetItem</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_WMI_PROVIDER_FUNCTION_CONTROL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_provider_function_control" data-raw-source="[&lt;em&gt;EvtWmiProviderFunctionControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_provider_function_control)"><em>EvtWmiProviderFunctionControl</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_WORKITEM</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem" data-raw-source="[&lt;em&gt;EvtWorkItem&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)"><em>EvtWorkItem</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDFDEVICE_WDM_IRP_PREPROCESS</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"><em>EvtDeviceWdmIrpPreprocess</em></a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idfunction_role_types_that_allow_multiple_callback_functionsspanspan-idfunction_role_types_that_allow_multiple_callback_functionsspanfunction-role-types-that-allow-multiple-callback-functions"></a><span id="function_role_types_that_allow_multiple_callback_functions"></span><span id="FUNCTION_ROLE_TYPES_THAT_ALLOW_MULTIPLE_CALLBACK_FUNCTIONS"></span>允许多个回调函数的函数角色类型

有一些函数角色类型可以有多个与之关联的事件回调函数。 例如，驱动程序可能有多个[*EvtTimerFunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/nc-wdftimer-evt_wdf_timer)或[*EvtDpcFunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc)回调函数。 下表显示了 SDV 支持的每个函数角色类型的最大回调数。 尽管驱动程序的驱动程序数量超过了表中列出的最大回调函数数量，但使用 SDV 时，它会使验证过程复杂化。 有关可能需要对 Sdv 文件进行的更改以容纳其他回调函数的信息，请参阅[函数角色类型的重复入口点](duplicate-entry-points-for-a-function-role-type.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数角色类型</th>
<th align="left">最大回调函数数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>EVT_WDF_DPC</p></td>
<td align="left"><p>7</p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_INTERRUPT_SYNCHRONIZE</p></td>
<td align="left"><p>11</p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_TIMER</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_WMI_INSTANCE_EXECUTE_METHOD</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_WMI_INSTANCE_QUERY_INSTANCE</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_WMI_INSTANCE_SET_INSTANCE</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_WMI_INSTANCE_SET_ITEM</p></td>
<td align="left"><p>5</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idfunction_role_types_and_i_o_queuesspanspan-idfunction_role_types_and_i_o_queuesspanfunction-role-types-and-io-queues"></a><span id="function_role_types_and_i_o_queues"></span><span id="FUNCTION_ROLE_TYPES_AND_I_O_QUEUES"></span>函数角色类型和 i/o 队列

在声明依赖于 KMDF 框架的[请求处理](https://go.microsoft.com/fwlink/p/?linkid=153345)程序和回调函数以将 i/o 请求传递给驱动程序（对于顺序或并行调度）时，请使用以下函数角色类型。 不要将这些函数角色类型用于手动将请求从默认队列转发到其他队列（手动分派）的函数。 SDV 不支持允许它跟踪从一个队列到另一个队列的请求的内存模型。

有关 i/o 队列的详细信息，请参阅[创建 I/o 队列](https://go.microsoft.com/fwlink/p/?linkid=153346)。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">用于为手动分派配置的 i/o 队列的函数角色类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_QUEUE_CONTEXT_CLEANUP_CALLBACK</p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_IO_QUEUE_CONTEXT_DESTROY_CALLBACK</p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_CANCELED_ON_QUEUE</p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_DEFAULT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_DEVICE_CONTROL</p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_INTERNAL_DEVICE_CONTROL</p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_READ</p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_RESUME</p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_STOP</p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_WRITE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_QUEUE_STATE</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idfunction_role_types_for_the_evtcleanupcallback_and_evtdestroycallback_spanspan-idfunction_role_types_for_the_evtcleanupcallback_and_evtdestroycallback_spanfunction-role-types-for-the-evtcleanupcallback-and-evtdestroycallback-functions"></a><span id="function_role_types_for_the_evtcleanupcallback_and_evtdestroycallback_"></span><span id="FUNCTION_ROLE_TYPES_FOR_THE_EVTCLEANUPCALLBACK_AND_EVTDESTROYCALLBACK_"></span>EvtCleanupCallback 和 EvtDestroyCallback 函数的函数角色类型

必须将[*EvtCleanupCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)和[*EvtDestroyCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)函数声明为特定于对象的函数角色类型。 SDV 需要这些特定于对象的角色类型来确定驱动程序是否正确使用了回调函数。 使用下表来确定要使用的函数类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">对象类型</th>
<th align="left">EvtCleanupCallback 的函数角色类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>设备对象</p></td>
<td align="left"><p>EVT_WDF_DEVICE_CONTEXT_CLEANUP</p></td>
</tr>
<tr class="even">
<td align="left"><p>I/o 队列对象</p></td>
<td align="left"><p>EVT_WDF_IO_QUEUE_CONTEXT_CLEANUP_CALLBACK</p></td>
</tr>
<tr class="odd">
<td align="left"><p>File 对象</p></td>
<td align="left"><p>EVT_WDF_FILE_CONTEXT_CLEANUP_CALLBACK</p></td>
</tr>
<tr class="even">
<td align="left"><p>所有其他对象</p></td>
<td align="left"><p>EVT_WDF_OBJECT_CONTEXT_CLEANUP</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">对象类型</th>
<th align="left">EvDestroyCallback 的函数角色类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>设备对象</p></td>
<td align="left"><p>EVT_WDF_DEVICE_CONTEXT_DESTROY</p></td>
</tr>
<tr class="even">
<td align="left"><p>I/o 队列对象</p></td>
<td align="left"><p>EVT_WDF_IO_QUEUE_CONTEXT_DESTROY_CALLBACK</p></td>
</tr>
<tr class="odd">
<td align="left"><p>File 对象</p></td>
<td align="left"><p>EVT_WDF_FILE_CONTEXT_DESTROY_CALLBACK</p></td>
</tr>
<tr class="even">
<td align="left"><p>所有其他对象</p></td>
<td align="left"><p>EVT_WDF_OBJECT_CONTEXT_DESTROY</p></td>
</tr>
</tbody>
</table>

 

 

 





