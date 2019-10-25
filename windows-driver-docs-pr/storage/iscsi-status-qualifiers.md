---
title: ISCSI\_状态\_限定符
description: ISCSI\_状态\_限定符
ms.assetid: d39ed448-5608-4f19-b49c-bbd6727e9491
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b9e05c4c2ff19408b2eb12060fcb0d69621312a6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823682"
---
# <a name="iscsi_status_qualifiers"></a>ISCSI\_状态\_限定符


## <span id="ddk_iscsi_status_qualifiers_kr"></span><span id="DDK_ISCSI_STATUS_QUALIFIERS_KR"></span>


ISCSI\_状态\_限定符 WMI 属性限定符对应于管理 iSCSI HBA 发起程序的微型端口驱动程序报告的状态值。 这些值通过将严重性代码与设备代码和在*Ntstatus*中描述的设施状态代码结合起来来构造。

下表描述了\_限定符值的 ISCSI\_状态。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状态值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>辉煌.</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_NON_SPECIFIC_ERROR (0xEFFF0001)</p></td>
<td align="left"><p>不特定的错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_LOGIN_FAILED (0xEFFF0002)</p></td>
<td align="left"><p>登录失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_CONNECTION_FAILED (0xEFFF0003)</p></td>
<td align="left"><p>连接失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INITIATOR_NODE_ALREADY_EXISTS (0xEFFF0004)</p></td>
<td align="left"><p>发起方节点已存在。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INITIATOR_NODE_NOT_FOUND (0xEFFF0005)</p></td>
<td align="left"><p>发起方节点不存在。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_MOVED_TEMPORARILY (0xEFFF0006)</p></td>
<td align="left"><p>目标已暂时移动。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_TARGET_MOVED_PERMANENTLY (0xEFFF0007)</p></td>
<td align="left"><p>目标已永久移动。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INITIATOR_ERROR (0xEFFF0008)</p></td>
<td align="left"><p>发起方错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_AUTHENTICATION_FAILURE (0xEFFF0009)</p></td>
<td align="left"><p>身份验证失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_AUTHORIZATION_FAILURE (0xEFFF000A)</p></td>
<td align="left"><p>授权失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_NOT_FOUND (0xEFFF000B)</p></td>
<td align="left"><p>找不到目标。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_REMOVED (0xEFFF000C)</p></td>
<td align="left"><p>删除目标。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_UNSUPPORTED_VERSION (0xEFFF000D)</p></td>
<td align="left"><p>版本不受支持。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TOO_MANY_CONNECTIONS (0xEFFF000E)</p></td>
<td align="left"><p>连接太多。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_MISSING_PARAMETER (0xEFFF000F)</p></td>
<td align="left"><p>缺少参数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_CANT_INCLUDE_IN_SESSION (0xEFFF0010)</p></td>
<td align="left"><p>无法在会话中包含连接。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_SESSION_TYPE_NOT_SUPPORTED (0xEFFF0011)</p></td>
<td align="left"><p>会话类型不受支持。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_ERROR (0xEFFF0012)</p></td>
<td align="left"><p>目标错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_SERVICE_UNAVAILABLE (0xEFFF0013)</p></td>
<td align="left"><p>服务不可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_OUT_OF_RESOURCES (0xEFFF0014)</p></td>
<td align="left"><p>资源不足。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_CONNECTION_ALREADY_EXISTS (0xEFFF0015)</p></td>
<td align="left"><p>发起程序节点上已存在连接。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_SESSION_ALREADY_EXISTS (0xEFFF0016)</p></td>
<td align="left"><p>该会话已经存在。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INITIATOR_INSTANCE_NOT_FOUND (0xEFFF0017)</p></td>
<td align="left"><p>发起方实例不存在。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_ALREADY_EXISTS (0xEFFF0018)</p></td>
<td align="left"><p>目标已存在。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_DRIVER_BUG (0xEFFF0019)</p></td>
<td align="left"><p>ISCSI 驱动程序实现未正确完成操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INVALID_TEXT_KEY (0xEFFF001A)</p></td>
<td align="left"><p>遇到无效的密钥文本。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INVALID_SENDTARGETS_TEXT (0xEFFF001B)</p></td>
<td align="left"><p>遇到无效的 endTargets 响应文本。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INVALID_SESSION_ID (0xEFFF001C)</p></td>
<td align="left"><p>会话标识符（ID）无效。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_SCSI_REQUEST_FAILED (0xEFFF001D)</p></td>
<td align="left"><p>SCSI 请求失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TOO_MANY_SESSIONS (0xEFFF001E)</p></td>
<td align="left"><p>超出了此发起程序的最大会话数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_SESSION_BUSY (0xEFFF001F)</p></td>
<td align="left"><p>会话正忙，因为请求已在进行中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_MAPPING_UNAVAILABLE (0xEFFF0020)</p></td>
<td align="left"><p>目标映射不可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_ADDRESS_TYPE_NOT_SUPPORTED (0xEFFF0021)</p></td>
<td align="left"><p>目标地址类型不受支持。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_LOGON_FAILED (0xEFFF0022)</p></td>
<td align="left"><p>登录失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_SEND_FAILED (0xEFFF0023)</p></td>
<td align="left"><p>TCP 发送失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TRANSPORT_ERROR (0xEFFF0024)</p></td>
<td align="left"><p>TCP 传输错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_VERSION_MISMATCH (0xEFFF0025)</p></td>
<td align="left"><p>iSCSI 版本不匹配。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_MAPPING_OUT_OF_RANGE (0xEFFF0026)</p></td>
<td align="left"><p>传递的目标映射地址超出了适配器配置的范围。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_TARGET_PRESHAREDKEY_UNAVAILABLE (0xEFFF0027)</p></td>
<td align="left"><p>目标或 internet 密钥交换（IKE）标识有效负载的预共享密钥不可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_AUTHINFO_UNAVAILABLE (0xEFFF0028)</p></td>
<td align="left"><p>目标的身份验证信息不可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_TARGET_NOT_FOUND (0xEFFF0029)</p></td>
<td align="left"><p>找不到目标名称或将其标记为隐藏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_LOGIN_USER_INFO_BAD (0xEFFF002A)</p></td>
<td align="left"><p>在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_logintotarget_in" data-raw-source="[&lt;strong&gt;LoginToTarget_IN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_logintotarget_in)"><strong>LoginToTarget_IN</strong></a>结构中指定的一个或多个参数无效。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_TARGET_MAPPING_EXISTS (0xEFFF002B)</p></td>
<td align="left"><p>给定的目标映射已存在。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_HBA_SECURITY_CACHE_FULL (0xEFFF002C)</p></td>
<td align="left"><p>HBA 安全信息缓存已满。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INVALID_PORT_NUMBER (0xEFFF002D)</p></td>
<td align="left"><p>传递的端口号对发起方无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_OPERATION_NOT_ALL_SUCCESS (0xEFFF002E)</p></td>
<td align="left"><p>所有发起程序的操作均失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_HBA_SECURITY_CACHE_NOT_SUPPORTED (0xEFFF002F)</p></td>
<td align="left"><p>适配器没有安全信息缓存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_IKE_ID_PAYLOAD_TYPE_NOT_SUPPORTED (0xEFFF0030)</p></td>
<td align="left"><p>指定的 IKE ID 负载类型不受支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_IKE_ID_PAYLOAD_INCORRECT_SIZE (0xEFFF0031)</p></td>
<td align="left"><p>指定的 IKE ID 负载大小不正确。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_PORTAL_ALREADY_EXISTS (0xEFFF0032)</p></td>
<td align="left"><p>目标门户结构已存在。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_TARGET_ADDRESS_ALREADY_EXISTS (0xEFFF0033)</p></td>
<td align="left"><p>目标地址结构已存在。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_NO_AUTH_INFO_AVAILABLE (0xEFFF0034)</p></td>
<td align="left"><p>没有可用的 IKE 身份验证信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_NO_TUNNEL_OUTER_MODE_ADDRESS (0xEFFF0035)</p></td>
<td align="left"><p>未指定隧道模式外部地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_CACHE_CORRUPTED (0xEFFF0036)</p></td>
<td align="left"><p>身份验证或隧道地址缓存已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_REQUEST_NOT_SUPPORTED (0xEFFF0037)</p></td>
<td align="left"><p>不支持该请求或操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_TARGET_OUT_OF_RESORCES (0xEFFF0038)</p></td>
<td align="left"><p>目标没有足够的资源来处理给定的请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_SERVICE_DID_NOT_RESPOND (0xEFFF0039)</p></td>
<td align="left"><p>发起方服务没有响应驱动程序发送的请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_ISNS_SERVER_NOT_FOUND (0xEFFF003A)</p></td>
<td align="left"><p>ISNS 服务器找不到或不可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_OPERATION_REQUIRES_REBOOT (0xAFFF003B)</p></td>
<td align="left"><p>操作成功，但需要重新加载驱动程序或重新启动才能生效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_NO_PORTAL_SPECIFIED (0xEFFF003C)</p></td>
<td align="left"><p>没有可用于完成登录的目标门户。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_CANT_REMOVE_LAST_CONNECTION (0xEFFF003D)</p></td>
<td align="left"><p>无法删除会话的上一个连接。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_SERVICE_NOT_RUNNING (0xEFFF003E)</p></td>
<td align="left"><p>ISCSI 发起程序服务尚未启动。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_TARGET_ALREADY_LOGGED_IN (0xEFFF003F)</p></td>
<td align="left"><p>目标已经通过 iSCSI 会话登录。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_DEVICE_BUSY_ON_SESSION (0xEFFF0040)</p></td>
<td align="left"><p>无法注销会话，因为当前正在使用该会话上的一个设备。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_COULD_NOT_SAVE_PERSISTENT_LOGIN_DATA (0xEFFF0041)</p></td>
<td align="left"><p>未能保存持久的登录信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_COULD_NOT_REMOVE_PERSISTENT_LOGIN_DATA (0xEFFF0042)</p></td>
<td align="left"><p>未能删除持久的登录信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_PORTAL_NOT_FOUND (0xEFFF0043)</p></td>
<td align="left"><p>找不到指定的发起程序名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INITIATOR_NOT_FOUND (0xEFFF0044)</p></td>
<td align="left"><p>找不到指定的门户。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_DISCOVERY_MECHANISM_NOT_FOUND (0xEFFF0045)</p></td>
<td align="left"><p>找不到指定的发现机制。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_IPSEC_NOT_SUPPORTED_ON_OS (0xEFFF0046)</p></td>
<td align="left"><p>对于此版本的操作系统，iSCSI 不支持 IPsec 协议。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_PERSISTENT_LOGIN_TIMEOUT (0xEFFF0047)</p></td>
<td align="left"><p>发现服务等待所有永久登录完成时超时。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_SHORT_CHAP_SECRET (0xEFFF0048)</p></td>
<td align="left"><p>指定的 CHAP 机密小于96位，无法用于通过非 IPsec 连接进行的身份验证协商。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_EVALUATION_PEROID_EXPIRED (0xEFFF0049)</p></td>
<td align="left"><p>ISCSI 发现服务的评估期已过。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INVALID_CHAP_SECRET (0xEFFF004A)</p></td>
<td align="left"><p>CHAP 机密不符合 Internet 工程任务组（IETF）网络工作组发布的质询握手身份验证协议（CHAP）规范。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INVALID_TARGET_CHAP_SECRET (0xEFFF004B)</p></td>
<td align="left"><p>目标 CHAP 机密无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INVALID_INITIATOR_CHAP_SECRET (0xEFFF004C)</p></td>
<td align="left"><p>发起程序 CHAP 密码无效。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INVALID_CHAP_USER_NAME (0xEFFF004D)</p></td>
<td align="left"><p>CHAP 用户名无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INVALID_LOGON_AUTH_TYPE (0xEFFF004E)</p></td>
<td align="left"><p>登录身份验证类型无效。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INVALID_TARGET_MAPPING (0xEFFF004F)</p></td>
<td align="left"><p>目标映射信息无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INVALID_TARGET_ID (0xEFFF0050)</p></td>
<td align="left"><p>目标映射中的64位 iSCSI 目标标识符无效。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INVALID_ISCSI_NAME (0xEFFF0051)</p></td>
<td align="left"><p>指定的 iSCSI 名称包含无效字符或太长。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INCOMPATIBLE_ISNS_VERSION (0xEFFF0052)</p></td>
<td align="left"><p>ISNS 服务器返回的 iSNS 版本号与此版本的 iSNS 客户端不兼容。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_FAILED_TO_CONFIGURE_IPSEC (0xEFFF0053)</p></td>
<td align="left"><p>发起程序无法为给定的连接配置 IPSec。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_BUFFER_TOO_SMALL (0xEFFF0054)</p></td>
<td align="left"><p>给定用于处理的缓冲区太小。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INVALID_LOAD_BALANCE_POLICY (0xEFFF0055)</p></td>
<td align="left"><p>给定的负载均衡策略无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_INVALID_PARAMETER (0xEFFF0056)</p></td>
<td align="left"><p>指定的一个或多个参数无效。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_DUPLICATE_PATH_SPECIFIED (0xEFFF0057)</p></td>
<td align="left"><p>尝试在冗余路径中设置负载均衡策略时指定了重复的路径 Id。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_PATH_COUNT_MISMATCH (0xEFFF0058)</p></td>
<td align="left"><p>设置负载平衡策略时指定的路径数与目标中的可用路径数不匹配。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INVALID_PATH_ID (0xEFFF0059)</p></td>
<td align="left"><p>在设置负载平衡策略时指定的路径 ID 无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_MULTIPLE_PRIMARY_PATHS_SPECIFIED (0xEFFF005A)</p></td>
<td align="left"><p>当只应有一个主路径时，指定多个主路径。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_NO_PRIMARY_PATH_SPECIFIED (0xEFFF005B)</p></td>
<td align="left"><p>至少应有一个主路径时未指定该路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_DEVICE_ALREADY_PERSISTENTLY_BOUND (0xEFFF005C)</p></td>
<td align="left"><p>设备已是永久绑定设备。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_DEVICE_NOT_FOUND (0xEFFF005D)</p></td>
<td align="left"><p>找不到设备。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_DEVICE_NOT_ISCSI_OR_PERSISTENT (0xEFFF005E)</p></td>
<td align="left"><p>指定的设备不是源自 iSCSI 磁盘或永久 iSCSI 登录名。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_DNS_NAME_UNRESOLVED (0xEFFF005F)</p></td>
<td align="left"><p>指定的 DNS 名称未解析。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_NO_CONNECTION_AVAILABLE (0xEFFF0060)</p></td>
<td align="left"><p>ISCSI 会话中没有可用于处理请求的连接。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_LB_POLICY_NOT_SUPPORTED (0xEFFF0061)</p></td>
<td align="left"><p>不支持给定的负载平衡策略。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_REMOVE_CONNECTION_IN_PROGRESS (0xEFFF0062)</p></td>
<td align="left"><p>此会话的删除连接请求已在进行中。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_INVALID_CONNECTION_ID (0xEFFF0063)</p></td>
<td align="left"><p>在会话中找不到给定的连接。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_CANNOT_REMOVE_LEADING_CONNECTION (0xEFFF0064)</p></td>
<td align="left"><p>无法删除会话中的主连接。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISDSC_RESTRICTED_BY_GROUP_POLICY (0xEFFF0065)</p></td>
<td align="left"><p>操作无法执行，因为它不符合分配给此计算机的组策略。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISDSC_ISNS_FIREWALL_BLOCKED (0xEFFF0066)</p></td>
<td align="left"><p>无法执行该操作，因为尚未启用 Internet 存储名称服务器（iSNS）防火墙例外。</p></td>
</tr>
</tbody>
</table>

 

 

 





