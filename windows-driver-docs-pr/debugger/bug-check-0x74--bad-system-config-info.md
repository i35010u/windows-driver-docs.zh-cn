---
title: Bug 检查 0x74 BAD_SYSTEM_CONFIG_INFO
description: BAD_SYSTEM_CONFIG_INFO bug 检查具有 0x00000074 值。 检查此错误指示在注册表中存在错误。
ms.assetid: c59ddc44-d860-4fbb-a975-ae7226fdce86
keywords:
- Bug 检查 0x74 BAD_SYSTEM_CONFIG_INFO
- BAD_SYSTEM_CONFIG_INFO
ms.date: 08/17/2018
topic_type:
- apiref
api_name:
- BAD_SYSTEM_CONFIG_INFO
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a659f649ce7950b466b85499c27d08123cb5ce40
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523377"
---
# <a name="bug-check-0x74-badsystemconfiginfo"></a>Bug 检查 0x74:错误\_系统\_CONFIG\_信息


缺点\_系统\_CONFIG\_信息错误检查的值为 0x00000074。 检查此错误指示在注册表中存在错误。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="badsystemconfiginfo-parameters"></a>错误\_系统\_CONFIG\_信息参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>NT 状态值/代码 （如果可用）</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

缺点\_系统\_CONFIG\_如果系统配置单元已损坏，则会出现信息 bug 检查。 但是，这种损坏，不太可能，因为引导加载程序，在加载配置单元时检查已损坏的 hive。

如果是缺少一些关键的注册表项和值，也可能发生此错误检查。 如果手动编辑注册表，用户或应用程序或服务损坏注册表，键和值可能会丢失。

查找参数 4 中返回的 NT 状态值可以提供其他信息，请参阅[NTSTATUS 值](https://msdn.microsoft.com/library/cc704588.aspx)有关的列表。 

<a name="resolution"></a>分辨率
----------

尝试进入安全模式启动，然后正常重新启动操作系统。 如果在重新启动无法解决问题，是太多，注册表损坏。 请尝试以下步骤。

-   如果您的系统还原点，请尝试还原到早期的还原点。
-   重置您的 PC。
-   使用安装媒体还原或重置您的 PC。
-   使用安装媒体重新安装 Windows。

有关详细信息，请参阅[Windows 10 中的恢复选项](https://windows.microsoft.com/windows-10/windows-10-recovery-options#)。

 

 




