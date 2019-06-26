---
title: WDI 属性 OID
description: 本部分包含 WDI 属性 Oid。
ms.assetid: 1B1B54B8-6CE4-4C17-AAF8-7394210B09E8
ms.date: 07/18/2017
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 4c67c049e0b3bf54f5d7d1db2bc55a03339b3a49
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387201"
---
# <a name="wdi-property-oids"></a>WDI 属性 OID


本部分包含 WDI 属性 Oid。

Wi-fi 驱动程序接口 (WDI) 对象标识符 (Oid) 仅适用于实现 WDI 的微型端口驱动程序。

下表指定 WDI OID 查询 (Q)、 集 (S) 和 NDIS 6.0 (M) 的方法请求是否为必需或可选的实现：

<a href="" id="r"></a>**R**  
表示支持的对象是必需的。 微型端口驱动程序不得失败的对象集或查询请求通过返回状态代码 NDIS\_状态\_不\_支持从其[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)函数。

<a href="" id="o"></a>**O**  
指示该功能的支持，该对象是可选的。 或微型端口驱动程序可以支持的查询或设置请求的对象，该驱动程序可以使该请求失败通过返回 NDIS\_状态\_不\_支持从其[ *MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)函数。

| 名称                                                                                                | Q   | S   | M   |
|-----------------------------------------------------------------------------------------------------|-----|-----|-----|
| [OID\_WDI\_ABORT\_TASK](oid-wdi-abort-task.md)                                                     |     |     | R   |
| [OID\_WDI\_获取\_适配器\_功能](oid-wdi-get-adapter-capabilities.md)                        |     |     | R   |
| [OID\_WDI\_GET\_AUTO\_POWER\_SAVE](oid-wdi-get-auto-power-save.md)                                 |     |     | R   |
| [OID\_WDI\_GET\_BSS\_ENTRY\_LIST](oid-wdi-get-bss-entry-list.md)                                   |     |     | O   |
| [OID\_WDI\_GET\_NEXT\_ACTION\_FRAME\_DIALOG\_TOKEN](oid-wdi-get-next-action-frame-dialog-token.md) |     |     | O   |
| [OID\_WDI\_GET\_PM\_PROTOCOL\_OFFLOAD](oid-wdi-get-pm-protocol-offload.md)                         |     |     | O   |
| [OID\_WDI\_GET\_RECEIVE\_COALESCING\_MATCH\_COUNT](oid-wdi-get-receive-coalescing-match-count.md)  |     |     | O   |
| [OID\_WDI\_GET\_STATISTICS](oid-wdi-get-statistics.md)                                             |     |     | R   |
| [OID\_WDI\_IHV\_REQUEST](oid-wdi-ihv-request.md)                                                   |     |     | O   |
| [OID\_WDI\_设置\_适配器\_配置](oid-wdi-set-adapter-configuration.md)                      |     |     | R   |
| [OID\_WDI\_SET\_ADD\_CIPHER\_KEYS](oid-wdi-set-add-cipher-keys.md)                                 |     |     | R   |
| [OID\_WDI\_SET\_ADD\_PM\_PROTOCOL\_OFFLOAD](oid-wdi-set-add-pm-protocol-offload.md)                |     |     | O   |
| [OID\_WDI\_SET\_ADD\_WOL\_PATTERN](oid-wdi-set-add-wol-pattern.md)                                 |     |     | O   |
| [OID\_WDI\_设置\_播发\_信息](oid-wdi-set-advertisement-information.md)              |     |     | O   |
| [OID\_WDI\_设置\_关联\_参数](oid-wdi-set-association-parameters.md)                    |     |     | R   |
| [OID\_WDI\_SET\_CLEAR\_RECEIVE\_COALESCING](oid-wdi-set-clear-receive-coalescing.md)               |     |     | O   |
| [OID\_WDI\_设置\_连接\_质量](oid-wdi-set-connection-quality.md)                            |     |     | R   |
| [OID\_WDI\_SET\_DEFAULT\_KEY\_ID](oid-wdi-set-default-key-id.md)                                   |     |     | R   |
| [OID\_WDI\_SET\_DELETE\_CIPHER\_KEYS](oid-wdi-set-delete-cipher-keys.md)                           |     |     | R   |
| [OID\_WDI\_SET\_ENCAPSULATION\_OFFLOAD](oid-wdi-set-encapsulation-offload.md)                      |     |     | O   |
| [OID\_WDI\_设置\_刷新\_BSS\_条目](oid-wdi-set-flush-bss-entry.md)                                 |     |     | O   |
| [OID\_WDI\_SET\_MULTICAST\_LIST](oid-wdi-set-multicast-list.md)                                    |     |     | R   |
| [OID\_WDI\_SET\_NETWORK\_LIST\_OFFLOAD](oid-wdi-set-network-list-offload.md)                       |     |     | O   |
| [OID\_WDI\_SET\_P2P\_LISTEN\_STATE](oid-wdi-set-p2p-listen-state.md)                               |     |     | O   |
| [OID\_WDI\_设置\_P2P\_启动\_背景\_发现](oid-wdi-set-p2p-start-background-discovery.md)  |     |     | O   |
| [OID\_WDI\_设置\_P2P\_停止\_背景\_发现](oid-wdi-set-p2p-stop-background-discovery.md)    |     |     | O   |
| [OID\_WDI\_SET\_P2P\_WPS\_ENABLED](oid-wdi-set-p2p-wps-enabled.md)                                 |     |     | O   |
| [OID\_WDI\_SET\_POWER\_STATE](oid-wdi-set-power-state.md)                                          |     |     | R   |
| [OID\_WDI\_设置\_隐私\_免除\_列表](oid-wdi-set-privacy-exemption-list.md)                   |     |     | R   |
| [OID\_WDI\_SET\_RECEIVE\_COALESCING](oid-wdi-set-receive-coalescing.md)                            |     |     | O   |
| [OID\_WDI\_SET\_RECEIVE\_PACKET\_FILTER](oid-wdi-set-receive-packet-filter.md)                     |     |     | R   |
| [OID\_WDI\_SET\_REMOVE\_PM\_PROTOCOL\_OFFLOAD](oid-wdi-set-remove-pm-protocol-offload.md)          |     |     | O   |
| [OID\_WDI\_SET\_REMOVE\_WOL\_PATTERN](oid-wdi-set-remove-wol-pattern.md)                           |     |     | O   |
| [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)                                      |     |     | O   |
| [OID\_WDI\_SET\_TCP\_OFFLOAD\_PARAMETERS](oid-wdi-set-tcp-offload-parameters.md)                   |     |     | O   |
| [OID\_WDI\_TCP\_RSC\_STATISTICS](oid-wdi-tcp-rsc-statistics.md)                                    |     |     | O   |

 

 

 




