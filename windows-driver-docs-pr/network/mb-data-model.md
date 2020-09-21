---
title: MB 数据模型
description: MB 数据模型
ms.assetid: 922b6b55-c332-4721-bbd1-571b0e154df3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 701049c3dd0383e4d0eff166dc7a6d0e70d612c7
ms.sourcegitcommit: 74a8dc9ef1da03857dec5cab8d304e2869ba54a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90759776"
---
# <a name="mb-data-model"></a>MB 数据模型


MB 驱动程序模型使用一种数据模型，此模型包含一组定义为 MB 设备功能的抽象的对象。 每个对象都由唯一对象标识符标识 (OID) 并由一组对应的属性定义。 属性集组织到一个数据结构中。 若要管理设备，MB 服务和 MB 微型端口驱动程序会根据网络驱动程序接口规范 (NDIS) 提供的 OID 请求和指示来交换 Oid 及其关联的数据结构。

在 MB 驱动程序模型中，只对 OID 请求使用 *set* 和 *query* 操作。 MB 驱动程序模型不使用 *方法* 操作。 对于指示，MB 驱动程序模型使用事件和事务通知来指示 MB 设备的对象中的状态更改。 事务通知还会指示异步事务的完成。

下表列出了为 MB 微型端口驱动程序定义的 Oid 和状态指示以及关联的数据结构。 MB 微型端口驱动程序必须实现 NDIS 6.20 规范要求的所有必需的常规 Oid。 有关 NDIS 1.x 的常规 Oid 列表，请参阅 [常规操作 oid](/windows-hardware/drivers/ddi/ntddndis/index)。

此外，MB 微型端口驱动程序必须实现 OID \_ GEN \_ 物理介质， \_ 即使 NDIS 规范将其描述为可用于实现。

下表中列出的 MB Oid 的语法和语义以 [Mb 操作语义](mb-operational-semantics.md)进行说明。 Mb 服务和 MB 微型端口驱动程序之间的交互在 [Mb 操作流程图](mb-operation-flowcharts.md)中进行了介绍。

## <a name="wwan-specific-oids"></a>WWAN 特定 Oid

| OID 和对应的数据结构 | 集，Windows 7 | 集，Windows 8  | 查询，Windows 7 | 查询，Windows 8  | GSM/CDMA |
| ---                                  | ---       | ---       | ---       | ---       |--- |
| [OID \_WWAN \_ 驱动程序 \_ Cap](./oid-wwan-driver-caps.md)使用[ **NDIS \_ WWAN \_ 驱动程序 \_ cap**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_driver_caps) | 不支持 | 不支持 |S | S | GSM，CDMA |
| [OID \_WWAN \_ 设备 \_ cap](./oid-wwan-device-caps.md) 没有对应的结构 | 不支持 | 不支持 | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | GSM，CDMA |
| [OID \_WWAN \_ 就绪 \_ 信息](./oid-wwan-ready-info.md) 没有对应的结构 | 不支持 | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | GSM，CDMA |
| [OID \_WWAN \_ 服务 \_ 激活](./oid-wwan-service-activation.md)†使用[ **NDIS \_ WWAN \_ 服务 \_ 激活**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_service_activation) | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | 不支持 | 不支持 | GSM，CDMA |
| [OID \_WWAN \_ 无线电 \_ 状态](./oid-wwan-radio-state.md)使用[ **NDIS \_ WWAN \_ 设置 \_ 无线电 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_radio_state) | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | GSM，CDMA |
| [OID \_WWAN \_ PIN](./oid-wwan-pin.md)使用[ **NDIS \_ WWAN \_ 集 \_ pin**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin) | 包含当前请求的 URL 的 | 不支持 | 包含当前请求的 URL 的 | 不支持 | GSM，CDMA |
| [OID \_WWAN \_ PIN \_ 列表](./oid-wwan-pin-list.md) 没有对应的结构 | 不支持 | 不支持 | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | GSM，CDMA |
| [OID \_WWAN \_ PIN \_ Ex](./oid-wwan-pin-ex.md)使用[ **NDIS \_ WWAN \_ 集 \_ PIN \_ ex**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin_ex) | 不支持 | 包含当前请求的 URL 的 | 不支持 | 包含当前请求的 URL 的 | GSM，CDMA |
| [OID \_WWAN \_ 主 \_ 提供程序](./oid-wwan-home-provider.md) 没有相应的结构 | 不支持 | 不支持 | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | GSM，CDMA |
| [OID \_WWAN \_ 首选 \_ 提供程序](./oid-wwan-preferred-providers.md)†使用[ **NDIS \_ WWAN \_ 集 \_ 首选 \_ 提供程序**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_preferred_providers) | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | 仅 GSM |
| [OID \_WWAN \_ 可见 \_ 提供程序](./oid-wwan-visible-providers.md) 没有相应的结构 | 不支持 | 不支持 | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | GSM |
| [OID \_WWAN \_ 注册 \_ 状态](./oid-wwan-register-state.md)使用[ **NDIS \_ WWAN \_ 集 \_ 注册 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_register_state) | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | CDMA |
| [OID \_WWAN \_ 信号 \_ 状态](./oid-wwan-signal-state.md)使用[ **NDIS \_ WWAN \_ 设置 \_ 信号 \_ 指示**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_signal_indication) | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | GSM，CDMA |
| [OID \_WWAN \_ 数据包 \_ 服务](./oid-wwan-packet-service.md)使用[ **NDIS \_ WWAN \_ 集 \_ 数据包 \_ 服务**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_packet_service) | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | GSM，CDMA |
| [OID \_WWAN \_ 预配 \_ 上下文](./oid-wwan-provisioned-contexts.md)††使用[ **NDIS \_ WWAN \_ 集 \_ 预配的 \_ 上下文**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_provisioned_context) | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | GSM，CDMA |
| [OID \_WWAN \_ CONNECT](./oid-wwan-connect.md)使用[ **NDIS \_ WWAN \_ 集 \_ 上下文 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_context_state) | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | GSM，CDMA |
| [OID \_WWAN \_ SMS \_ 配置](./oid-wwan-sms-configuration.md)使用[ **NDIS \_ WWAN \_ 设置 \_ SMS \_ 配置**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sms_configuration) | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | GSM，CDMA | 
| [OID \_WWAN \_ sms \_ 读取](./oid-wwan-sms-read.md)使用[ **NDIS \_ WWAN \_ sms \_ 读取**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_read) | 不支持 | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 |GSM，CDMA | 
| [OID \_WWAN \_ sms \_ Send](./oid-wwan-sms-send.md)使用[ **NDIS \_ WWAN \_ sms \_ 发送**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send) | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | 不支持 | 不支持 | GSM，CDMA |
| [OID \_WWAN \_ 短信 \_ 删除](./oid-wwan-sms-delete.md)使用[ **NDIS \_ WWAN \_ sms \_ 删除**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete) | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | 不支持 | 不支持 |  GSM，CDMA |
| [OID \_WWAN \_ sms \_ 状态](./oid-wwan-sms-status.md)使用[ **NDIS \_ WWAN \_ sms \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_status) | 不支持 | 不支持 | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | GSM，CDMA |
| [OID \_WWAN \_ 供应商 \_ 特定](./oid-wwan-vendor-specific.md)†使用供应商定义的结构 | 包含当前请求的 URL 的 | 包含当前请求的 URL 的 | 不支持 | 不支持 | GSM，CDMA |
| [OID \_WWAN \_ 设备 \_ 服务](./oid-wwan-device-services.md) 没有相应的结构 | 不支持 | 不支持 | 不支持 | 包含当前请求的 URL 的 | GSM，CDMA |
| [OID \_WWAN \_ 订阅 \_ 设备 \_ 服务 \_ 事件](./oid-wwan-subscribe-device-service-events.md)使用[ **NDIS \_ WWAN \_ 订阅 \_ 设备 \_ 服务 \_ 事件**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_subscribe_device_service_events) | 不支持 | 包含当前请求的 URL 的 | 不支持 | 不支持 | GSM，CDMA |
| [OID \_WWAN \_ 身份验证 \_ 质询](./oid-wwan-auth-challenge.md)使用[ **NDIS \_ WWAN \_ 身份验证 \_ 质询**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_auth_challenge) | 不支持 | 不支持 | 不支持 | 包含当前请求的 URL 的 | GSM，CDMA |
| [OID \_WWAN \_ USSD](./oid-wwan-ussd.md)使用[ **NDIS \_ WWAN \_ USSD \_ 请求**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_request) | 不支持 | 包含当前请求的 URL 的 | 不支持 | 不支持 | GSM |
| [OID \_WWAN \_ 设备 \_ 服务 \_ 命令](./oid-wwan-device-service-command.md)使用[ **NDIS \_ WWAN \_ 设备 \_ 服务 \_ 命令**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_command) | 不支持 | 包含当前请求的 URL 的 | 不支持 | 包含当前请求的 URL 的| GSM，CDMA |

> [!NOTE]
> 以下说明适用于上表：†表示微型端口驱动程序可以支持的可选 Oid。 不支持可选 Oid 的微型端口驱动程序不得将其返回到 OID \_ 生成 \_ 支持的列表中 \_ 。
>
> †表示支持基于 GSM 的设备的微型端口驱动程序，这些设备可以选择支持 OID \_ WWAN \_ 预配 \_ 上下文集和查询操作。 支持基于 CDMA 的设备的微型端口驱动程序可以选择 \_ 支持 \_ CDMA 设备的 OID WWAN 预配 \_ 上下文查询操作，这些设备报告简单 ip (WWAN \_ CTRL \_ cap \_ CDMA \_ 简单 \_ ip) 。
>
> 微型端口驱动程序必须支持所有非可选 Oid。 MB 服务可能会忽略不报告所有必需 Oid 的任何微型端口驱动程序。
> 
> 上表的 Set 和 Query 操作列中的 "a" 和 "S" 反映了完成 OID 请求的事务的性质： "A" 表示异步事务，"S" 表示同步事务。
>
> 上表中的数据结构对应于设置操作 Oid，并为同步查询操作 Oid 返回数据。
> 
> 以下 Oid 在其相应的数据结构中共享名为 [**WWAN \_ 列表 \_ 标头**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_list_header) 的通用可变长度列表数据结构：
> -   OID \_ WWAN \_ 就绪 \_ 信息
> -   OID \_ WWAN \_ 首选 \_ 提供程序
> -   OID \_ WWAN \_ 可见 \_ 提供程序
> -   OID \_ WWAN \_ 预配 \_ 上下文
> -   OID \_ WWAN \_ SMS \_ 读取 

## <a name="wwan-specific-indications-corresponding-data-structures-and-os-revisions"></a>特定于 WWAN 的指示、相应的数据结构和操作系统修订版本

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>指示</strong> 和 <strong>对应的数据结构</strong></p></td>
<td align="left"><p><strong>Windows 7 版本</strong></p>
<p><strong>Windows 8 修订版本</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-device-caps" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_CAPS&lt;/strong&gt;](./ndis-status-wwan-device-caps.md)"><strong>NDIS_STATUS_WWAN_DEVICE_CAPS</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_CAPS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)"> <strong>NDIS_WWAN_DEVICE_CAPS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_CAPS_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_CAPS_REVISION_2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-ready-info" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_READY_INFO&lt;/strong&gt;](./ndis-status-wwan-ready-info.md)"><strong>NDIS_STATUS_WWAN_READY_INFO</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ready_info" data-raw-source="[&lt;strong&gt;NDIS_WWAN_READY_INFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ready_info)"> <strong>NDIS_WWAN_READY_INFO</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_READY_INFO_REVISION_1</p>
<p>NDIS_WWAN_READY_INFO_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-radio-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_RADIO_STATE&lt;/strong&gt;](./ndis-status-wwan-radio-state.md)"><strong>NDIS_STATUS_WWAN_RADIO_STATE</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_RADIO_STATE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state)"> <strong>NDIS_WWAN_RADIO_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_RADIO_STATE_REVISION_1</p>
<p>NDIS_WWAN_RADIO_STATE_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-pin-info" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_INFO&lt;/strong&gt;](./ndis-status-wwan-pin-info.md)"><strong>NDIS_STATUS_WWAN_PIN_INFO</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PIN_INFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)"> <strong>NDIS_WWAN_PIN_INFO</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PIN_INFO_REVISION_1</p>
<p>NDIS_WWAN_PIN_INFO_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-pin-list" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_LIST&lt;/strong&gt;](./ndis-status-wwan-pin-list.md)"><strong>NDIS_STATUS_WWAN_PIN_LIST</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_list" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PIN_LIST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_list)"> <strong>NDIS_WWAN_PIN_LIST</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PIN_LIST_REVISION_1</p>
<p>NDIS_WWAN_PIN_LIST_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-service-activation" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SERVICE_ACTIVATION&lt;/strong&gt;](./ndis-status-wwan-service-activation.md)"><strong>NDIS_STATUS_WWAN_SERVICE_ACTIVATION</strong></a>†</p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_service_activation_status" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SERVICE_ACTIVATION_STATUS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_service_activation_status)"> <strong>NDIS_WWAN_SERVICE_ACTIVATION_STATUS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SERVICE_ACTIVATION_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SERVICE_ACTIVATION_STATUS_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-home-provider" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_HOME_PROVIDER&lt;/strong&gt;](./ndis-status-wwan-home-provider.md)"><strong>NDIS_STATUS_WWAN_HOME_PROVIDER</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider" data-raw-source="[&lt;strong&gt;NDIS_WWAN_HOME_PROVIDER&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider)"> <strong>NDIS_WWAN_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_HOME_PROVIDER_REVISION_1</p>
<p>NDIS_WWAN_HOME_PROVIDER_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-preferred-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_PROVIDERS&lt;/strong&gt;](./ndis-status-wwan-preferred-providers.md)"><strong>NDIS_STATUS_WWAN_PREFERRED_PROVIDERS</strong></a>†</p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PREFERRED_PROVIDERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers)"> <strong>NDIS_WWAN_PREFERRED_PROVIDERS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PREFERRED_PROVIDERS_REVISION_1</p>
<p>NDIS_WWAN_PREFERRED_PROVIDERS_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-visible-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](./ndis-status-wwan-visible-providers.md)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)"> <strong>NDIS_WWAN_VISIBLE_PROVIDERS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_VISIBLE_PROVIDERS_REVISION_1</p>
<p>NDIS_WWAN_VISIBLE_PROVIDERS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-register-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_REGISTER_STATE&lt;/strong&gt;](./ndis-status-wwan-register-state.md)"><strong>NDIS_STATUS_WWAN_REGISTER_STATE</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_registration_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_REGISTRATION_STATE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_registration_state)"> <strong>NDIS_WWAN_REGISTRATION_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_REGISTRATION_STATE_REVISION_1</p>
<p>NDIS_WWAN_REGISTRATION_STATE_REVISION_2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-signal-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SIGNAL_STATE&lt;/strong&gt;](./ndis-status-wwan-signal-state.md)"><strong>NDIS_STATUS_WWAN_SIGNAL_STATE</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SIGNAL_STATE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)"> <strong>NDIS_WWAN_SIGNAL_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SIGNAL_STATE_REVISION_1</p>
<p>NDIS_WWAN_SIGNAL_STATE_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-packet-service" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PACKET_SERVICE&lt;/strong&gt;](./ndis-status-wwan-packet-service.md)"><strong>NDIS_STATUS_WWAN_PACKET_SERVICE</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PACKET_SERVICE_STATE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state)"> <strong>NDIS_WWAN_PACKET_SERVICE_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PACKET_SERVICE_STATE_REVISION_1</p>
<p>NDIS_WWAN_PACKET_SERVICE_STATE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-provisioned-contexts" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS&lt;/strong&gt;](./ndis-status-wwan-provisioned-contexts.md)"><strong>NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_provisioned_contexts" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PROVISIONED_CONTEXTS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_provisioned_contexts)"> <strong>NDIS_WWAN_PROVISIONED_CONTEXTS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PROVISIONED_CONTEXTS_REVISION_1</p>
<p>NDIS_WWAN_PROVISIONED_CONTEXTS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-context-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_CONTEXT_STATE&lt;/strong&gt;](./ndis-status-wwan-context-state.md)"><strong>NDIS_STATUS_WWAN_CONTEXT_STATE</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_context_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_CONTEXT_STATE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_context_state)"> <strong>NDIS_WWAN_CONTEXT_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_CONTEXT_STATE_REVISION_1</p>
<p>NDIS_WWAN_CONTEXT_STATE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-sms-configuration" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_CONFIGURATION&lt;/strong&gt;](./ndis-status-wwan-sms-configuration.md)"><strong>NDIS_STATUS_WWAN_SMS_CONFIGURATION</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_configuration" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_CONFIGURATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_configuration)"> <strong>NDIS_WWAN_SMS_CONFIGURATION</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_CONFIGURATION_REVISION_1</p>
<p>NDIS_WWAN_SMS_CONFIGURATION_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-sms-receive" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_RECEIVE&lt;/strong&gt;](./ndis-status-wwan-sms-receive.md)"><strong>NDIS_STATUS_WWAN_SMS_RECEIVE</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_receive" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_RECEIVE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_receive)"> <strong>NDIS_WWAN_SMS_RECEIVE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_RECEIVE_REVISION_1</p>
<p>NDIS_WWAN_SMS_RECEIVE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-sms-send" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_SEND&lt;/strong&gt;](./ndis-status-wwan-sms-send.md)"><strong>NDIS_STATUS_WWAN_SMS_SEND</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_SEND_STATUS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status)"> <strong>NDIS_WWAN_SMS_SEND_STATUS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_SEND_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SMS_SEND_STATUS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-sms-delete" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_DELETE&lt;/strong&gt;](./ndis-status-wwan-sms-delete.md)"><strong>NDIS_STATUS_WWAN_SMS_DELETE</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete_status" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_DELETE_STATUS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete_status)"> <strong>NDIS_WWAN_SMS_DELETE_STATUS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_DELETE_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SMS_DELETE_STATUS_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-sms-status" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_STATUS&lt;/strong&gt;](./ndis-status-wwan-sms-status.md)"><strong>NDIS_STATUS_WWAN_SMS_STATUS</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_status" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_STATUS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_status)"> <strong>NDIS_WWAN_SMS_STATUS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SMS_STATUS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-vendor-specific" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VENDOR_SPECIFIC&lt;/strong&gt;](./ndis-status-wwan-vendor-specific.md)"><strong>NDIS_STATUS_WWAN_VENDOR_SPECIFIC</strong></a>†</p>
<p>使用供应商定义的结构</p></td>
<td align="left"><p>空值</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-ussd" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_USSD&lt;/strong&gt;](./ndis-status-wwan-ussd.md)"><strong>NDIS_STATUS_WWAN_USSD</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_event" data-raw-source="[&lt;strong&gt;NDIS_WWAN_USSD_EVENT&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_event)"> <strong>NDIS_WWAN_USSD_EVENT</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_USSD_EVENT_REVISION_1</p>
<p>NDIS_WWAN_USSD_EVENT_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS&lt;/strong&gt;](./ndis-status-wwan-device-service-supported-commands.md)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_supported_commands" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_supported_commands)"> <strong>NDIS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICES_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICES_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-device-service-response" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE&lt;/strong&gt;](./ndis-status-wwan-device-service-response.md)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_response" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_RESPONSE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_response)"> <strong>NDIS_WWAN_DEVICE_SERVICE_RESPONSE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICE_RESPONSE_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICE_RESPONSE_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-device-service-event" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT&lt;/strong&gt;](./ndis-status-wwan-device-service-event.md)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_event" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_EVENT&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_event)"> <strong>NDIS_WWAN_DEVICE_SERVICE_EVENT</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICE_EVENT_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICE_EVENT_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-device-service-subscription" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION&lt;/strong&gt;](./ndis-status-wwan-device-service-subscription.md)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_subscription" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_subscription)"> <strong>NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-auth-response" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_AUTH_RESPONSE&lt;/strong&gt;](./ndis-status-wwan-auth-response.md)"><strong>NDIS_STATUS_WWAN_AUTH_RESPONSE</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_auth_response" data-raw-source="[&lt;strong&gt;NDIS_WWAN_AUTH_RESPONSE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_auth_response)"> <strong>NDIS_WWAN_AUTH_RESPONSE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_AUTH_RESPONSE_REVISION_1</p>
<p>NDIS_WWAN_AUTH_RESPONSE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-set-home-provider-complete" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE&lt;/strong&gt;](./ndis-status-wwan-set-home-provider-complete.md)"><strong>NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_home_provider" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SET_HOME_PROVIDER&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_home_provider)"> <strong>NDIS_WWAN_SET_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>空值</p>
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
<td align="left"><p><strong>指示</strong></p></td>
<td align="left"><p><strong>GSM</strong></p></td>
<td align="left"><p><strong>CDMA</strong></p></td>
<td align="left"><p><strong>依靠</strong></p>
<p><strong>有人</strong></p>
<p><strong>获准?</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-device-caps" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_CAPS&lt;/strong&gt;](./ndis-status-wwan-device-caps.md)"><strong>NDIS_STATUS_WWAN_DEVICE_CAPS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-ready-info" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_READY_INFO&lt;/strong&gt;](./ndis-status-wwan-ready-info.md)"><strong>NDIS_STATUS_WWAN_READY_INFO</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-radio-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_RADIO_STATE&lt;/strong&gt;](./ndis-status-wwan-radio-state.md)"><strong>NDIS_STATUS_WWAN_RADIO_STATE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-pin-info" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_INFO&lt;/strong&gt;](./ndis-status-wwan-pin-info.md)"><strong>NDIS_STATUS_WWAN_PIN_INFO</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-pin-list" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_LIST&lt;/strong&gt;](./ndis-status-wwan-pin-list.md)"><strong>NDIS_STATUS_WWAN_PIN_LIST</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-service-activation" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SERVICE_ACTIVATION&lt;/strong&gt;](./ndis-status-wwan-service-activation.md)"><strong>NDIS_STATUS_WWAN_SERVICE_ACTIVATION</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-home-provider" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_HOME_PROVIDER&lt;/strong&gt;](./ndis-status-wwan-home-provider.md)"><strong>NDIS_STATUS_WWAN_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-preferred-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_PROVIDERS&lt;/strong&gt;](./ndis-status-wwan-preferred-providers.md)"><strong>NDIS_STATUS_WWAN_PREFERRED_PROVIDERS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-visible-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](./ndis-status-wwan-visible-providers.md)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-register-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_REGISTER_STATE&lt;/strong&gt;](./ndis-status-wwan-register-state.md)"><strong>NDIS_STATUS_WWAN_REGISTER_STATE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-signal-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SIGNAL_STATE&lt;/strong&gt;](./ndis-status-wwan-signal-state.md)"><strong>NDIS_STATUS_WWAN_SIGNAL_STATE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-packet-service" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PACKET_SERVICE&lt;/strong&gt;](./ndis-status-wwan-packet-service.md)"><strong>NDIS_STATUS_WWAN_PACKET_SERVICE</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PACKET_SERVICE_STATE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state)"> <strong>NDIS_WWAN_PACKET_SERVICE_STATE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-provisioned-contexts" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS&lt;/strong&gt;](./ndis-status-wwan-provisioned-contexts.md)"><strong>NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-context-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_CONTEXT_STATE&lt;/strong&gt;](./ndis-status-wwan-context-state.md)"><strong>NDIS_STATUS_WWAN_CONTEXT_STATE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-sms-configuration" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_CONFIGURATION&lt;/strong&gt;](./ndis-status-wwan-sms-configuration.md)"><strong>NDIS_STATUS_WWAN_SMS_CONFIGURATION</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-sms-receive" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_RECEIVE&lt;/strong&gt;](./ndis-status-wwan-sms-receive.md)"><strong>NDIS_STATUS_WWAN_SMS_RECEIVE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-sms-send" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_SEND&lt;/strong&gt;](./ndis-status-wwan-sms-send.md)"><strong>NDIS_STATUS_WWAN_SMS_SEND</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_SEND_STATUS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status)"> <strong>NDIS_WWAN_SMS_SEND_STATUS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-sms-delete" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_DELETE&lt;/strong&gt;](./ndis-status-wwan-sms-delete.md)"><strong>NDIS_STATUS_WWAN_SMS_DELETE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-sms-status" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_STATUS&lt;/strong&gt;](./ndis-status-wwan-sms-status.md)"><strong>NDIS_STATUS_WWAN_SMS_STATUS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-vendor-specific" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VENDOR_SPECIFIC&lt;/strong&gt;](./ndis-status-wwan-vendor-specific.md)"><strong>NDIS_STATUS_WWAN_VENDOR_SPECIFIC</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-ussd" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_USSD&lt;/strong&gt;](./ndis-status-wwan-ussd.md)"><strong>NDIS_STATUS_WWAN_USSD</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS&lt;/strong&gt;](./ndis-status-wwan-device-service-supported-commands.md)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-device-service-response" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE&lt;/strong&gt;](./ndis-status-wwan-device-service-response.md)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-device-service-event" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT&lt;/strong&gt;](./ndis-status-wwan-device-service-event.md)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-device-service-subscription" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION&lt;/strong&gt;](./ndis-status-wwan-device-service-subscription.md)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-auth-response" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_AUTH_RESPONSE&lt;/strong&gt;](./ndis-status-wwan-auth-response.md)"><strong>NDIS_STATUS_WWAN_AUTH_RESPONSE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-set-home-provider-complete" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE&lt;/strong&gt;](./ndis-status-wwan-set-home-provider-complete.md)"><strong>NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE</strong></a></p></td>
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
<td align="left"><p><strong>OID</strong> 和 <strong>Windows 8 相应的数据结构</strong></p></td>
<td align="left"><p><strong>查询操作</strong></p></td>
<td align="left"><p><strong>设置操作</strong></p></td>
<td align="left"><p><strong>GSM/CDMA</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-wwan-home-provider" data-raw-source="[OID_WWAN_HOME_PROVIDER](./oid-wwan-home-provider.md)">OID_WWAN_HOME_PROVIDER</a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_home_provider" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SET_HOME_PROVIDER&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_home_provider)"> <strong>NDIS_WWAN_SET_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>包含当前请求的 URL 的</p></td>
<td align="left"><p>包含当前请求的 URL 的</p></td>
<td align="left"><p>GSM，CDMA</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-wwan-preferred-providers" data-raw-source="[OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS](./oid-wwan-preferred-providers.md)">OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</a></p>
<p>使用 <a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_preferred_multicarrier_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SET_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_preferred_multicarrier_providers)"><strong>NDIS_WWAN_SET_PREFERRED_MULTICARRIER_PROVIDERS</strong></a>。 应将 <strong>PreferredListHeader</strong> 设置为 <strong>WwanStructProvider2</strong> ，并 WWAN_PROVIDER2 结构。</p></td>
<td align="left"><p>包含当前请求的 URL 的</p></td>
<td align="left"><p>包含当前请求的 URL 的</p></td>
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
<td align="left"><p><strong>指示</strong> 和 <strong>对应的数据结构</strong></p></td>
<td align="left"><p><strong>Windows 8 修订版本</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-home-provider" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_HOME_PROVIDER&lt;/strong&gt;](./ndis-status-wwan-home-provider.md)"><strong>NDIS_STATUS_WWAN_HOME_PROVIDER</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider2" data-raw-source="[&lt;strong&gt;NDIS_WWAN_HOME_PROVIDER2&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_home_provider2)"> <strong>NDIS_WWAN_HOME_PROVIDER2</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_HOME_PROVIDER_REVISION_2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-preferred-multicarrier-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](./ndis-status-wwan-preferred-multicarrier-providers.md)"><strong>NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers)"> <strong>NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS_REVISION_1。 应将 <strong>PreferredListHeader</strong> 设置为 <strong>WwanStructProvider2</strong> ，并且列表应包含 WWAN_PROVIDER2 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-visible-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](./ndis-status-wwan-visible-providers.md)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)"> <strong>NDIS_WWAN_VISIBLE_PROVIDERS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_VISIBLE_PROVIDERS_REVISION_1。 应将 <strong>VisibleListHeader</strong> 设置为 <strong>WwanStructProvider2</strong> ，并且列表应包含 WWAN_PROVIDER2 结构。</p></td>
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
<td align="left"><p><strong>指示</strong> 和 <strong>对应的数据结构</strong></p></td>
<td align="left"><p><strong>GSM</strong></p></td>
<td align="left"><p><strong>CDMA</strong></p></td>
<td align="left"><p><strong>依靠</strong></p>
<p><strong>有人</strong></p>
<p><strong>获准?</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-home-provider" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_HOME_PROVIDER&lt;/strong&gt;](./ndis-status-wwan-home-provider.md)"><strong>NDIS_STATUS_WWAN_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-preferred-multicarrier-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](./ndis-status-wwan-preferred-multicarrier-providers.md)"><strong>NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/network/ndis-status-wwan-visible-providers" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](./ndis-status-wwan-visible-providers.md)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p>
<p>使用<a href="/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers" data-raw-source="[&lt;strong&gt;NDIS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)"> <strong>NDIS_WWAN_VISIBLE_PROVIDERS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
</tbody>
</table>