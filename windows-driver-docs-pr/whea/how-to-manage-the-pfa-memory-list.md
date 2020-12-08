---
title: 如何管理 PFA 内存列表
description: 如何管理 PFA 内存列表
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7876a69f2a9a1da14e1285227ea317f9151599b6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809745"
---
# <a name="how-to-manage-the-pfa-memory-list"></a>如何管理 PFA 内存列表


您可以使用 BCDEdit 命令行工具查看和删除在 BCD 系统存储区中保存的内存页的列表。 若要使用 BCDEdit 工具，你必须是计算机上 Administrators 组的成员，并从提升的命令提示符运行 BCDEdit。 若要打开提升的命令提示符窗口，请执行以下步骤：

1.  单击 " **开始**"，指向 " **所有程序**"，然后单击 " **附件**"。

2.  右键单击“命令提示符”并选择“以管理员身份运行”。 

3.  如果显示了 "用户帐户控制" 对话框，请单击对话框中的 **"是"** 。

### <a name="viewing-the-current-list-of-pfns"></a>查看 PFNs 的当前列表

若要查看 BCD 系统存储中的 PFNs 的当前列表，请运行以下命令：

``` syntax
C:\Windows\system32>bcdedit /enum {badmemory}
```

如果未预测 ECC 内存页出现故障，则 BCDEdit 工具的输出将如以下示例中所示：

``` syntax
C:\Windows\system32>bcdedit /enum {badmemory}

RAM Defects
-----------
identifier              {badmemory}
```

如果预测 ECC 内存页失败，则 **{badmemory}** 对象将包含一个 **badmemorylist** 值。 此值包含 PFA 预测将失败的内存页的 PFNs 列表，如以下示例中所示：

``` syntax
C:\Windows\system32>bcdedit /enum {badmemory}

RAM Defects
-----------
identifier              {badmemory}
badmemorylist           0xffe38
                        0x100f
```

### <a name="clearing-the-current-list-of-pfns"></a>清除当前的 PFNs 列表

若要清除 BCD 系统存储中的 PFNs 列表，请运行以下命令：

``` syntax
C:\Windows\system32>bcdedit /deletevalue {badmemory} badmemorylist
```

**注意**  更改 BCD 系统存储会阻止 Windows 启动。 因此，在重新启动 Windows 之前，必须仔细查看命令和结果。

 

 

 




