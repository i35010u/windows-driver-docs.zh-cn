---
description: 远程 NDIS 初始化 CMPLT
title: REMOTE_NDIS_INITIALIZE_CMPLT
ms.assetid: e1e057bf-aa92-4b90-b993-a82cc260ff7f
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96113a86fa97439281f521be465f0995f6ae2649
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968776"
---
# <a name="remote_ndis_initialize_cmplt"></a>远程 \_ NDIS \_ 初始化 \_ CMPLT


远程 ndis \_ \_ initialize \_ CMPLT 消息由远程 ndis 设备发送到主机，以响应 [**远程 \_ ndis \_ initialize \_ **](remote-ndis-initialize-msg.md) 消息消息。 在远程 \_ ndis \_ INITIALIZE \_ CMPLT 消息中，设备会报告其中型类型、远程 NDIS 版本号，并将其类型 (无连接或面向连接的) 。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>Offset</th>
<th>大小</th>
<th>字段</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>4</p></td>
<td><p>MessageType</p></td>
<td><p>指定要发送的消息的类型。 设置为数0x80000002。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>MessageLength</p></td>
<td><p>从消息的开头指定此消息的总长度（以字节为单位）。</p></td>
</tr>
<tr class="odd">
<td><p>8</p></td>
<td><p>4</p></td>
<td><p>RequestId</p></td>
<td><p>指定远程 NDIS 消息 ID 值。 此值用于匹配主机发送的包含设备响应的消息。</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>状态</p></td>
<td><p>如果设备初始化成功，则指定 RNDIS_STATUS_SUCCESS;否则，它将指定指示失败的错误代码。</p></td>
</tr>
<tr class="odd">
<td><p>16</p></td>
<td><p>4</p></td>
<td><p>MajorVersion</p></td>
<td><p>指定设备支持的最高远程 NDIS 主要协议版本。</p></td>
</tr>
<tr class="even">
<td><p>20</p></td>
<td><p>4</p></td>
<td><p>MinorVersion</p></td>
<td><p>指定设备支持的最高远程 NDIS 次协议版本。</p></td>
</tr>
<tr class="odd">
<td><p>24</p></td>
<td><p>4</p></td>
<td><p>DeviceFlags</p></td>
<td><p>将小型端口驱动程序类型指定为无连接或面向连接的。 此值可以为下列值之一：</p>
<p>RNDIS_DF_CONNECTIONLESS 0x00000001</p>
<p>RNDIS_DF_CONNECTION_ORIENTED 0x00000002</p></td>
</tr>
<tr class="even">
<td><p>28</p></td>
<td><p>4</p></td>
<td><p>中等</p></td>
<td><p>指定设备支持的介质。 设置为 RNDIS_MEDIUM_802_3 (0x00000000) </p></td>
</tr>
<tr class="odd">
<td><p>32</p></td>
<td><p>4</p></td>
<td><p>MaxPacketsPerMessage</p></td>
<td><p>指定设备在单个传输中可以处理的远程 NDIS 数据消息的最大数量。 此值至少应为1。</p></td>
</tr>
<tr class="even">
<td><p>36</p></td>
<td><p>4</p></td>
<td><p>MaxTransferSize</p></td>
<td><p>指定设备预期从主机接收的任何单个总线数据传输的最大大小（以字节为单位）。</p></td>
</tr>
<tr class="odd">
<td><p>40</p></td>
<td><p>4</p></td>
<td><p>PacketAlignmentFactor</p></td>
<td><p>指定设备需要对作为 multimessage 传输的一部分的每个远程 NDIS 消息使用的字节对齐方式。 此值是在2的幂中指定的。 例如，将此值设置为3，以指示8字节对齐。 此值的最大设置为7，这指定了128字节的对齐方式。</p></td>
</tr>
<tr class="even">
<td><p>44</p></td>
<td><p>4</p></td>
<td><p>AFListOffset</p></td>
<td><p>为面向连接的设备保留。 将值设置为零。</p></td>
</tr>
<tr class="odd">
<td><p>48</p></td>
<td><p>4</p></td>
<td><p>AFListSize</p></td>
<td><p>为面向连接的设备保留。 将值设置为零。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注解
-------

如果设备初始化成功，则 " *状态* " 字段应设置为 RNDIS \_ 状态 "成功" \_ ; 否则，它将设置为指示失败的错误代码。 设备应返回它可支持的最高远程 NDIS 协议版本（在 *MajorVersion* 和 *MinorVersion*中），组合版本号应小于或等于 [**远程 \_ ndis \_ 初始化 \_ **](remote-ndis-initialize-msg.md) 消息消息中指定的主机版本号。

*AFListSize*和*AFListOffset*字段仅与包含呼叫管理器的面向连接的设备相关。 无连接设备应将这些字段设置为零。

在此消息中，远程 NDIS 设备表示以下内容：

-   设备可以支持的最高远程 NDIS 协议版本号。 组合版本号应小于或等于主机在 [**远程 \_ NDIS \_ 初始化 \_ **](remote-ndis-initialize-msg.md) 消息消息中指定的版本号。 当主机实现的远程 NDIS 协议版本低于设备所支持的版本时，这允许设备回退到兼容性模式。

-   设备预期从主机接收的单个数据传输的最大大小（以字节为单位）。 该设备可以指定它预期用于作为 multimessage 传输的一部分的每个远程 NDIS 消息的字节对齐方式。 此对齐方式值是根据2的幂来指定的。 例如，将此值设置为3，以指示8字节对齐。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 Microsoft Windows XP 和更高版本的 Windows 操作系统中可用。 在 Windows 2000 中也可以作为可再发行二进制文件。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Rndis (包含 Rndis) </td>
</tr>
</tbody>
</table>

 

 




