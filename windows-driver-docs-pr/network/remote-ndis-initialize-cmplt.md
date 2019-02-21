---
title: REMOTE_NDIS_INITIALIZE_CMPLT
ms.assetid: e1e057bf-aa92-4b90-b993-a82cc260ff7f
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 599c811c124304595867c899fd750bdaa15dd45c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541017"
---
# <a name="remotendisinitializecmplt"></a>远程\_NDIS\_初始化\_CMPLT


在远程\_NDIS\_初始化\_CMPLT 消息由远程 NDIS 设备发送到主机上的响应[**远程\_NDIS\_初始化\_MSG** ](remote-ndis-initialize-msg.md)消息。 在远程\_NDIS\_初始化\_CMPLT 消息，设备将报告其介质类型、 远程 NDIS 版本数字和其类型 (无连接或面向连接的和 / 或)。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>偏移量</th>
<th>尺寸</th>
<th>字段</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>4</p></td>
<td><p>MessageType</p></td>
<td><p>指定发送消息的类型。 将设置为数 0x80000002。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>MessageLength</p></td>
<td><p>以字节为单位指定的消息的开始，这封邮件的总长度。</p></td>
</tr>
<tr class="odd">
<td><p>8</p></td>
<td><p>4</p></td>
<td><p>RequestId</p></td>
<td><p>指定远程 NDIS 消息 ID 值。 此值用于匹配的设备响应主机发送的消息。</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>状态</p></td>
<td><p>指定 RNDIS_STATUS_SUCCESS 如果设备成功，则初始化否则，它指定错误代码指示失败。</p></td>
</tr>
<tr class="odd">
<td><p>16</p></td>
<td><p>4</p></td>
<td><p>主要版本</p></td>
<td><p>指定设备支持的最高远程 NDIS 主要协议版本。</p></td>
</tr>
<tr class="even">
<td><p>20</p></td>
<td><p>4</p></td>
<td><p>MinorVersion</p></td>
<td><p>指定设备支持的最高远程 NDIS 次要协议版本。</p></td>
</tr>
<tr class="odd">
<td><p>24</p></td>
<td><p>4</p></td>
<td><p>DeviceFlags</p></td>
<td><p>指定为无连接或面向连接的微型端口驱动程序类型。 此值可以是以下值之一：</p>
<p>RNDIS_DF_CONNECTIONLESS 0x00000001</p>
<p>RNDIS_DF_CONNECTION_ORIENTED 0x00000002</p></td>
</tr>
<tr class="even">
<td><p>28</p></td>
<td><p>4</p></td>
<td><p>中等</p></td>
<td><p>指定设备支持的介质。 设置为 RNDIS_MEDIUM_802_3 (0x00000000)</p></td>
</tr>
<tr class="odd">
<td><p>32</p></td>
<td><p>4</p></td>
<td><p>MaxPacketsPerMessage</p></td>
<td><p>在单个传输到其指定的最大远程 NDIS 设备可以处理的数据消息数。 此值应至少一个。</p></td>
</tr>
<tr class="even">
<td><p>36</p></td>
<td><p>4</p></td>
<td><p>MaxTransferSize</p></td>
<td><p>以字节为单位的设备需要从主机接收的任何单个总线数据传输指定的最大大小。</p></td>
</tr>
<tr class="odd">
<td><p>40</p></td>
<td><p>4</p></td>
<td><p>PacketAlignmentFactor</p></td>
<td><p>指定设备所预期的是 multimessage 传输到它的一部分的每个远程 NDIS 消息的字节对齐方式。 指定此值中的 2 的幂。 例如，此值设置为三个指示 8 字节对齐方式。 此值，其最大设置为 7，这指定 128 个字节对齐方式。</p></td>
</tr>
<tr class="even">
<td><p>44</p></td>
<td><p>4</p></td>
<td><p>AFListOffset</p></td>
<td><p>保留的面向连接的设备。 将值设置为零。</p></td>
</tr>
<tr class="odd">
<td><p>48</p></td>
<td><p>4</p></td>
<td><p>AFListSize</p></td>
<td><p>保留的面向连接的设备。 将值设置为零。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

*状态*字段应设置为 RNDIS\_状态\_其设置为一个错误代码指示失败，如果成功; 否则为，该设备初始化成功。 设备应返回的最高的远程 NDIS 协议版本，它可以支持，在*MajorVersion*并*MinorVersion*-组合的版本号应该是小于或等于版本数中指定的主机[**远程\_NDIS\_初始化\_MSG** ](remote-ndis-initialize-msg.md)消息。

*AFListSize*并*AFListOffset*字段是仅适用于包含呼叫管理器的面向连接的设备。 无连接的设备应将这些字段设置为零。

此消息中，如下所示远程 NDIS 设备：

-   最大远程 NDIS 协议版本数量的设备可以支持。 组合的版本号应该是小于或等于该主机中指定的版本号[**远程\_NDIS\_初始化\_MSG** ](remote-ndis-initialize-msg.md)消息。 这允许设备回退到兼容性模式下，当主机实现远程 NDIS 协议版本低于支持的设备。

-   以字节为单位的设备需要从主机接收的单个数据传输的最大大小。 设备可以指定它需要为属于 multimessage 传输到它的每个远程 NDIS 消息的字节对齐方式。 根据为 2 的幂指定此对齐值。 例如，此值设置为 3 以指示 8 字节对齐方式。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 Microsoft Windows XP 和更高版本的 Windows 操作系统中可用。 也可在 Windows 2000 中作为可再发行组件的二进制文件。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Rndis.h （包括 Rndis.h）</td>
</tr>
</tbody>
</table>

 

 




