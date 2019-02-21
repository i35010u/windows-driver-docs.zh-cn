---
title: MB 数据模型
description: MB 数据模型
ms.assetid: 922b6b55-c332-4721-bbd1-571b0e154df3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc3dd2bed0ba8d236447879c7bacc2445ddbf991
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542522"
---
# <a name="mb-data-model"></a>MB 数据模型


MB 驱动程序模型使用的对象定义为抽象的 MB 设备功能的一组组成的数据模型。 每个对象的唯一对象标识符 (OID) 标识，由相应的属性的一组定义。 一组属性组织到一个数据结构。 若要管理设备，MB 服务和 MB 微型端口驱动程序交换 Oid 和基于 OID 请求并提供通过网络驱动程序接口规范 (NDIS) 指示其关联的数据结构。

在 MB 驱动程序模型中，仅*设置*并*查询*操作用于 OID 请求。 MB 驱动程序模型不使用*方法*操作。 迹象，MB 驱动程序模型将使用事件和事务通知来指示的 MB 设备对象中的状态更改。 事务通知还指示异步事务已完成。

下表列出的 Oid 和状态指示为 MB 微型端口驱动程序，以及关联的数据结构定义。 MB 微型端口驱动程序必须实现所有必需的常规 Oid 的 NDIS 6.20 规范要求。 有关一系列常规 Oid ndis 6.x，请参阅[常规操作 Oid](https://msdn.microsoft.com/library/windows/hardware/ff552474)。

此外，MB 微型端口驱动程序必须实现 OID\_GEN\_物理\_中等即使 NDIS 规范描述为可选实现也是如此。

中所述的语法和语义下表中列出了 MB Oid [MB 的操作语义](mb-operational-semantics.md)。 MB 服务和 MB 微型端口驱动程序之间的交互中所述[MB 操作流程图](mb-operation-flowcharts.md)。

## <a name="wwan-specific-oids"></a>特定于 WWAN 的 Oid

| OID 和相应的数据结构 | 设置操作 |   | 查询操作 |   | GSM/CDMA |
| ---                                  | ---       | ---       | ---       | ---       |--- |
|                                      | Windows 7 | Windows 8 | Windows 7 | Windows 8 |    |
| [OID\_WWAN\_驱动程序\_CAP](https://msdn.microsoft.com/library/windows/hardware/ff569825)使用[ **NDIS\_WWAN\_驱动程序\_CAP**](https://msdn.microsoft.com/library/windows/hardware/ff567908) | 不支持 | 不支持 |S | S | GSM, CDMA |
| [OID\_WWAN\_设备\_CAPS](https://msdn.microsoft.com/library/windows/hardware/ff569824)没有相应的结构 | 不支持 | 不支持 | A | A | GSM, CDMA |
| [OID\_WWAN\_准备\_信息](https://msdn.microsoft.com/library/windows/hardware/ff569833)没有相应的结构 | 不支持的不受支持 | A | A | GSM, CDMA |
| [OID\_WWAN\_服务\_激活](https://msdn.microsoft.com/library/windows/hardware/ff569835)† 使用[ **NDIS\_WWAN\_服务\_激活**](https://msdn.microsoft.com/library/windows/hardware/ff567918) | A | A | 不支持 | 不支持 | GSM, CDMA |
| [OID\_WWAN\_单选\_状态](https://msdn.microsoft.com/library/windows/hardware/ff569832)使用[ **NDIS\_WWAN\_设置\_单选\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567925) | A | A | A | A | GSM, CDMA |
| [OID\_WWAN\_PIN](https://msdn.microsoft.com/library/windows/hardware/ff569828)使用[ **NDIS\_WWAN\_设置\_PIN**](https://msdn.microsoft.com/library/windows/hardware/ff567922) | A | 不支持 | A | 不支持 | GSM, CDMA |
| [OID\_WWAN\_PIN\_列表](https://msdn.microsoft.com/library/windows/hardware/ff569829)没有相应的结构 | 不支持 | 不支持 | A | A | GSM, CDMA |
| [OID\_WWAN\_PIN\_EX](https://msdn.microsoft.com/library/windows/hardware/hh440095)使用[ **NDIS\_WWAN\_设置\_PIN\_EX**](https://msdn.microsoft.com/library/windows/hardware/hh439842) | 不支持 | A | 不支持 | A | GSM, CDMA |
| [OID\_WWAN\_主页\_提供程序](https://msdn.microsoft.com/library/windows/hardware/ff569826)没有相应的结构 | 不支持 | 不支持 | A | A | GSM, CDMA |
| [OID\_WWAN\_PREFERRED\_提供程序](https://msdn.microsoft.com/library/windows/hardware/ff569830)† 使用[ **NDIS\_WWAN\_设置\_首选\_提供程序**](https://msdn.microsoft.com/library/windows/hardware/ff567923) | A | A | A | A | 仅使用 GSM |
| [OID\_WWAN\_VISIBLE\_提供程序](https://msdn.microsoft.com/library/windows/hardware/ff569843)没有相应的结构 | 不支持 | 不支持 | A | A | GSM |
| [OID\_WWAN\_注册\_状态](https://msdn.microsoft.com/library/windows/hardware/ff569834)使用[ **NDIS\_WWAN\_设置\_注册\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567926) | A | A | A | A | CDMA |
| [OID\_WWAN\_信号\_状态](https://msdn.microsoft.com/library/windows/hardware/ff569836)使用[ **NDIS\_WWAN\_设置\_信号\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567928) | A | A | A | A | GSM, CDMA |
| [OID\_WWAN\_数据包\_服务](https://msdn.microsoft.com/library/windows/hardware/ff569827)使用[ **NDIS\_WWAN\_设置\_数据包\_服务**](https://msdn.microsoft.com/library/windows/hardware/ff567921) | A | A | A | A | GSM, CDMA |
| [OID\_WWAN\_已预配\_上下文](https://msdn.microsoft.com/library/windows/hardware/ff569831)† 使用[ **NDIS\_WWAN\_设置\_已预配\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff567924) | A | A | A | A | GSM, CDMA |
| [OID\_WWAN\_CONNECT](https://msdn.microsoft.com/library/windows/hardware/ff569823)使用[ **NDIS\_WWAN\_设置\_上下文\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567920) | A | A | A | A | GSM, CDMA |
| [OID\_WWAN\_SMS\_配置](https://msdn.microsoft.com/library/windows/hardware/ff569837)使用[ **NDIS\_WWAN\_设置\_SMS\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff567929) | A | A | A | A | GSM, CDMA | 
| [OID\_WWAN\_SMS\_读取](https://msdn.microsoft.com/library/windows/hardware/ff569839)使用[ **NDIS\_WWAN\_SMS\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff567941) | 不支持 | A | A | A |GSM, CDMA | 
| [OID\_WWAN\_SMS\_发送](https://msdn.microsoft.com/library/windows/hardware/ff569840)使用[ **NDIS\_WWAN\_SMS\_发送**](https://msdn.microsoft.com/library/windows/hardware/ff567943) | A | A | 不支持 | 不支持 | GSM, CDMA |
| [OID\_WWAN\_SMS\_删除](https://msdn.microsoft.com/library/windows/hardware/ff569838)使用[ **NDIS\_WWAN\_SMS\_删除**](https://msdn.microsoft.com/library/windows/hardware/ff567938) | A | A | 不支持 | 不支持 |  GSM, CDMA |
| [OID\_WWAN\_SMS\_状态](https://msdn.microsoft.com/library/windows/hardware/ff569841)使用[ **NDIS\_WWAN\_SMS\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567945) | 不支持 | 不支持 | A | A | GSM, CDMA |
| [OID\_WWAN\_供应商\_特定](https://msdn.microsoft.com/library/windows/hardware/ff569842)† 使用供应商定义的结构 | A | A | 不支持 | 不支持 | GSM, CDMA |
| [OID\_WWAN\_设备\_服务](https://msdn.microsoft.com/library/windows/hardware/hh440093)没有相应的结构 | 不支持 | 不支持 | 不支持 | A | GSM, CDMA |
| [OID\_WWAN\_SUBSCRIBE\_设备\_服务\_事件](https://msdn.microsoft.com/library/windows/hardware/hh440096)使用[ **NDIS\_WWAN\_订阅\_设备\_服务\_事件**](https://msdn.microsoft.com/library/windows/hardware/hh439843) | 不支持 | A | 不支持 | 不支持 | GSM, CDMA |
| [OID\_WWAN\_身份验证\_质询](https://msdn.microsoft.com/library/windows/hardware/hh440092)使用[ **NDIS\_WWAN\_身份验证\_质询**](https://msdn.microsoft.com/library/windows/hardware/hh439833) | 不支持 | 不支持 | 不支持 | A | GSM, CDMA |
| [OID\_WWAN\_USSD](https://msdn.microsoft.com/library/windows/hardware/hh440100)使用[ **NDIS\_WWAN\_USSD\_请求**](https://msdn.microsoft.com/library/windows/hardware/hh439846) | 不支持 | A | 不支持 | 不支持 | GSM |
| [OID\_WWAN\_设备\_服务\_命令](https://msdn.microsoft.com/library/windows/hardware/hh440094)使用[ **NDIS\_WWAN\_设备\_服务\_命令**](https://msdn.microsoft.com/library/windows/hardware/hh439836) | 不支持 | A | 不支持 | A| GSM, CDMA |

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
> 以下 Oid 共享常见的可变长度列表数据结构称为[ **WWAN\_列表\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff571208)其对应的数据结构中：
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567845" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_CAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567845)"><strong>NDIS_STATUS_WWAN_DEVICE_CAPS</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567907" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_CAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567907)"> <strong>NDIS_WWAN_DEVICE_CAPS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_CAPS_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_CAPS_REVISION_2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567856" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_READY_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567856)"><strong>NDIS_STATUS_WWAN_READY_INFO</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567916" data-raw-source="[&lt;strong&gt;NDIS_WWAN_READY_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567916)"> <strong>NDIS_WWAN_READY_INFO</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_READY_INFO_REVISION_1</p>
<p>NDIS_WWAN_READY_INFO_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567855" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_RADIO_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567855)"><strong>NDIS_STATUS_WWAN_RADIO_STATE</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567915" data-raw-source="[&lt;strong&gt;NDIS_WWAN_RADIO_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567915)"> <strong>NDIS_WWAN_RADIO_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_RADIO_STATE_REVISION_1</p>
<p>NDIS_WWAN_RADIO_STATE_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567851" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567851)"><strong>NDIS_STATUS_WWAN_PIN_INFO</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567911" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PIN_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567911)"> <strong>NDIS_WWAN_PIN_INFO</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PIN_INFO_REVISION_1</p>
<p>NDIS_WWAN_PIN_INFO_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567852" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_LIST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567852)"><strong>NDIS_STATUS_WWAN_PIN_LIST</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567912" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PIN_LIST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567912)"> <strong>NDIS_WWAN_PIN_LIST</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PIN_LIST_REVISION_1</p>
<p>NDIS_WWAN_PIN_LIST_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567858" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SERVICE_ACTIVATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567858)"><strong>NDIS_STATUS_WWAN_SERVICE_ACTIVATION</strong></a>†</p>
<p>uses <a href="https://msdn.microsoft.com/library/windows/hardware/ff567919" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SERVICE_ACTIVATION_STATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567919)"><strong>NDIS_WWAN_SERVICE_ACTIVATION_STATUS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SERVICE_ACTIVATION_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SERVICE_ACTIVATION_STATUS_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567848" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567848)"><strong>NDIS_STATUS_WWAN_HOME_PROVIDER</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567909" data-raw-source="[&lt;strong&gt;NDIS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567909)"> <strong>NDIS_WWAN_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_HOME_PROVIDER_REVISION_1</p>
<p>NDIS_WWAN_HOME_PROVIDER_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567853" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567853)"><strong>NDIS_STATUS_WWAN_PREFERRED_PROVIDERS</strong></a>†</p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567913" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PREFERRED_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567913)"> <strong>NDIS_WWAN_PREFERRED_PROVIDERS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PREFERRED_PROVIDERS_REVISION_1</p>
<p>NDIS_WWAN_PREFERRED_PROVIDERS_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567866" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567866)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567948" data-raw-source="[&lt;strong&gt;NDIS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567948)"> <strong>NDIS_WWAN_VISIBLE_PROVIDERS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_VISIBLE_PROVIDERS_REVISION_1</p>
<p>NDIS_WWAN_VISIBLE_PROVIDERS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567857" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_REGISTER_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567857)"><strong>NDIS_STATUS_WWAN_REGISTER_STATE</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567917" data-raw-source="[&lt;strong&gt;NDIS_WWAN_REGISTRATION_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567917)"> <strong>NDIS_WWAN_REGISTRATION_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_REGISTRATION_STATE_REVISION_1</p>
<p>NDIS_WWAN_REGISTRATION_STATE_REVISION_2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567859" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SIGNAL_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567859)"><strong>NDIS_STATUS_WWAN_SIGNAL_STATE</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567931" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SIGNAL_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567931)"> <strong>NDIS_WWAN_SIGNAL_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SIGNAL_STATE_REVISION_1</p>
<p>NDIS_WWAN_SIGNAL_STATE_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567850" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PACKET_SERVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567850)"><strong>NDIS_STATUS_WWAN_PACKET_SERVICE</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567910" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PACKET_SERVICE_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567910)"> <strong>NDIS_WWAN_PACKET_SERVICE_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PACKET_SERVICE_STATE_REVISION_1</p>
<p>NDIS_WWAN_PACKET_SERVICE_STATE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567854" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567854)"><strong>NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567914" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PROVISIONED_CONTEXTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567914)"> <strong>NDIS_WWAN_PROVISIONED_CONTEXTS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PROVISIONED_CONTEXTS_REVISION_1</p>
<p>NDIS_WWAN_PROVISIONED_CONTEXTS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567843" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_CONTEXT_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567843)"><strong>NDIS_STATUS_WWAN_CONTEXT_STATE</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567906" data-raw-source="[&lt;strong&gt;NDIS_WWAN_CONTEXT_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567906)"> <strong>NDIS_WWAN_CONTEXT_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_CONTEXT_STATE_REVISION_1</p>
<p>NDIS_WWAN_CONTEXT_STATE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567860" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_CONFIGURATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567860)"><strong>NDIS_STATUS_WWAN_SMS_CONFIGURATION</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567935" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_CONFIGURATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567935)"> <strong>NDIS_WWAN_SMS_CONFIGURATION</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_CONFIGURATION_REVISION_1</p>
<p>NDIS_WWAN_SMS_CONFIGURATION_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567862" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_RECEIVE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567862)"><strong>NDIS_STATUS_WWAN_SMS_RECEIVE</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567942" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_RECEIVE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567942)"> <strong>NDIS_WWAN_SMS_RECEIVE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_RECEIVE_REVISION_1</p>
<p>NDIS_WWAN_SMS_RECEIVE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567863" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_SEND&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567863)"><strong>NDIS_STATUS_WWAN_SMS_SEND</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567944" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_SEND_STATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567944)"> <strong>NDIS_WWAN_SMS_SEND_STATUS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_SEND_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SMS_SEND_STATUS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567861" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_DELETE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567861)"><strong>NDIS_STATUS_WWAN_SMS_DELETE</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567940" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_DELETE_STATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567940)"> <strong>NDIS_WWAN_SMS_DELETE_STATUS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_DELETE_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SMS_DELETE_STATUS_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567864" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_STATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567864)"><strong>NDIS_STATUS_WWAN_SMS_STATUS</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567945" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_STATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567945)"> <strong>NDIS_WWAN_SMS_STATUS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SMS_STATUS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567865" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VENDOR_SPECIFIC&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567865)"><strong>NDIS_STATUS_WWAN_VENDOR_SPECIFIC</strong></a>†</p>
<p>使用供应商定义的结构</p></td>
<td align="left"><p>不适用</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439822" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_USSD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439822)"><strong>NDIS_STATUS_WWAN_USSD</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/hh439844" data-raw-source="[&lt;strong&gt;NDIS_WWAN_USSD_EVENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439844)"> <strong>NDIS_WWAN_USSD_EVENT</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_USSD_EVENT_REVISION_1</p>
<p>NDIS_WWAN_USSD_EVENT_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh846210" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846210)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/hh846214" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846214)"> <strong>NDIS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICES_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICES_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh846205" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846205)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/hh439838" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_RESPONSE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439838)"> <strong>NDIS_WWAN_DEVICE_SERVICE_RESPONSE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICE_RESPONSE_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICE_RESPONSE_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh846204" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846204)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/hh439837" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_EVENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439837)"> <strong>NDIS_WWAN_DEVICE_SERVICE_EVENT</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICE_EVENT_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICE_EVENT_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh846209" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846209)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/hh439839" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439839)"> <strong>NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439821" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_AUTH_RESPONSE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439821)"><strong>NDIS_STATUS_WWAN_AUTH_RESPONSE</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/hh439834" data-raw-source="[&lt;strong&gt;NDIS_WWAN_AUTH_RESPONSE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439834)"> <strong>NDIS_WWAN_AUTH_RESPONSE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_AUTH_RESPONSE_REVISION_1</p>
<p>NDIS_WWAN_AUTH_RESPONSE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh846212" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846212)"><strong>NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/hh439841" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SET_HOME_PROVIDER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439841)"> <strong>NDIS_WWAN_SET_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>不适用</p>
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567845" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_CAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567845)"><strong>NDIS_STATUS_WWAN_DEVICE_CAPS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567856" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_READY_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567856)"><strong>NDIS_STATUS_WWAN_READY_INFO</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567855" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_RADIO_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567855)"><strong>NDIS_STATUS_WWAN_RADIO_STATE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567851" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567851)"><strong>NDIS_STATUS_WWAN_PIN_INFO</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567852" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_LIST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567852)"><strong>NDIS_STATUS_WWAN_PIN_LIST</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567858" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SERVICE_ACTIVATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567858)"><strong>NDIS_STATUS_WWAN_SERVICE_ACTIVATION</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567848" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567848)"><strong>NDIS_STATUS_WWAN_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567853" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567853)"><strong>NDIS_STATUS_WWAN_PREFERRED_PROVIDERS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567866" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567866)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567857" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_REGISTER_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567857)"><strong>NDIS_STATUS_WWAN_REGISTER_STATE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567859" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SIGNAL_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567859)"><strong>NDIS_STATUS_WWAN_SIGNAL_STATE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567850" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PACKET_SERVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567850)"><strong>NDIS_STATUS_WWAN_PACKET_SERVICE</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567910" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PACKET_SERVICE_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567910)"> <strong>NDIS_WWAN_PACKET_SERVICE_STATE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567854" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567854)"><strong>NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567843" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_CONTEXT_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567843)"><strong>NDIS_STATUS_WWAN_CONTEXT_STATE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567860" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_CONFIGURATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567860)"><strong>NDIS_STATUS_WWAN_SMS_CONFIGURATION</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567862" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_RECEIVE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567862)"><strong>NDIS_STATUS_WWAN_SMS_RECEIVE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567863" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_SEND&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567863)"><strong>NDIS_STATUS_WWAN_SMS_SEND</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567944" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_SEND_STATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567944)"> <strong>NDIS_WWAN_SMS_SEND_STATUS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567861" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_DELETE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567861)"><strong>NDIS_STATUS_WWAN_SMS_DELETE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567864" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_STATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567864)"><strong>NDIS_STATUS_WWAN_SMS_STATUS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567865" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VENDOR_SPECIFIC&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567865)"><strong>NDIS_STATUS_WWAN_VENDOR_SPECIFIC</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439822" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_USSD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439822)"><strong>NDIS_STATUS_WWAN_USSD</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh846210" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846210)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh846205" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846205)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh846204" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846204)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh846209" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846209)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439821" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_AUTH_RESPONSE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439821)"><strong>NDIS_STATUS_WWAN_AUTH_RESPONSE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh846212" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846212)"><strong>NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE</strong></a></p></td>
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569826" data-raw-source="[OID_WWAN_HOME_PROVIDER](https://msdn.microsoft.com/library/windows/hardware/ff569826)">OID_WWAN_HOME_PROVIDER</a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/hh439841" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SET_HOME_PROVIDER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439841)"> <strong>NDIS_WWAN_SET_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>A</p></td>
<td align="left"><p>A</p></td>
<td align="left"><p>GSM, CDMA</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569830" data-raw-source="[OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS](https://msdn.microsoft.com/library/windows/hardware/ff569830)">OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/hh831866" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SET_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh831866)"> <strong>NDIS_WWAN_SET_PREFERRED_MULTICARRIER_PROVIDERS</strong></a>。 <strong>PreferredListHeader.ElementType</strong>应设置为<strong>WwanStructProvider2</strong>而且结构 WWAN_PROVIDER2。</p></td>
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567848" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567848)"><strong>NDIS_STATUS_WWAN_HOME_PROVIDER</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/hh439840" data-raw-source="[&lt;strong&gt;NDIS_WWAN_HOME_PROVIDER2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439840)"> <strong>NDIS_WWAN_HOME_PROVIDER2</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_HOME_PROVIDER_REVISION_2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh846211" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846211)"><strong>NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/hh831864" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh831864)"> <strong>NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS_REVISION_1. <strong>PreferredListHeader.ElementType</strong>应设置为<strong>WwanStructProvider2</strong>列表应包含 WWAN_PROVIDER2 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567866" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567866)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567948" data-raw-source="[&lt;strong&gt;NDIS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567948)"> <strong>NDIS_WWAN_VISIBLE_PROVIDERS</strong></a></p></td>
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567848" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567848)"><strong>NDIS_STATUS_WWAN_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh846211" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846211)"><strong>NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567866" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567866)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567948" data-raw-source="[&lt;strong&gt;NDIS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567948)"> <strong>NDIS_WWAN_VISIBLE_PROVIDERS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
</tbody>
</table>
