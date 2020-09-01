---
title: 启用文本日志的事件类别
description: 启用文本日志的事件类别
ms.assetid: 555f698b-69e2-469b-b958-185cb35eeb5a
keywords:
- 事件类别 WDK Setupapi.log 日志记录
- 文本日志 WDK Setupapi.log，事件类别
- LogMask
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b4a3f6997b684b368298a5cf12e2a12e119ac22
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097169"
---
# <a name="enabling-event-categories-for-a-text-log"></a>启用文本日志的事件类别


仅当为文本日志启用了日志条目的事件类别并且文本日志的 [事件级别](setting-the-event-level-for-a-text-log.md) 等于或大于日志条目的事件级别时，setupapi.log 才会在文本日志中写入日志条目。

下表列出了 Setupapi.log 支持的事件类别、表示事件类别的清单常量以及清单常量的值。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">事件类别操作</th>
<th align="left">事件类别清单常量</th>
<th align="left">事件类别值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>设备安装</p></td>
<td align="left"><p>TXTLOG_DEVINST</p></td>
<td align="left"><p>0x00000001</p></td>
</tr>
<tr class="even">
<td align="left"><p>管理 INF 文件</p></td>
<td align="left"><p>TXTLOG_INF</p></td>
<td align="left"><p>0x00000002</p></td>
</tr>
<tr class="odd">
<td align="left"><p>管理文件队列</p></td>
<td align="left"><p>TXTLOG_FILEQ</p></td>
<td align="left"><p>0x00000004</p></td>
</tr>
<tr class="even">
<td align="left"><p>复制文件</p></td>
<td align="left"><p>TXTLOG_COPYFILES</p></td>
<td align="left"><p>0x00000008</p></td>
</tr>
<tr class="odd">
<td align="left"><p>管理注册表设置</p></td>
<td align="left"><p>TXTLOG_REGISTRY</p></td>
<td align="left"><p>0x00000010</p></td>
</tr>
<tr class="even">
<td align="left"><p>验证数字签名</p></td>
<td align="left"><p>TXTLOG_SIGVERIF</p></td>
<td align="left"><p>0x00000020</p></td>
</tr>
<tr class="odd">
<td align="left"><p>管理设备和驱动程序属性</p></td>
<td align="left"><p>TXTLOG_PROPERTIES</p></td>
<td align="left"><p>0x00000040</p></td>
</tr>
<tr class="even">
<td align="left"><p>备份数据</p></td>
<td align="left"><p>TXTLOG_BACKUP</p></td>
<td align="left"><p>0x00000080</p></td>
</tr>
<tr class="odd">
<td align="left"><p>"管理用户界面" 对话框</p></td>
<td align="left"><p>TXTLOG_UI</p></td>
<td align="left"><p>0x00000100</p></td>
</tr>
<tr class="even">
<td align="left"><p>新设备管理器</p></td>
<td align="left"><p>TXTLOG_NEWDEV</p></td>
<td align="left"><p>0x01000000</p></td>
</tr>
<tr class="odd">
<td align="left"><p>用户模式 PnP 管理器</p></td>
<td align="left"><p>TXTLOG_UMPNPMGR</p></td>
<td align="left"><p>0x02000000</p></td>
</tr>
<tr class="even">
<td align="left"><p>管理驱动程序存储</p></td>
<td align="left"><p>TXTLOG_DRIVER_STORE</p></td>
<td align="left"><p>0x04000000</p></td>
</tr>
<tr class="odd">
<td align="left"><p>类安装程序或共同安装程序操作</p></td>
<td align="left"><p>TXTLOG_INSTALLER</p></td>
<td align="left"><p>0x40000000</p></td>
</tr>
<tr class="even">
<td align="left"><p>供应商提供的操作</p></td>
<td align="left"><p>TXTLOG_VENDOR</p></td>
<td align="left"><p>0x80000000</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="to-enable-event-categories-for-the-setupapi-logs--create--or-modify--the-following-reg-dword-registry-value-"></a>若要为 Setupapi.log 日志启用事件类别，请创建 (或修改) 以下 [REG_DWORD](/windows/desktop/SysInfo/registry-value-types) 注册表值：  
**HKEY_LOCAL_MACHINE \\ Software \\ Microsoft \\ Windows \\ CurrentVersion \\ 安装程序 \\ LogMask**

**LogMask**注册表值适用于设备安装文本日志和应用程序安装文本日志。

如果 **LogMask** 注册表值不存在，则 setupapi.log 将启用文本日志的所有事件类别。 如果 **LogMask** 注册表值为零，则 setupapi.log 将禁用文本日志的所有事件类别。

**LogMask**注册表值的格式为 0x*VVVVVVVV，其中 VVVVVVVV*为32位域。 若要启用所有类别，请将 **LogMask** 设置为0xffffffff。 若要仅启用特定类别，请对相应的事件类别常量执行按位 "或" 运算。 例如：

-   若要仅启用由设备安装操作写入的日志条目，请将 **LogMask** 设置为 TXTLOG_DEVINST (0x00000001 的值) 

-   若要仅启用由设备安装操作和驱动程序存储操作编写的日志条目，请将 **LogMask** 设置为 (TTXTLOG_DRIVER_STORE |TEXTLOG_DEVINST)  (0x04000001) 。

-   若要仅启用由自定义安装操作写入的日志条目，请将 **LogMask** 设置为 TXTLOG_VENDOR (0x80000000) "。

 

