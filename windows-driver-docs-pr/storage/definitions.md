---
title: 定义
description: 定义
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e58fe369250f27f655466630d006623d28e3342
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804705"
---
# <a name="definitions"></a>定义


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IEEE 1667</p></td>
<td align="left"><p>一种标准协议，用于安全的身份验证，并在安全主机和直接附加的临时存储设备之间创建信任 (TSD) ，如 USB 闪存驱动器、便携式硬盘或移动电话）。</p>
<p>有关详细信息，请参阅 <a href="https://standards.ieee.org/standard/1667-2018.html">ieee 1667-2018-Ieee 标准，用于发现、身份验证和存储设备的主机附件中的授权</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1667身份验证接收器</p></td>
<td align="left"><p>一种1667接收器，其函数提供主机到设备、设备到主机或两者的身份验证。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1667标准身份验证接收器</p></td>
<td align="left"><p>在基本1667规范中定义的标准证书或密码身份验证接收器，适用于 Microsoft 的发运驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1667 (UFD) USB 闪存设备</p></td>
<td align="left"><p>USB 闪存设备根据 IEEE 1667 规范实现1667命令集。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>第三方身份验证接收器</p></td>
<td align="left"><p>未在1667指定的基本字符集中定义思洛组。</p></td>
</tr>
<tr class="even">
<td align="left"><p>第三方接收器</p></td>
<td align="left"><p>未包含在由1667指定的标准接收器集中的接收器。 此函数是专有的，不在 IEEE 1667 基本标准中记录。 有时称为 "未知" 接收器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可寻址命令目标 (ACT) </p></td>
<td align="left"><p>独立的访问单元，可接受1667命令和（可选）提供对用户数据的访问权限 (参阅逻辑单元) 。 根据1667规范，无需执行 ACT 即可提供用户数据访问函数。 1667设备可以实现一个或多个作用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>身份验证</p></td>
<td align="left"><p>与 IEEE 1667 相关的 () 验证主机或设备所声称的标识的精确性的行为。 在密码身份验证情况下，由设备用户建立的密钥密码是用于实现此目的的凭据。 在证书身份验证情况下，必须通过成功解密使用成对公钥加密的随机字节流来验证私钥的所有权。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>授权</p></td>
<td align="left"><p>指示在对设备或主机标识进行身份验证后，授权对受管辖资源的 concomitant 访问。 主机到设备身份验证控制对相关操作的用户数据部分的授权访问，而成功的设备到主机身份验证将在设备和主机之间授权已连接的数据通道。</p></td>
</tr>
<tr class="even">
<td align="left"><p>证书接收器 (证书接收器) </p></td>
<td align="left"><p>身份验证接收器，使用证书以及关联的公钥-私钥对作为身份验证的基础。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>旧大容量存储 (或旧 UFD) </p></td>
<td align="left"><p>USB 大容量存储 (或 USB 闪存设备) 未实现1667命令集。</p></td>
</tr>
<tr class="even">
<td align="left"><p>逻辑单元 (LUN) </p></td>
<td align="left"><p>独立于设备的访问单元，该设备上包含的用户数据作为主机系统上的单个磁盘公开。 LUN 与当前处于授权状态的数据轴承1667操作同义。</p>
<p>有些 Ufd 是支持多 LUN 的。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>密码接收器 (PW 接收器) </p></td>
<td align="left"><p>身份验证接收器，使用传递短语匹配作为身份验证的基础。</p></td>
</tr>
<tr class="even">
<td align="left"><p>可移动媒体位 (RMB) </p></td>
<td align="left"><p>设备对 SCSI 查询命令的响应中包含的位 (0x12) ，指示媒体是可移动 (RMB = 1) 还是固定 (RMB = 0) 。 不要与用于指示 PDO 是否表示热插拔设备的 DEVICE_CAPABILITIES 的可移动字段混淆，RMB 是指媒体的属性而不是设备本身。 系统以不同于显示带有 RMB = 0 的媒体的方式处理 RMB = 1 的媒体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>洛</p></td>
<td align="left"><p>响应1667命令的独立功能单元。 对于每个 ACT，都可以附加一个或多个接收器。 1667接收器命令可能会寻址到特定的 ACT 索引和接收器索引。</p></td>
</tr>
</tbody>
</table>

 

 

 




