---
title: 定义
description: 定义
ms.assetid: 904b7dd3-472d-4286-81c1-2af1109e2139
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07c043d0f4f095dccf25c714c34f17e553cc5a70
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392750"
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
<td align="left"><p>标准协议进行安全身份验证和安全主机和直接连接暂时性存储设备 (TSD)，如 USB 闪存驱动器、 便携式硬盘驱动器或移动电话之间的信任关系的创建。"</p>
<p>有关详细信息，请参阅<a href="https://standards.ieee.org/standard/1667-2018.html">IEEE 1667 2018-IEEE 标准发现、 身份验证和主机附件的存储设备中的授权</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1667 身份验证接收器</p></td>
<td align="left"><p>1667 接收器，其函数提供了主机到设备、 设备到主机，或两者的任一身份验证。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1667 标准身份验证接收器</p></td>
<td align="left"><p>标准证书或密码身份验证接收器 Microsoft 是传送驱动程序的基 1667年规范中定义。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1667 USB 闪存设备 (UFD)</p></td>
<td align="left"><p>USB 闪存设备实现的 1667年命令根据 IEEE 1667 规范集。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>第三方身份验证接收器</p></td>
<td align="left"><p>未在基本集的 1667年实现身份验证函数的指定标准身份验证接收器中定义的接收器。</p></td>
</tr>
<tr class="even">
<td align="left"><p>第三方接收器</p></td>
<td align="left"><p>接收器 1667年集中不包含指定标准接收器。 该函数是专有的 IEEE 1667 基本标准中未记录。 有时称为"未知"的接收器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可寻址命令目标 (ACT)</p></td>
<td align="left"><p>接受 1667年命令并选择性地提供访问用户数据 （请参阅逻辑单元） 的访问的独立单元。 根据 1667年规范，行为不是需要提供用户数据访问函数。 1667 设备可能会实现一个或多个作用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>身份验证</p></td>
<td align="left"><p>（因为它与 IEEE 1667） 验证身份的真实性的 act 声明通过以下任一方法在主机或设备。 密码身份验证的情况下，通过设备的用户建立一个密钥密码是能够实现此目的的凭据。 证书身份验证的情况下，拥有私有密钥必须通过已成功解密随机字节流的配对的公钥加密的证明。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>授权</p></td>
<td align="left"><p>指示配备控制资源访问授权后设备或主机标识已经过身份验证。 主机设备身份验证控制对关联的 ACT 的用户数据部分的授权的访问，而设备主机身份验证成功授权设备和主机之间的连接的数据通道。</p></td>
</tr>
<tr class="even">
<td align="left"><p>证书接收器 （Cert 接收器）</p></td>
<td align="left"><p>使用证书和关联的公共 / 专用密钥对的基础，进行身份验证的身份验证接收器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>旧版大容量存储 （或旧版 UFD）</p></td>
<td align="left"><p>不实现 1667年命令 USB 大容量存储 （或 USB 闪存设备） 设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p>逻辑单元 (LUN)</p></td>
<td align="left"><p>对包含在作为单个磁盘在主机系统上的设备上的用户数据的访问的独立单元。 LUN 是当前处于已授权状态数据的承载 1667 ACT 的同义词。</p>
<p>多 LUN 支持某些 Ufd。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>密码接收器 （PW 接收器）</p></td>
<td align="left"><p>身份验证接收器使用通行短语匹配，用作身份验证的基础。</p></td>
</tr>
<tr class="even">
<td align="left"><p>可移动媒体位 (RMB)</p></td>
<td align="left"><p>有点 SCSI 查询命令的设备响应中包含 (0x12)，该值指示媒体是否可移动 (RMB = 1) 或固定 (RMB = 0)。 无法与用来指示 PDO 是否表示热插拔设备 DEVICE_CAPABILITIES 可移动字段相混淆，RMB 指媒体而不是设备本身的属性。 媒体的 RMB = 1 的处理方式是由系统超过显示带有 RMB 的媒体 = 0。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>接收器</p></td>
<td align="left"><p>响应 1667年命令的独立功能单元。 为每个 ACT 可附加一个或多个接收器。 1667 接收器命令可能会发送到特定法案索引和接收器索引。</p></td>
</tr>
</tbody>
</table>

 

 

 




