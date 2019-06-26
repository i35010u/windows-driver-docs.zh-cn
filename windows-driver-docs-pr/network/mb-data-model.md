---
title: MB 数据模型
description: MB 数据模型
ms.assetid: 922b6b55-c332-4721-bbd1-571b0e154df3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03efe34af831856edbdf568c12d52e365aca5701
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379409"
---
# <a name="mb-data-model"></a>MB 数据模型


MB 驱动程序模型使用的对象定义为抽象的 MB 设备功能的一组组成的数据模型。 每个对象的唯一对象标识符 (OID) 标识，由相应的属性的一组定义。 一组属性组织到一个数据结构。 若要管理设备，MB 服务和 MB 微型端口驱动程序交换 Oid 和基于 OID 请求并提供通过网络驱动程序接口规范 (NDIS) 指示其关联的数据结构。

在 MB 驱动程序模型中，仅*设置*并*查询*操作用于 OID 请求。 MB 驱动程序模型不使用*方法*操作。 迹象，MB 驱动程序模型将使用事件和事务通知来指示的 MB 设备对象中的状态更改。 事务通知还指示异步事务已完成。

下表列出的 Oid 和状态指示为 MB 微型端口驱动程序，以及关联的数据结构定义。 MB 微型端口驱动程序必须实现所有必需的常规 Oid 的 NDIS 6.20 规范要求。 有关一系列常规 Oid ndis 6.x，请参阅[常规操作 Oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/index)。

此外，MB 微型端口驱动程序必须实现 OID\_GEN\_物理\_中等即使 NDIS 规范描述为可选实现也是如此。

中所述的语法和语义下表中列出了 MB Oid [MB 的操作语义](mb-operational-semantics.md)。 MB 服务和 MB 微型端口驱动程序之间的交互中所述[MB 操作流程图](mb-operation-flowcharts.md)。

## <a name="wwan-specific-oids"></a>特定于 WWAN 的 Oid

| OID 和相应的数据结构 | 设置操作 |   | 查询操作 |   | GSM/CDMA |
| ---                                  | ---       | ---       | ---       | ---       |--- |
|                                      | Windows 7 | Windows 8 | Windows 7 | Windows 8 |    |
| [OID\_WWAN\_驱动程序\_CAP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-driver-caps)使用[ **NDIS\_WWAN\_驱动程序\_CAP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_driver_caps) | 不支持 | 不支持 |S | S | GSM, CDMA |
| [OID\_WWAN\_设备\_CAPS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps)没有相应的结构 | 不支持 | 不支持 | A | A | GSM, CDMA |
| [OID\_WWAN\_准备\_信息](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ready-info)没有相应的结构 | 不支持的不受支持 | A | A | GSM, CDMA |
| [OID\_WWAN\_服务\_激活](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-service-activation)† 使用[ **NDIS\_WWAN\_服务\_激活**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_service_activation) | A | A | 不支持 | 不支持 | GSM, CDMA |
| [OID\_WWAN\_单选\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-radio-state)使用[ **NDIS\_WWAN\_设置\_单选\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_radio_state) | A | A | A | A | GSM, CDMA |
| [OID\_WWAN\_PIN](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin)使用[ **NDIS\_WWAN\_设置\_PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin) | A | 不支持 | A | 不支持 | GSM, CDMA |
| [OID\_WWAN\_PIN\_列表](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin-list)没有相应的结构 | 不支持 | 不支持 | A | A | GSM, CDMA |
| [OID\_WWAN\_PIN\_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin-ex)使用[ **NDIS\_WWAN\_设置\_PIN\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin_ex) | 不支持 | A | 不支持 | A | GSM, CDMA |
| [OID\_WWAN\_主页\_提供程序](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-home-provider)没有相应的结构 | 不支持 | 不支持 | A | A | GSM, CDMA |
| [OID\_WWAN\_PREFERRED\_提供程序](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-preferred-providers)† 使用[ **NDIS\_WWAN\_设置\_首选\_提供程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_preferred_providers) | A | A | A | A | 仅使用 GSM |
| [OID\_WWAN\_VISIBLE\_提供程序](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-visible-providers)没有相应的结构 | 不支持 | 不支持 | A | A | GSM |
| [OID\_WWAN\_注册\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-register-state)使用[ **NDIS\_WWAN\_设置\_注册\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_register_state) | A | A | A | A | CDMA |
| [OID\_WWAN\_信号\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-signal-state)使用[ **NDIS\_WWAN\_设置\_信号\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_signal_indication) | A | A | A | A | GSM, CDMA |
| [OID\_WWAN\_数据包\_服务](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-packet-service)使用[ **NDIS\_WWAN\_设置\_数据包\_服务**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_packet_service) | A | A | A | A | GSM, CDMA |
| [OID\_WWAN\_已预配\_上下文](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-provisioned-contexts)† 使用[ **NDIS\_WWAN\_设置\_已预配\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_provisioned_context) | A | A | A | A | GSM, CDMA |
| [OID\_WWAN\_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-connect)使用[ **NDIS\_WWAN\_设置\_上下文\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_context_state) | A | A | A | A | GSM, CDMA |
| [OID\_WWAN\_SMS\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-configuration)使用[ **NDIS\_WWAN\_设置\_SMS\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sms_configuration) | A | A | A | A | GSM, CDMA | 
| [OID\_WWAN\_SMS\_读取](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-read)使用[ **NDIS\_WWAN\_SMS\_读取**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_read) | 不支持 | A | A | A |GSM, CDMA | 
| [OID\_WWAN\_SMS\_发送](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-send)使用[ **NDIS\_WWAN\_SMS\_发送**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send) | A | A | 不支持 | 不支持 | GSM, CDMA |
| [OID\_WWAN\_SMS\_删除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-delete)使用[ **NDIS\_WWAN\_SMS\_删除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete) | A | A | 不支持 | 不支持 |  GSM, CDMA |
| [OID\_WWAN\_SMS\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-status)使用[ **NDIS\_WWAN\_SMS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_status) | 不支持 | 不支持 | A | A | GSM, CDMA |
| [OID\_WWAN\_供应商\_特定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-vendor-specific)† 使用供应商定义的结构 | A | A | 不支持 | 不支持 | GSM, CDMA |
| [OID\_WWAN\_设备\_服务](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-services)没有相应的结构 | 不支持 | 不支持 | 不支持 | A | GSM, CDMA |
| [OID\_WWAN\_SUBSCRIBE\_设备\_服务\_事件](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-subscribe-device-service-events)使用[ **NDIS\_WWAN\_订阅\_设备\_服务\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_subscribe_device_service_events) | 不支持 | A | 不支持 | 不支持 | GSM, CDMA |
| [OID\_WWAN\_身份验证\_质询](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-auth-challenge)使用[ **NDIS\_WWAN\_身份验证\_质询**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_auth_challenge) | 不支持 | 不支持 | 不支持 | A | GSM, CDMA |
| [OID\_WWAN\_USSD](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ussd)使用[ **NDIS\_WWAN\_USSD\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_request) | 不支持 | A | 不支持 | 不支持 | GSM |
| [OID\_WWAN\_设备\_服务\_命令](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-service-command)使用[ **NDIS\_WWAN\_设备\_服务\_命令**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_command) | 不支持 | A | 不支持 | A| GSM, CDMA |

> [!NOTE]
> 以下说明适用于前面的表: † 表示微型端口驱动程序可能支持的可选 Oid。 不支持可选的 Oid 的微型端口驱动程序必须在 OID 时不返回\_GEN\_支持\_列表。
>
> † 表示微型端口驱动程序支持基于 GSM 的设备可以选择性地支持 OID\_WWAN\_已设置\_上下文设置和查询操作。 支持基于 CDMA 的设备的微型端口驱动程序可以选择性地支持 OID\_WWAN\_已预配\_上下文查询操作的基于 CDMA 的设备的报告简单 IP (WWAN\_CTRL\_CAP\_CDMA\_简单\_IP)。
>
> 微型端口驱动程序必须支持所有的非可选 Oid。 MB 服务可能会忽略任何不会报告所有必需的 Oid 的微型端口驱动程序。
> 
> "A"和"S"中的集和查询操作列上表中的反映的事务的完成 OID 请求的性质："A"代表异步事务和"S"的同步事务。
>
> 上表中的数据结构对应设置操作 Oid 并返回同步查询操作 Oid 的数据。
> 
> 以下 Oid 共享常见的可变长度列表数据结构称为[ **WWAN\_列表\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_list_header)其对应的数据结构中：
> -   OID\_WWAN\_准备\_信息
> -   OID\_WWAN\_首选\_提供程序
> -   OID\_WWAN\_VISIBLE\_提供程序
> -   OID\_WWAN\_已设置\_上下文
> -   OID\_WWAN\_SMS\_READ 

## <a name="wwan-specific-indications-corresponding-data-structures-and-os-revisions"></a>特定于 WWAN 的迹象，对应的数据结构和 OS 修订

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>指示</strong>和<strong>对应的数据结构</strong></p></td>
<td align="left"><p><strong>Windows 7 修订版本</strong></p>
<p><strong>Windows 8 修订版本</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_CAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps)"><strong>NDIS_STATUS_WWAN_DEVICE_CAPS</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_CAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)"> <strong>NDIS_WWAN_DEVICE_CAPS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_CAPS_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_CAPS_REVISION_2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ready-info" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_READY_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ready-info)"><strong>NDIS_STATUS_WWAN_READY_INFO</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_ready_info" data-raw-source="[&lt;strong&gt;NDIS_WWAN_READY_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_ready_info)"> <strong>NDIS_WWAN_READY_INFO</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_READY_INFO_REVISION_1</p>
<p>NDIS_WWAN_READY_INFO_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-radio-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_RADIO_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-radio-state)"><strong>NDIS_STATUS_WWAN_RADIO_STATE</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_RADIO_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state)"> <strong>NDIS_WWAN_RADIO_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_RADIO_STATE_REVISION_1</p>
<p>NDIS_WWAN_RADIO_STATE_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-info" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-info)"><strong>NDIS_STATUS_WWAN_PIN_INFO</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PIN_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)"> <strong>NDIS_WWAN_PIN_INFO</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PIN_INFO_REVISION_1</p>
<p>NDIS_WWAN_PIN_INFO_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-list" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_LIST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-list)"><strong>NDIS_STATUS_WWAN_PIN_LIST</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_list" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PIN_LIST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_list)"> <strong>NDIS_WWAN_PIN_LIST</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PIN_LIST_REVISION_1</p>
<p>NDIS_WWAN_PIN_LIST_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-service-activation" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SERVICE_ACTIVATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-service-activation)"><strong>NDIS_STATUS_WWAN_SERVICE_ACTIVATION</strong></a>†</p>
<p>uses <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_service_activation_status" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SERVICE_ACTIVATION_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_service_activation_status)"><strong>NDIS_WWAN_SERVICE_ACTIVATION_STATUS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SERVICE_ACTIVATION_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SERVICE_ACTIVATION_STATUS_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider)"><strong>NDIS_STATUS_WWAN_HOME_PROVIDER</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider" data-raw-source="[&lt;strong&gt;NDIS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider)"> <strong>NDIS_WWAN_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_HOME_PROVIDER_REVISION_1</p>
<p>NDIS_WWAN_HOME_PROVIDER_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-providers)"><strong>NDIS_STATUS_WWAN_PREFERRED_PROVIDERS</strong></a>†</p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PREFERRED_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers)"> <strong>NDIS_WWAN_PREFERRED_PROVIDERS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PREFERRED_PROVIDERS_REVISION_1</p>
<p>NDIS_WWAN_PREFERRED_PROVIDERS_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)"> <strong>NDIS_WWAN_VISIBLE_PROVIDERS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_VISIBLE_PROVIDERS_REVISION_1</p>
<p>NDIS_WWAN_VISIBLE_PROVIDERS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_REGISTER_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state)"><strong>NDIS_STATUS_WWAN_REGISTER_STATE</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_registration_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_REGISTRATION_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_registration_state)"> <strong>NDIS_WWAN_REGISTRATION_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_REGISTRATION_STATE_REVISION_1</p>
<p>NDIS_WWAN_REGISTRATION_STATE_REVISION_2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-signal-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SIGNAL_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-signal-state)"><strong>NDIS_STATUS_WWAN_SIGNAL_STATE</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SIGNAL_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)"> <strong>NDIS_WWAN_SIGNAL_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SIGNAL_STATE_REVISION_1</p>
<p>NDIS_WWAN_SIGNAL_STATE_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PACKET_SERVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service)"><strong>NDIS_STATUS_WWAN_PACKET_SERVICE</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PACKET_SERVICE_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state)"> <strong>NDIS_WWAN_PACKET_SERVICE_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PACKET_SERVICE_STATE_REVISION_1</p>
<p>NDIS_WWAN_PACKET_SERVICE_STATE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-provisioned-contexts" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-provisioned-contexts)"><strong>NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_provisioned_contexts" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PROVISIONED_CONTEXTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_provisioned_contexts)"> <strong>NDIS_WWAN_PROVISIONED_CONTEXTS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PROVISIONED_CONTEXTS_REVISION_1</p>
<p>NDIS_WWAN_PROVISIONED_CONTEXTS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-context-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_CONTEXT_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-context-state)"><strong>NDIS_STATUS_WWAN_CONTEXT_STATE</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_context_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_CONTEXT_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_context_state)"> <strong>NDIS_WWAN_CONTEXT_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_CONTEXT_STATE_REVISION_1</p>
<p>NDIS_WWAN_CONTEXT_STATE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-configuration" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_CONFIGURATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-configuration)"><strong>NDIS_STATUS_WWAN_SMS_CONFIGURATION</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_configuration" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_CONFIGURATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_configuration)"> <strong>NDIS_WWAN_SMS_CONFIGURATION</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_CONFIGURATION_REVISION_1</p>
<p>NDIS_WWAN_SMS_CONFIGURATION_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-receive" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_RECEIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-receive)"><strong>NDIS_STATUS_WWAN_SMS_RECEIVE</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_receive" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_RECEIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_receive)"> <strong>NDIS_WWAN_SMS_RECEIVE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_RECEIVE_REVISION_1</p>
<p>NDIS_WWAN_SMS_RECEIVE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-send" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_SEND&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-send)"><strong>NDIS_STATUS_WWAN_SMS_SEND</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_SEND_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status)"> <strong>NDIS_WWAN_SMS_SEND_STATUS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_SEND_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SMS_SEND_STATUS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-delete" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_DELETE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-delete)"><strong>NDIS_STATUS_WWAN_SMS_DELETE</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete_status" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_DELETE_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete_status)"> <strong>NDIS_WWAN_SMS_DELETE_STATUS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_DELETE_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SMS_DELETE_STATUS_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-status" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-status)"><strong>NDIS_STATUS_WWAN_SMS_STATUS</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_status" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_status)"> <strong>NDIS_WWAN_SMS_STATUS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SMS_STATUS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-vendor-specific" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VENDOR_SPECIFIC&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-vendor-specific)"><strong>NDIS_STATUS_WWAN_VENDOR_SPECIFIC</strong></a>†</p>
<p>使用供应商定义的结构</p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ussd" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_USSD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ussd)"><strong>NDIS_STATUS_WWAN_USSD</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_event" data-raw-source="[&lt;strong&gt;NDIS_WWAN_USSD_EVENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_event)"> <strong>NDIS_WWAN_USSD_EVENT</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_USSD_EVENT_REVISION_1</p>
<p>NDIS_WWAN_USSD_EVENT_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_supported_commands" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_supported_commands)"> <strong>NDIS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICES_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICES_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-response" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-response)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_response" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_RESPONSE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_response)"> <strong>NDIS_WWAN_DEVICE_SERVICE_RESPONSE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICE_RESPONSE_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICE_RESPONSE_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-event" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-event)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_event" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_EVENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_event)"> <strong>NDIS_WWAN_DEVICE_SERVICE_EVENT</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICE_EVENT_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICE_EVENT_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-subscription" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-subscription)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_subscription" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_subscription)"> <strong>NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-auth-response" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_AUTH_RESPONSE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-auth-response)"><strong>NDIS_STATUS_WWAN_AUTH_RESPONSE</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_auth_response" data-raw-source="[&lt;strong&gt;NDIS_WWAN_AUTH_RESPONSE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_auth_response)"> <strong>NDIS_WWAN_AUTH_RESPONSE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_AUTH_RESPONSE_REVISION_1</p>
<p>NDIS_WWAN_AUTH_RESPONSE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-set-home-provider-complete" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-set-home-provider-complete)"><strong>NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_home_provider" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SET_HOME_PROVIDER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_home_provider)"> <strong>NDIS_WWAN_SET_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>不可用</p>
<p>NDIS_WWAN_HOME_PROVIDER_REVISION_2</p></td>
</tr>
</tbody>
</table>

> [!NOTE]
> 以下说明适用于前面的表: † 表示微型端口驱动程序可能支持的可选指示。 请注意，如果微型端口驱动程序支持可选的 OID，微型端口驱动程序还应支持相应的指示。 

## <a name="wwan-specific-indication-support-for-gsm-cdma-and-unsolicited-indications"></a>特定于 WWAN 的指示支持 GSM、 CDMA 和未经请求的迹象

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>指示</strong></p></td>
<td align="left"><p><strong>GSM</strong></p></td>
<td align="left"><p><strong>CDMA</strong></p></td>
<td align="left"><p><strong>未经请求</strong></p>
<p><strong>indication</strong></p>
<p><strong>允许使用？</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_CAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps)"><strong>NDIS_STATUS_WWAN_DEVICE_CAPS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ready-info" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_READY_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ready-info)"><strong>NDIS_STATUS_WWAN_READY_INFO</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-radio-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_RADIO_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-radio-state)"><strong>NDIS_STATUS_WWAN_RADIO_STATE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-info" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-info)"><strong>NDIS_STATUS_WWAN_PIN_INFO</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-list" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_LIST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-list)"><strong>NDIS_STATUS_WWAN_PIN_LIST</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-service-activation" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SERVICE_ACTIVATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-service-activation)"><strong>NDIS_STATUS_WWAN_SERVICE_ACTIVATION</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider)"><strong>NDIS_STATUS_WWAN_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-providers)"><strong>NDIS_STATUS_WWAN_PREFERRED_PROVIDERS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_REGISTER_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state)"><strong>NDIS_STATUS_WWAN_REGISTER_STATE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-signal-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SIGNAL_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-signal-state)"><strong>NDIS_STATUS_WWAN_SIGNAL_STATE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PACKET_SERVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service)"><strong>NDIS_STATUS_WWAN_PACKET_SERVICE</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PACKET_SERVICE_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state)"> <strong>NDIS_WWAN_PACKET_SERVICE_STATE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-provisioned-contexts" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-provisioned-contexts)"><strong>NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-context-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_CONTEXT_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-context-state)"><strong>NDIS_STATUS_WWAN_CONTEXT_STATE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-configuration" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_CONFIGURATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-configuration)"><strong>NDIS_STATUS_WWAN_SMS_CONFIGURATION</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-receive" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_RECEIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-receive)"><strong>NDIS_STATUS_WWAN_SMS_RECEIVE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-send" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_SEND&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-send)"><strong>NDIS_STATUS_WWAN_SMS_SEND</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_SEND_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status)"> <strong>NDIS_WWAN_SMS_SEND_STATUS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-delete" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_DELETE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-delete)"><strong>NDIS_STATUS_WWAN_SMS_DELETE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-status" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-status)"><strong>NDIS_STATUS_WWAN_SMS_STATUS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-vendor-specific" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VENDOR_SPECIFIC&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-vendor-specific)"><strong>NDIS_STATUS_WWAN_VENDOR_SPECIFIC</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ussd" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_USSD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ussd)"><strong>NDIS_STATUS_WWAN_USSD</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-response" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-response)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-event" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-event)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-subscription" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-subscription)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-auth-response" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_AUTH_RESPONSE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-auth-response)"><strong>NDIS_STATUS_WWAN_AUTH_RESPONSE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-set-home-provider-complete" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-set-home-provider-complete)"><strong>NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
</tbody>
</table> 

## <a name="multi-carrier-specific-oids"></a>多运营商的特定 Oid

以下更改适用于支持多运营商模式的 NDIS 6.30 微型端口驱动程序。 如果微型端口驱动程序不支持多运营商模式，则请参阅上表中。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>OID</strong>和<strong>Windows 8 相对应的数据结构</strong></p></td>
<td align="left"><p><strong>查询操作</strong></p></td>
<td align="left"><p><strong>设置操作</strong></p></td>
<td align="left"><p><strong>GSM/CDMA</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-home-provider" data-raw-source="[OID_WWAN_HOME_PROVIDER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-home-provider)">OID_WWAN_HOME_PROVIDER</a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_home_provider" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SET_HOME_PROVIDER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_home_provider)"> <strong>NDIS_WWAN_SET_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>A</p></td>
<td align="left"><p>A</p></td>
<td align="left"><p>GSM, CDMA</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-preferred-providers" data-raw-source="[OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-preferred-providers)">OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_preferred_multicarrier_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SET_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_preferred_multicarrier_providers)"> <strong>NDIS_WWAN_SET_PREFERRED_MULTICARRIER_PROVIDERS</strong></a>。 <strong>PreferredListHeader.ElementType</strong>应设置为<strong>WwanStructProvider2</strong>而且结构 WWAN_PROVIDER2。</p></td>
<td align="left"><p>A</p></td>
<td align="left"><p>A</p></td>
<td align="left"><p>GSM, CDMA</p></td>
</tr>
</tbody>
</table> 

## <a name="multi-carrier-specific-indications-corresponding-data-structures-and-os-revisions"></a>多运营商的特定指示、 对应的数据结构和 OS 修订版

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>指示</strong>和<strong>对应的数据结构</strong></p></td>
<td align="left"><p><strong>Windows 8 修订版本</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider)"><strong>NDIS_STATUS_WWAN_HOME_PROVIDER</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider2" data-raw-source="[&lt;strong&gt;NDIS_WWAN_HOME_PROVIDER2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider2)"> <strong>NDIS_WWAN_HOME_PROVIDER2</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_HOME_PROVIDER_REVISION_2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-multicarrier-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-multicarrier-providers)"><strong>NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers)"> <strong>NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS_REVISION_1. <strong>PreferredListHeader.ElementType</strong>应设置为<strong>WwanStructProvider2</strong>列表应包含 WWAN_PROVIDER2 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)"> <strong>NDIS_WWAN_VISIBLE_PROVIDERS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_VISIBLE_PROVIDERS_REVISION_1. <strong>VisibleListHeader.ElementType</strong>应设置为<strong>WwanStructProvider2</strong>列表应包含 WWAN_PROVIDER2 结构。</p></td>
</tr>
</tbody>
</table> 

## <a name="multi-carrier-specific-indication-support-for-gsm-cdma-and-unsolicited-indications"></a>多运营商具体的说明支持 GSM、 CDMA 和未经请求的迹象

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>指示</strong>和<strong>对应的数据结构</strong></p></td>
<td align="left"><p><strong>GSM</strong></p></td>
<td align="left"><p><strong>CDMA</strong></p></td>
<td align="left"><p><strong>未经请求</strong></p>
<p><strong>indication</strong></p>
<p><strong>允许使用？</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider)"><strong>NDIS_STATUS_WWAN_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-multicarrier-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-multicarrier-providers)"><strong>NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)"> <strong>NDIS_WWAN_VISIBLE_PROVIDERS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
</tbody>
</table>
