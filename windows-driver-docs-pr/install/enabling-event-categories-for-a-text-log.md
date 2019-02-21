---
title: 对于文本日志启用事件类别
description: 对于文本日志启用事件类别
ms.assetid: 555f698b-69e2-469b-b958-185cb35eeb5a
keywords:
- 事件类别 WDK SetupAPI 日志记录
- 文本日志 WDK SetupAPI，事件类别
- LogMask
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f5229398b921b6a2ff122096444b2349a60af1d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525964"
---
# <a name="enabling-event-categories-for-a-text-log"></a>对于文本日志启用事件类别


安装程序 Api 写入日志项中的文本日志仅当事件类别的文本日志启用了日志条目并[事件级别](setting-the-event-level-for-a-text-log.md)文本日志是等于或大于日志条目事件的事件级别。

下表列出了安装程序 Api 支持的事件类别，表示事件类别和清单常量的值的清单常量。

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
<td align="left"><p>管理文件的队列</p></td>
<td align="left"><p>TXTLOG_FILEQ</p></td>
<td align="left"><p>0x00000004</p></td>
</tr>
<tr class="even">
<td align="left"><p>将文件复制</p></td>
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
<td align="left"><p>管理用户界面对话框</p></td>
<td align="left"><p>TXTLOG_UI</p></td>
<td align="left"><p>0x00000100</p></td>
</tr>
<tr class="even">
<td align="left"><p>新的设备管理器</p></td>
<td align="left"><p>TXTLOG_NEWDEV</p></td>
<td align="left"><p>0x01000000</p></td>
</tr>
<tr class="odd">
<td align="left"><p>用户模式即插即用管理器</p></td>
<td align="left"><p>TXTLOG_UMPNPMGR</p></td>
<td align="left"><p>0x02000000</p></td>
</tr>
<tr class="even">
<td align="left"><p>管理驱动程序存储区</p></td>
<td align="left"><p>TXTLOG_DRIVER_STORE</p></td>
<td align="left"><p>0x04000000</p></td>
</tr>
<tr class="odd">
<td align="left"><p>类安装程序或辅助安装程序操作</p></td>
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

 

<a href="" id="to-enable-event-categories-for-the-setupapi-logs--create--or-modify--the-following-reg-dword-registry-value-"></a>若要启用 SetupAPI 日志的事件类别，创建 （或修改） 以下[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)注册表值：  
**HKEY_LOCAL_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Setup\\LogMask**

**LogMask**注册表值适用于设备安装文本日志和应用程序安装文本日志。

如果**LogMask**注册表值不存在，安装程序 Api 使文本日志的所有事件类别。 如果**LogMask**注册表值为零，则安装程序 Api 禁用文本日志的所有事件类别。

**LogMask**注册表值的格式设置为 0 X*VVVVVVVV，其中 VVVVVVVV*是 32 位域。 若要启用所有类别，设置**LogMask**为 0XFFFFFFFF。 若要启用特定的类别，请执行相应的事件类别常量的按位 OR。 例如：

-   若要编写的设备安装操作的日志项，设置**LogMask**为值的 TXTLOG_DEVINST (0X00000001)

-   若要编写的设备安装操作和驱动程序存储区操作的日志项，设置**LogMask**到 (TTXTLOG_DRIVER_STORE |TEXTLOG_DEVINST) (0X04000001)。

-   若要编写的自定义安装操作的日志项，设置**LogMask**到 TXTLOG_VENDOR (0x80000000)。

 

 





