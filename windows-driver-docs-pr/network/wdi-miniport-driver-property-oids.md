---
title: WDI 属性 OID
description: 本部分包含 WDI 属性 Oid。
ms.assetid: 1B1B54B8-6CE4-4C17-AAF8-7394210B09E8
ms.date: 07/18/2017
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: dc215bc96c813c97b372f125d07f0110df6768e7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842918"
---
# <a name="wdi-property-oids"></a>WDI 属性 OID


本部分包含 WDI 属性 Oid。

Wi-fi 驱动程序接口（WDI）对象标识符（Oid）仅适用于实现 WDI 的微型端口驱动程序。

下表指定 WDI OID query （Q）、set （S）和 NDIS 6.0 方法（M）请求是否必需或可选来实现：

<a href="" id="r"></a>**迅驰**  
指示对对象的支持是必需的。 微型端口驱动程序不能通过返回状态代码 "NDIS\_状态"\_不\_其[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数支持的状态来对对象进行失败设置或查询请求。

<a href="" id="o"></a>**I/o**  
指示对对象的支持是可选的。 微型端口驱动程序可以支持对对象的查询或设置请求，或者通过返回 NDIS\_状态\_不\_其[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数支持的请求来使请求失败。

| 名称                                                                                                | Q   | S   | M   |
|-----------------------------------------------------------------------------------------------------|-----|-----|-----|
| [OID\_WDI\_中止\_任务](oid-wdi-abort-task.md)                                                     |     |     | R   |
| [OID\_WDI\_获取\_适配器\_功能](oid-wdi-get-adapter-capabilities.md)                        |     |     | R   |
| [OID\_WDI\_获取\_自动\_POWER\_保存](oid-wdi-get-auto-power-save.md)                                 |     |     | R   |
| [OID\_WDI\_获取\_BSS\_条目\_列表](oid-wdi-get-bss-entry-list.md)                                   |     |     | O   |
| [OID\_WDI\_获取\_下一\_操作\_帧\_对话框\_标记](oid-wdi-get-next-action-frame-dialog-token.md) |     |     | O   |
| [OID\_WDI\_获取\_PM\_协议\_卸载](oid-wdi-get-pm-protocol-offload.md)                         |     |     | O   |
| [OID\_WDI\_获取\_接收\_合并\_匹配\_计数](oid-wdi-get-receive-coalescing-match-count.md)  |     |     | O   |
| [OID\_WDI\_获取\_统计信息](oid-wdi-get-statistics.md)                                             |     |     | R   |
| [OID\_WDI\_IHV\_请求](oid-wdi-ihv-request.md)                                                   |     |     | O   |
| [OID\_WDI\_设置\_适配器\_配置](oid-wdi-set-adapter-configuration.md)                      |     |     | R   |
| [OID\_WDI\_集\_添加\_密码\_密钥](oid-wdi-set-add-cipher-keys.md)                                 |     |     | R   |
| [OID\_WDI\_集\_添加\_PM\_协议\_卸载](oid-wdi-set-add-pm-protocol-offload.md)                |     |     | O   |
| [OID\_WDI\_集\_添加\_WOL\_模式](oid-wdi-set-add-wol-pattern.md)                                 |     |     | O   |
| [OID\_WDI\_设置\_播发\_信息](oid-wdi-set-advertisement-information.md)              |     |     | O   |
| [OID\_WDI\_SET\_ASSOCIATION\_参数](oid-wdi-set-association-parameters.md)                    |     |     | R   |
| [OID\_WDI\_集\_清楚\_接收\_合并](oid-wdi-set-clear-receive-coalescing.md)               |     |     | O   |
| [OID\_WDI\_集\_连接\_质量](oid-wdi-set-connection-quality.md)                            |     |     | R   |
| [OID\_WDI\_集\_默认\_密钥\_ID](oid-wdi-set-default-key-id.md)                                   |     |     | R   |
| [OID\_WDI\_集\_DELETE\_密码\_密钥](oid-wdi-set-delete-cipher-keys.md)                           |     |     | R   |
| [OID\_WDI\_集\_封装\_卸载](oid-wdi-set-encapsulation-offload.md)                      |     |     | O   |
| [OID\_WDI\_集\_刷新\_BSS\_条目](oid-wdi-set-flush-bss-entry.md)                                 |     |     | O   |
| [OID\_WDI\_设置\_多播\_列表](oid-wdi-set-multicast-list.md)                                    |     |     | R   |
| [OID\_WDI\_设置\_网络\_列表\_卸载](oid-wdi-set-network-list-offload.md)                       |     |     | O   |
| [OID\_WDI\_集\_P2P\_侦听\_状态](oid-wdi-set-p2p-listen-state.md)                               |     |     | O   |
| [OID\_WDI\_集\_P2P\_开始\_后台\_发现](oid-wdi-set-p2p-start-background-discovery.md)  |     |     | O   |
| [OID\_WDI\_集\_P2P\_停止\_后台\_发现](oid-wdi-set-p2p-stop-background-discovery.md)    |     |     | O   |
| [已启用 OID\_WDI\_集\_P2P\_WPS\_](oid-wdi-set-p2p-wps-enabled.md)                                 |     |     | O   |
| [OID\_WDI\_设置\_电源\_状态](oid-wdi-set-power-state.md)                                          |     |     | R   |
| [OID\_WDI\_设置\_隐私\_免除\_列表](oid-wdi-set-privacy-exemption-list.md)                   |     |     | R   |
| [OID\_WDI\_集\_接收\_合并](oid-wdi-set-receive-coalescing.md)                            |     |     | O   |
| [OID\_WDI\_集\_接收\_数据包\_筛选器](oid-wdi-set-receive-packet-filter.md)                     |     |     | R   |
| [OID\_WDI\_集\_删除\_PM\_协议\_卸载](oid-wdi-set-remove-pm-protocol-offload.md)          |     |     | O   |
| [OID\_WDI\_集\_删除\_WOL\_模式](oid-wdi-set-remove-wol-pattern.md)                           |     |     | O   |
| [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)                                      |     |     | O   |
| [OID\_WDI\_集\_TCP\_卸载\_参数](oid-wdi-set-tcp-offload-parameters.md)                   |     |     | O   |
| [OID\_WDI\_TCP\_RSC\_统计信息](oid-wdi-tcp-rsc-statistics.md)                                    |     |     | O   |

 

 

 




