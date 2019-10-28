---
title: MB 数据模型
description: MB 数据模型
ms.assetid: 922b6b55-c332-4721-bbd1-571b0e154df3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cedf9e52e1a74cba00494d523ba83d06d7f4e149
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844296"
---
# <a name="mb-data-model"></a>MB 数据模型


MB 驱动程序模型使用一种数据模型，此模型包含一组定义为 MB 设备功能的抽象的对象。 每个对象都由一个唯一的对象标识符（OID）标识，并由一组对应的属性定义。 属性集组织到一个数据结构中。 若要管理设备，MB 服务和 MB 微型端口驱动程序会根据网络驱动程序接口规范（NDIS）提供的 OID 请求和指示来交换 Oid 及其关联的数据结构。

在 MB 驱动程序模型中，只对 OID 请求使用*set*和*query*操作。 MB 驱动程序模型不使用*方法*操作。 对于指示，MB 驱动程序模型使用事件和事务通知来指示 MB 设备的对象中的状态更改。 事务通知还会指示异步事务的完成。

下表列出了为 MB 微型端口驱动程序定义的 Oid 和状态指示以及关联的数据结构。 MB 微型端口驱动程序必须实现 NDIS 6.20 规范要求的所有必需的常规 Oid。 有关 NDIS 1.x 的常规 Oid 列表，请参阅[常规操作 oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/index)。

此外，MB 的微型端口驱动程序必须\_物理\_中型\_代实现 OID，即使 NDIS 规范将其描述为可用于实现。

下表中列出的 MB Oid 的语法和语义以[Mb 操作语义](mb-operational-semantics.md)进行说明。 Mb 服务和 MB 微型端口驱动程序之间的交互在[Mb 操作流程图](mb-operation-flowcharts.md)中进行了介绍。

## <a name="wwan-specific-oids"></a>WWAN 特定 Oid

| OID 和对应的数据结构 | 设置操作 |   | 查询操作 |   | GSM/CDMA |
| ---                                  | ---       | ---       | ---       | ---       |--- |
|                                      | Windows 7 | Windows 8 | Windows 7 | Windows 8 |    |
| [OID\_wwan\_驱动程序\_cap](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-driver-caps)使用[ **NDIS\_WWAN\_驱动程序\_cap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_driver_caps) | 不支持 | 不支持 |S | S | GSM，CDMA |
| [OID\_WWAN\_设备\_cap](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps)没有对应的结构 | 不支持 | 不支持 | 一个 | 一个 | GSM，CDMA |
| [OID\_WWAN\_就绪\_信息](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ready-info)没有对应的结构 | 不支持 | 一个 | 一个 | GSM，CDMA |
| [OID\_wwan\_service\_ACTIVATION](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-service-activation)†使用[ **NDIS\_WWAN\_服务\_激活**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_service_activation) | 一个 | 一个 | 不支持 | 不支持 | GSM，CDMA |
| [OID\_wwan\_无线电\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-radio-state)使用[ **NDIS\_WWAN\_集\_广播\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_radio_state) | 一个 | 一个 | 一个 | 一个 | GSM，CDMA |
| [OID\_wwan\_pin](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin)使用[ **NDIS\_WWAN\_集\_PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin) | 一个 | 不支持 | 一个 | 不支持 | GSM，CDMA |
| [OID\_WWAN\_PIN\_列表](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin-list)没有对应的结构 | 不支持 | 不支持 | 一个 | 一个 | GSM，CDMA |
| [OID\_wwan\_PIN\_ex](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin-ex)使用[ **NDIS\_WWAN\_集\_PIN\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin_ex) | 不支持 | 一个 | 不支持 | 一个 | GSM，CDMA |
| [OID\_WWAN\_HOME\_提供程序](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-home-provider)没有相应的结构 | 不支持 | 不支持 | 一个 | 一个 | GSM，CDMA |
| [OID\_wwan\_首选\_提供者](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-preferred-providers)†使用[ **NDIS\_WWAN\_集\_首选\_提供程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_preferred_providers) | 一个 | 一个 | 一个 | 一个 | 仅 GSM |
| [OID\_WWAN\_可见\_提供程序](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-visible-providers)没有相应的结构 | 不支持 | 不支持 | 一个 | 一个 | GSM |
| [OID\_wwan\_REGISTER\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-register-state)使用[ **NDIS\_WWAN\_集\_注册\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_register_state) | 一个 | 一个 | 一个 | 一个 | CDMA |
| [OID\_wwan\_信号\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-signal-state)使用[ **NDIS\_WWAN\_集\_信号\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_signal_indication) | 一个 | 一个 | 一个 | 一个 | GSM，CDMA |
| [OID\_wwan\_数据包\_服务](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-packet-service)使用[ **NDIS\_WWAN\_集\_包\_服务**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_packet_service) | 一个 | 一个 | 一个 | 一个 | GSM，CDMA |
| [OID\_wwan\_预配\_上下文](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-provisioned-contexts)††使用[ **NDIS\_WWAN\_集\_预配\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_provisioned_context) | 一个 | 一个 | 一个 | 一个 | GSM，CDMA |
| [OID\_wwan\_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-connect)使用[ **NDIS\_WWAN\_集\_上下文\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_context_state) | 一个 | 一个 | 一个 | 一个 | GSM，CDMA |
| [OID\_wwan\_SMS\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-configuration)使用[ **NDIS\_WWAN\_设置\_SMS\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sms_configuration) | 一个 | 一个 | 一个 | 一个 | GSM，CDMA | 
| [OID\_wwan\_sms\_read](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-read)使用[ **NDIS\_WWAN\_SMS\_读取**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_read) | 不支持 | 一个 | 一个 | 一个 |GSM，CDMA | 
| [OID\_wwan\_sms\_send](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-send)使用[ **NDIS\_WWAN\_SMS\_发送**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send) | 一个 | 一个 | 不支持 | 不支持 | GSM，CDMA |
| [OID\_wwan\_sms\_删除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-delete)使用[ **NDIS\_WWAN\_SMS\_删除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete) | 一个 | 一个 | 不支持 | 不支持 |  GSM，CDMA |
| [OID\_wwan\_sms\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-status)使用[ **NDIS\_WWAN\_sms\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_status) | 不支持 | 不支持 | 一个 | 一个 | GSM，CDMA |
| [OID\_WWAN\_供应商\_特定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-vendor-specific)†使用供应商定义的结构 | 一个 | 一个 | 不支持 | 不支持 | GSM，CDMA |
| [OID\_WWAN\_设备\_服务](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-services)没有相应的结构 | 不支持 | 不支持 | 不支持 | 一个 | GSM，CDMA |
| [OID\_wwan\_订阅\_设备\_服务\_事件](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-subscribe-device-service-events)使用[ **NDIS\_WWAN\_订阅\_\_SERVICE\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_subscribe_device_service_events) | 不支持 | 一个 | 不支持 | 不支持 | GSM，CDMA |
| [OID\_wwan\_身份验证\_质询](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-auth-challenge)使用[ **NDIS\_WWAN\_身份验证\_质询**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_auth_challenge) | 不支持 | 不支持 | 不支持 | 一个 | GSM，CDMA |
| [OID\_wwan\_USSD](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ussd)使用[ **NDIS\_WWAN\_USSD\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_request) | 不支持 | 一个 | 不支持 | 不支持 | GSM |
| [OID\_wwan\_设备\_服务\_命令](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-service-command)使用[ **NDIS\_WWAN\_设备\_SERVICE\_命令**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_command) | 不支持 | 一个 | 不支持 | 一个| GSM，CDMA |

> [!NOTE]
> 以下说明适用于上表：†表示微型端口驱动程序可以支持的可选 Oid。 不支持可选 Oid 的微型端口驱动程序不得以 OID 方式返回它们\_代\_支持\_列表。
>
> †表示支持基于 GSM 的设备的微型端口驱动程序，这些设备可以选择支持 OID\_WWAN\_预配\_上下文集和查询操作。 支持基于 CDMA 的设备的微型端口驱动程序可以选择支持\_WWAN\_预配\_上下文查询操作的上下文查询\_\_操作。简单\_IP）。
>
> 微型端口驱动程序必须支持所有非可选 Oid。 MB 服务可能会忽略不报告所有必需 Oid 的任何微型端口驱动程序。
> 
> 上表的 Set 和 Query 操作列中的 "a" 和 "S" 反映了完成 OID 请求的事务的性质： "A" 表示异步事务，"S" 表示同步事务。
>
> 上表中的数据结构对应于设置操作 Oid，并为同步查询操作 Oid 返回数据。
> 
> 以下 Oid 在其相应的数据结构中共享名为[**WWAN\_list\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_list_header)的通用可变长度列表数据结构：
> -   OID\_WWAN\_就绪\_信息
> -   OID\_WWAN\_首选\_提供程序
> -   OID\_WWAN\_可见\_提供程序
> -   OID\_WWAN\_预配\_上下文
> -   OID\_WWAN\_SMS\_读取 

## <a name="wwan-specific-indications-corresponding-data-structures-and-os-revisions"></a>特定于 WWAN 的指示、相应的数据结构和操作系统修订版本

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>指示</strong>和<strong>对应的数据结构</strong></p></td>
<td align="left"><p><strong>Windows 7 版本</strong></p>
<p><strong>Windows 8 修订版本</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_CAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps)"><strong>NDIS_STATUS_WWAN_DEVICE_CAPS</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_CAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)"> <strong>NDIS_WWAN_DEVICE_CAPS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_CAPS_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_CAPS_REVISION_2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ready-info" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_READY_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ready-info)"><strong>NDIS_STATUS_WWAN_READY_INFO</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ready_info" data-raw-source="[&lt;strong&gt;NDIS_WWAN_READY_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ready_info)"> <strong>NDIS_WWAN_READY_INFO</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_READY_INFO_REVISION_1</p>
<p>NDIS_WWAN_READY_INFO_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-radio-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_RADIO_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-radio-state)"><strong>NDIS_STATUS_WWAN_RADIO_STATE</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_RADIO_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state)"> <strong>NDIS_WWAN_RADIO_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_RADIO_STATE_REVISION_1</p>
<p>NDIS_WWAN_RADIO_STATE_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-info" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-info)"><strong>NDIS_STATUS_WWAN_PIN_INFO</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PIN_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)"> <strong>NDIS_WWAN_PIN_INFO</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PIN_INFO_REVISION_1</p>
<p>NDIS_WWAN_PIN_INFO_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-list" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_LIST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-list)"><strong>NDIS_STATUS_WWAN_PIN_LIST</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_list" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PIN_LIST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_list)"> <strong>NDIS_WWAN_PIN_LIST</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PIN_LIST_REVISION_1</p>
<p>NDIS_WWAN_PIN_LIST_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-service-activation" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SERVICE_ACTIVATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-service-activation)"><strong>NDIS_STATUS_WWAN_SERVICE_ACTIVATION</strong></a>†</p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_service_activation_status" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SERVICE_ACTIVATION_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_service_activation_status)"> <strong>NDIS_WWAN_SERVICE_ACTIVATION_STATUS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SERVICE_ACTIVATION_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SERVICE_ACTIVATION_STATUS_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider)"><strong>NDIS_STATUS_WWAN_HOME_PROVIDER</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider" data-raw-source="[&lt;strong&gt;NDIS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider)"> <strong>NDIS_WWAN_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_HOME_PROVIDER_REVISION_1</p>
<p>NDIS_WWAN_HOME_PROVIDER_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-providers)"><strong>NDIS_STATUS_WWAN_PREFERRED_PROVIDERS</strong></a>†</p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PREFERRED_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers)"> <strong>NDIS_WWAN_PREFERRED_PROVIDERS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PREFERRED_PROVIDERS_REVISION_1</p>
<p>NDIS_WWAN_PREFERRED_PROVIDERS_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)"> <strong>NDIS_WWAN_VISIBLE_PROVIDERS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_VISIBLE_PROVIDERS_REVISION_1</p>
<p>NDIS_WWAN_VISIBLE_PROVIDERS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_REGISTER_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state)"><strong>NDIS_STATUS_WWAN_REGISTER_STATE</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_registration_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_REGISTRATION_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_registration_state)"> <strong>NDIS_WWAN_REGISTRATION_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_REGISTRATION_STATE_REVISION_1</p>
<p>NDIS_WWAN_REGISTRATION_STATE_REVISION_2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-signal-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SIGNAL_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-signal-state)"><strong>NDIS_STATUS_WWAN_SIGNAL_STATE</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SIGNAL_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)"> <strong>NDIS_WWAN_SIGNAL_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SIGNAL_STATE_REVISION_1</p>
<p>NDIS_WWAN_SIGNAL_STATE_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PACKET_SERVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service)"><strong>NDIS_STATUS_WWAN_PACKET_SERVICE</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PACKET_SERVICE_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state)"> <strong>NDIS_WWAN_PACKET_SERVICE_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PACKET_SERVICE_STATE_REVISION_1</p>
<p>NDIS_WWAN_PACKET_SERVICE_STATE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-provisioned-contexts" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-provisioned-contexts)"><strong>NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_provisioned_contexts" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PROVISIONED_CONTEXTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_provisioned_contexts)"> <strong>NDIS_WWAN_PROVISIONED_CONTEXTS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PROVISIONED_CONTEXTS_REVISION_1</p>
<p>NDIS_WWAN_PROVISIONED_CONTEXTS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-context-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_CONTEXT_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-context-state)"><strong>NDIS_STATUS_WWAN_CONTEXT_STATE</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_context_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_CONTEXT_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_context_state)"> <strong>NDIS_WWAN_CONTEXT_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_CONTEXT_STATE_REVISION_1</p>
<p>NDIS_WWAN_CONTEXT_STATE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-configuration" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_CONFIGURATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-configuration)"><strong>NDIS_STATUS_WWAN_SMS_CONFIGURATION</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_configuration" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_CONFIGURATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_configuration)"> <strong>NDIS_WWAN_SMS_CONFIGURATION</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_CONFIGURATION_REVISION_1</p>
<p>NDIS_WWAN_SMS_CONFIGURATION_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-receive" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_RECEIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-receive)"><strong>NDIS_STATUS_WWAN_SMS_RECEIVE</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_receive" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_RECEIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_receive)"> <strong>NDIS_WWAN_SMS_RECEIVE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_RECEIVE_REVISION_1</p>
<p>NDIS_WWAN_SMS_RECEIVE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-send" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_SEND&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-send)"><strong>NDIS_STATUS_WWAN_SMS_SEND</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_SEND_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status)"> <strong>NDIS_WWAN_SMS_SEND_STATUS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_SEND_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SMS_SEND_STATUS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-delete" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_DELETE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-delete)"><strong>NDIS_STATUS_WWAN_SMS_DELETE</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete_status" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_DELETE_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete_status)"> <strong>NDIS_WWAN_SMS_DELETE_STATUS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_DELETE_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SMS_DELETE_STATUS_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-status" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-status)"><strong>NDIS_STATUS_WWAN_SMS_STATUS</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_status" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_status)"> <strong>NDIS_WWAN_SMS_STATUS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SMS_STATUS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-vendor-specific" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VENDOR_SPECIFIC&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-vendor-specific)"><strong>NDIS_STATUS_WWAN_VENDOR_SPECIFIC</strong></a>†</p>
<p>使用供应商定义的结构</p></td>
<td align="left"><p>N/A</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ussd" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_USSD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ussd)"><strong>NDIS_STATUS_WWAN_USSD</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_event" data-raw-source="[&lt;strong&gt;NDIS_WWAN_USSD_EVENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_event)"> <strong>NDIS_WWAN_USSD_EVENT</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_USSD_EVENT_REVISION_1</p>
<p>NDIS_WWAN_USSD_EVENT_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_supported_commands" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_supported_commands)"> <strong>NDIS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICES_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICES_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-response" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-response)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_response" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_RESPONSE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_response)"> <strong>NDIS_WWAN_DEVICE_SERVICE_RESPONSE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICE_RESPONSE_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICE_RESPONSE_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-event" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-event)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_event" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_EVENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_event)"> <strong>NDIS_WWAN_DEVICE_SERVICE_EVENT</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICE_EVENT_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICE_EVENT_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-subscription" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-subscription)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_subscription" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_subscription)"> <strong>NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-auth-response" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_AUTH_RESPONSE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-auth-response)"><strong>NDIS_STATUS_WWAN_AUTH_RESPONSE</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_auth_response" data-raw-source="[&lt;strong&gt;NDIS_WWAN_AUTH_RESPONSE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_auth_response)"> <strong>NDIS_WWAN_AUTH_RESPONSE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_AUTH_RESPONSE_REVISION_1</p>
<p>NDIS_WWAN_AUTH_RESPONSE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-set-home-provider-complete" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-set-home-provider-complete)"><strong>NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_home_provider" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SET_HOME_PROVIDER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_home_provider)"> <strong>NDIS_WWAN_SET_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>N/A</p>
<p>NDIS_WWAN_HOME_PROVIDER_REVISION_2</p></td>
</tr>
</tbody>
</table>

> [!NOTE]
> 以下说明适用于上表：†表示微型端口驱动程序可以支持的可选指示。 请注意，如果微型端口驱动程序支持可选 OID，则微型端口驱动程序还应支持相应的指示。 

## <a name="wwan-specific-indication-support-for-gsm-cdma-and-unsolicited-indications"></a>针对 GSM、CDMA 和未经请求的指示的 WWAN 特定指示支持

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>有人</strong></p></td>
<td align="left"><p><strong>GSM</strong></p></td>
<td align="left"><p><strong>CDMA</strong></p></td>
<td align="left"><p><strong>依靠</strong></p>
<p><strong>有人</strong></p>
<p><strong>获准?</strong></p></td>
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
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PACKET_SERVICE_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state)"> <strong>NDIS_WWAN_PACKET_SERVICE_STATE</strong></a></p></td>
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
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_SEND_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status)"> <strong>NDIS_WWAN_SMS_SEND_STATUS</strong></a></p></td>
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

## <a name="multi-carrier-specific-oids"></a>多载波特定 Oid

以下更改适用于支持多载波模式的 NDIS 6.30 微型端口驱动程序。 如果微型端口驱动程序不支持多载波模式，请参阅上表。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>OID</strong>和<strong>Windows 8 相应的数据结构</strong></p></td>
<td align="left"><p><strong>查询操作</strong></p></td>
<td align="left"><p><strong>设置操作</strong></p></td>
<td align="left"><p><strong>GSM/CDMA</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-home-provider" data-raw-source="[OID_WWAN_HOME_PROVIDER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-home-provider)">OID_WWAN_HOME_PROVIDER</a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_home_provider" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SET_HOME_PROVIDER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_home_provider)"> <strong>NDIS_WWAN_SET_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>一个</p></td>
<td align="left"><p>一个</p></td>
<td align="left"><p>GSM，CDMA</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-preferred-providers" data-raw-source="[OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-preferred-providers)">OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_preferred_multicarrier_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SET_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_preferred_multicarrier_providers)"><strong>NDIS_WWAN_SET_PREFERRED_MULTICARRIER_PROVIDERS</strong></a>。 应将<strong>PreferredListHeader</strong>设置为<strong>WwanStructProvider2</strong> ，并将结构设置为 WWAN_PROVIDER2。</p></td>
<td align="left"><p>一个</p></td>
<td align="left"><p>一个</p></td>
<td align="left"><p>GSM，CDMA</p></td>
</tr>
</tbody>
</table> 

## <a name="multi-carrier-specific-indications-corresponding-data-structures-and-os-revisions"></a>多运营商特定指示、相应的数据结构和操作系统修订版本

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
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider2" data-raw-source="[&lt;strong&gt;NDIS_WWAN_HOME_PROVIDER2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider2)"> <strong>NDIS_WWAN_HOME_PROVIDER2</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_HOME_PROVIDER_REVISION_2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-multicarrier-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-multicarrier-providers)"><strong>NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers)"> <strong>NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS_REVISION_1. 应将<strong>PreferredListHeader</strong>设置为<strong>WwanStructProvider2</strong> ，并且列表应包含 WWAN_PROVIDER2 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)"> <strong>NDIS_WWAN_VISIBLE_PROVIDERS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_VISIBLE_PROVIDERS_REVISION_1. 应将<strong>VisibleListHeader</strong>设置为<strong>WwanStructProvider2</strong> ，并且列表应包含 WWAN_PROVIDER2 结构。</p></td>
</tr>
</tbody>
</table> 

## <a name="multi-carrier-specific-indication-support-for-gsm-cdma-and-unsolicited-indications"></a>针对 GSM、CDMA 和未经请求的指示的多运营商特定指示支持

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
<td align="left"><p><strong>依靠</strong></p>
<p><strong>有人</strong></p>
<p><strong>获准?</strong></p></td>
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
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)"> <strong>NDIS_WWAN_VISIBLE_PROVIDERS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
</tbody>
</table>
