---
title: ESRT 表定义
description: 指向 ESRT 表的指针通过其在 EFI_CONFIGURATION_TABLE 中的相应 GUID 标识。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 455cf80dda8e479a5d83d77576c1384bded7e497
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803353"
---
# <a name="esrt-table-definition"></a>ESRT 表定义


指向 ESRT 表的指针通过其在 EFI 配置表中的相应 GUID \_ 标识 \_ 。

```cpp
#define EFI_SYSTEM_RESOURCE_TABLE_GUID   \
{ 0xb122a263, 0x3661, 0x4f68,  0x99, 0x29, 0x78, 0xf8, 0xb0, 0xd6, 0x21, 0x80  }
```

下表描述了 ESRT 表的格式和表中包含的固件资源条目。

<table>
<colgroup>
<col width="20%" />
<col width="10%" />
<col width="10%" />
<col width="10%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>字段</th>
<th>数组值</th>
<th>字节长度</th>
<th>字节偏移量</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>固件资源计数</td>
<td></td>
<td>4</td>
<td>0</td>
<td>ESRT 中的固件资源条目数。 不得为零。</td>
</tr>
<tr class="even">
<td>固件资源最大值</td>
<td></td>
<td>4</td>
<td>4</td>
<td>在不重新分配表的情况下可以添加的资源数组条目的最大数目。 必须大于或等于固件资源计数。</td>
</tr>
<tr class="odd">
<td>固件资源版本</td>
<td></td>
<td>8</td>
<td>8</td>
<td>固件资源条目版本。 此值应设置为1。</td>
</tr>
<tr class="even">
<td>固件资源条目数组</td>
<td></td>
<td></td>
<td></td>
<td>固件资源条目0</td>
</tr>
<tr class="odd">
<td></td>
<td>固件类</td>
<td>16</td>
<td>16</td>
<td>标识可通过 update 胶囊更新的固件组件的 GUID。 在更新过程中，此 GUID 将作为 update 胶囊标头的 CapsuleGuid 参数传递到 UEFI 更新包运行时服务。</td>
</tr>
<tr class="even">
<td></td>
<td>固件类型</td>
<td>4</td>
<td>32</td>
<td>标识固件资源类型的下列值之一：
<ul>
<li>0：未知</li>
<li>1：系统固件</li>
<li>2：设备固件</li>
<li>3： UEFI 驱动程序</li>
</ul></td>
</tr>
<tr class="odd">
<td></td>
<td>固件版本</td>
<td>4</td>
<td>36</td>
<td>当前固件版本，其中较大的数字表示较新的版本。 此值的格式未定义，但应包含版本的主要版本号和次要版本号。 建议的格式为第一个字，第二个单词为次要版本号。</td>
</tr>
<tr class="even">
<td></td>
<td>支持的最低固件版本</td>
<td>4</td>
<td>40</td>
<td>固件资源可针对给定系统/设备回滚到的最低固件资源版本。 如果此固件版本中提供了与安全相关的修补程序，则兼容性最低的版本应等于当前固件版本。</td>
</tr>
<tr class="odd">
<td></td>
<td>胶囊标志</td>
<td>4</td>
<td>44</td>
<td>将传入 UEFI 更新胶囊运行时服务的标志，在 update 胶囊标头的 "标志" 字段 (的位0–15中，负责配置 UEFI 规范) 部分7.5.3 定义的标志的位 16-31。</td>
</tr>
<tr class="even">
<td></td>
<td>上次尝试版本</td>
<td>4</td>
<td>48</td>
<td>尝试更新的最后一个固件版本。 此值使用与固件版本相同的格式。</td>
</tr>
<tr class="odd">
<td></td>
<td>上次尝试状态</td>
<td>4</td>
<td>52</td>
<td>描述上次固件更新尝试状态的下列值之一：
<ul>
<li>0：成功</li>
<li>1：失败</li>
<li>2：资源不足</li>
<li>3：版本不正确</li>
<li>4：图像格式无效</li>
<li>5：身份验证错误</li>
<li>6：电源事件-未连接 AC</li>
<li>7：电源事件-电池不足</li>
</ul></td>
</tr>
<tr class="even">
<td> ...</td>
<td></td>
<td></td>
<td></td>
<td>固件资源条目1</td>
</tr>
</tbody>
</table>

 

为了 (系统固件) ，核心 UEFI 固件应分配和填充包含一个系统资源条目的 "ESRT" 配置表。 出于说明目的，在本指南中，核心固件还将创建一个额外的条目，该条目表示使用固件更新包机制支持设备固件更新的设备。

必须始终有一个描述系统固件的条目。 此条目用于作为系统固件更新的目标。 如果实现将系统和设备固件更新作为单一单一操作执行，则必须使用系统固件条目作为更新的目标。 在所有其他情况下，设备固件更新的目标是描述设备固件的 ESRT 项。

第一步是生成 Guid，用于表示这两个固件资源，即 {系统 \_ 固件} 和 {设备 \_ 固件}。 表2显示了一个表定义的示例。 此示例假设两个固件版本当前为版本 1 (固件版本 = = 1) 。

| 字段                         | 数组值                       | 值                     | 注释                                                                                                            |
|-------------------------------|-----------------------------------|---------------------------|--------------------------------------------------------------------------------------------------------------------|
| 固件资源计数       |                                   | 2                         | 此表包含两个固件资源条目。                                                                 |
| 固件资源最大值     |                                   | 2                         | 此表分配包含足够的空间，最多可描述两个资源。                                |
| 固件资源版本     |                                   | 1                         | 此表使用的固件资源条目格式版本为1。                                                   |
| 固件资源条目数组 |                                   | 固件资源条目0 |                                                                                                                    |
|                               | 固件类                    |  (系统 \_ 固件)         | 此 GUID 标识用于通过 PnP 进行更新的系统固件。                                                       |
|                               | 固件类型                     | 1                         | 系统固件类型为1。                                                                                         |
|                               | 固件版本                  | 1                         | 当前系统固件版本为1。                                                                          |
|                               | 支持的最低固件版本 | 1                         | 支持的最低固件版本为1，因此固件不能回滚到版本1之前的版本。 |
|                               | 胶囊标志                     | 0                         | 系统固件未定义任何专用胶囊更新标志。                                                   |
|                               | 上次尝试版本              | 1                         | 上次尝试更新的系统固件版本为版本1。                                  |
|                               | 上次尝试状态               | 0                         | 上次系统固件更新尝试成功。                                                            |
|                               |                                   | 固件资源条目1 |                                                                                                                    |
|                               | 固件类                    |  (设备 \_ 固件)         | 此 GUID 标识通过 PnP 进行更新的设备固件。                                                       |
|                               | 固件类型                     | 2                         | 设备固件类型为2。                                                                                         |
|                               | 固件版本                  | 1                         | 当前设备固件版本为1。                                                                          |
|                               | 支持的最低固件版本 | 1                         | 支持的最低固件版本为1，因此无法将固件回滚到版本1之前的版本。 |
|                               | 胶囊标志                     | 0x8010                    | 设备固件定义专用胶囊更新标志 (0x8010) 。                                                     |
|                               | 上次尝试版本              | 1                         | 尝试更新的最后一个设备固件版本是版本1                                    |
|                               | 上次尝试状态               | 0                         | 上次设备固件更新尝试成功。                                                            |

 

此文档中的其他位置使用上述 ESRT 示例来逐步完成固件更新过程，并介绍更新过程的 Windows 支持以及支持固件实现。

## <a name="related-topics"></a>相关主题
[即插即用设备](plug-and-play-device.md)  
[创作更新驱动程序包](authoring-an-update-driver-package.md)  
[处理更新](processing-updates.md)  
[来自 UEFI 环境的设备 I/O](device-i-o-from-the-uefi-environment.md)  
[无缝危机预防和恢复](seamless-crisis-prevention-and-recovery.md)  
[固件更新状态](firmware-update-status.md)  



