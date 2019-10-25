---
title: WDI 任务 OID
description: 本部分包含 WDI 任务 Oid。
ms.assetid: CAA92CA5-5CD6-4705-AA4C-54C1AA83ACA3
ms.date: 07/18/2017
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 696b2b320977be6341f37afc3354751ee6c6a5b5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842911"
---
# <a name="wdi-task-oids"></a>WDI 任务 OID


本部分包含 WDI 任务 Oid。

Wi-fi 驱动程序接口（WDI）对象标识符（Oid）仅适用于实现 WDI 的微型端口驱动程序。

下表指定 WDI OID query （Q）、set （S）和 NDIS 6.0 方法（M）请求是否必需或可选来实现：

<a href="" id="r"></a>**迅驰**  
指示对对象的支持是必需的。 微型端口驱动程序不能通过返回状态代码 "NDIS\_状态"\_不\_其[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数支持的状态来对对象进行失败设置或查询请求。

<a href="" id="o"></a>**I/o**  
指示对对象的支持是可选的。 微型端口驱动程序可以支持对对象的查询或设置请求，或者通过返回 NDIS\_状态\_不\_其[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数支持的请求来使请求失败。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>名称</th>
<th>Q</th>
<th>S</th>
<th>M</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="oid-wdi-task-change-operation-mode.md" data-raw-source="[OID_WDI_TASK_CHANGE_OPERATION_MODE](oid-wdi-task-change-operation-mode.md)">OID_WDI_TASK_CHANGE_OPERATION_MODE</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>R</p></td>
</tr>
<tr class="even">
<td><p><a href="oid-wdi-task-close.md" data-raw-source="[OID_WDI_TASK_CLOSE](oid-wdi-task-close.md)">OID_WDI_TASK_CLOSE</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>R</p></td>
</tr>
<tr class="odd">
<td><p><a href="oid-wdi-task-connect.md" data-raw-source="[OID_WDI_TASK_CONNECT](oid-wdi-task-connect.md)">OID_WDI_TASK_CONNECT</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>R</p></td>
</tr>
<tr class="even">
<td><p><a href="oid-wdi-task-create-port.md" data-raw-source="[OID_WDI_TASK_CREATE_PORT](oid-wdi-task-create-port.md)">OID_WDI_TASK_CREATE_PORT</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>R</p></td>
</tr>
<tr class="odd">
<td><p><a href="oid-wdi-task-delete-port.md" data-raw-source="[OID_WDI_TASK_DELETE_PORT](oid-wdi-task-delete-port.md)">OID_WDI_TASK_DELETE_PORT</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>R</p></td>
</tr>
<tr class="even">
<td><p><a href="oid-wdi-task-disconnect.md" data-raw-source="[OID_WDI_TASK_DISCONNECT](oid-wdi-task-disconnect.md)">OID_WDI_TASK_DISCONNECT</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>R</p></td>
</tr>
<tr class="odd">
<td><p><a href="oid-wdi-task-dot11-reset.md" data-raw-source="[OID_WDI_TASK_DOT11_RESET](oid-wdi-task-dot11-reset.md)">OID_WDI_TASK_DOT11_RESET</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>R</p></td>
</tr>
<tr class="even">
<td><p><a href="oid-wdi-task-ihv.md" data-raw-source="[OID_WDI_TASK_IHV](oid-wdi-task-ihv.md)">OID_WDI_TASK_IHV</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>O</p></td>
</tr>
<tr class="odd">
<td><p><a href="oid-wdi-task-open.md" data-raw-source="[OID_WDI_TASK_OPEN](oid-wdi-task-open.md)">OID_WDI_TASK_OPEN</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>O</p></td>
</tr>
<tr class="even">
<td><p><a href="oid-wdi-task-p2p-discover.md" data-raw-source="[OID_WDI_TASK_P2P_DISCOVER](oid-wdi-task-p2p-discover.md)">OID_WDI_TASK_P2P_DISCOVER</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>O</p></td>
</tr>
<tr class="odd">
<td><p><a href="oid-wdi-task-p2p-send-request-action-frame.md" data-raw-source="[OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME](oid-wdi-task-p2p-send-request-action-frame.md)">OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>O</p></td>
</tr>
<tr class="even">
<td><p><a href="oid-wdi-task-p2p-send-response-action-frame.md" data-raw-source="[OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME](oid-wdi-task-p2p-send-response-action-frame.md)">OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>O</p></td>
</tr>
<tr class="odd">
<td><p><a href="oid-wdi-task-request-ftm.md" data-raw-source="[OID_WDI_TASK_REQUEST_FTM](oid-wdi-task-request-ftm.md)">OID_WDI_TASK_REQUEST_FTM</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>O</p></td>
</tr>
<tr class="even">
<td><p><a href="oid-wdi-task-roam.md" data-raw-source="[OID_WDI_TASK_ROAM](oid-wdi-task-roam.md)">OID_WDI_TASK_ROAM</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>R</p></td>
</tr>
<tr class="odd">
<td><p><a href="oid-wdi-task-scan.md" data-raw-source="[OID_WDI_TASK_SCAN](oid-wdi-task-scan.md)">OID_WDI_TASK_SCAN</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>R</p></td>
</tr>
<tr class="even">
<td><p><a href="oid-wdi-task-send-ap-association-response.md" data-raw-source="[OID_WDI_TASK_SEND_AP_ASSOCIATION_RESPONSE](oid-wdi-task-send-ap-association-response.md)">OID_WDI_TASK_SEND_AP_ASSOCIATION_RESPONSE</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>O</p></td>
</tr>
<tr class="odd">
<td><p><a href="oid-wdi-task-send-request-action-frame.md" data-raw-source="[OID_WDI_TASK_SEND_REQUEST_ACTION_FRAME](oid-wdi-task-send-request-action-frame.md)">OID_WDI_TASK_SEND_REQUEST_ACTION_FRAME</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>O</p></td>
</tr>
<tr class="even">
<td><p><a href="oid-wdi-task-send-response-action-frame.md" data-raw-source="[OID_WDI_TASK_SEND_RESPONSE_ACTION_FRAME](oid-wdi-task-send-response-action-frame.md)">OID_WDI_TASK_SEND_RESPONSE_ACTION_FRAME</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>O</p></td>
</tr>
<tr class="odd">
<td><p><a href="oid-wdi-task-set-radio-state.md" data-raw-source="[OID_WDI_TASK_SET_RADIO_STATE](oid-wdi-task-set-radio-state.md)">OID_WDI_TASK_SET_RADIO_STATE</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>R</p></td>
</tr>
<tr class="even">
<td><p><a href="oid-wdi-task-start-ap.md" data-raw-source="[OID_WDI_TASK_START_AP](oid-wdi-task-start-ap.md)">OID_WDI_TASK_START_AP</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>O</p></td>
</tr>
<tr class="odd">
<td><p><a href="oid-wdi-task-stop-ap.md" data-raw-source="[OID_WDI_TASK_STOP_AP](oid-wdi-task-stop-ap.md)">OID_WDI_TASK_STOP_AP</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>O</p></td>
</tr>
</tbody>
</table>

 

 

 




