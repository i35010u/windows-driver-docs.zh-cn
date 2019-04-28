---
title: 如何管理 PFA 内存列表
description: 如何管理 PFA 内存列表
ms.assetid: 28463f91-275b-4ad4-af64-59bed7fd3806
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9b8e74e2307f7e8da4d02db62368c164336a55a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340815"
---
# <a name="how-to-manage-the-pfa-memory-list"></a>如何管理 PFA 内存列表


您可以查看和删除通过使用 BCDEdit 命令行工具在 BCD 系统存储中保存的内存页的列表。 若要使用 BCDEdit 工具时，必须是计算机上 Administrators 组的成员，并从提升的命令提示符运行 BCDEdit。 若要打开提升的命令提示符窗口，请执行以下步骤：

1.  单击**启动**，依次指向**所有程序**，然后单击**附件**。

2.  右键单击**命令提示符**，然后选择**以管理员身份运行**。

3.  如果显示用户帐户控制对话框中，单击**是**对话框框中。

### <a name="viewing-the-current-list-of-pfns"></a>查看当前的 PFNs 列表

若要在 BCD 系统存储区中查看 PFNs 的当前列表，请运行以下命令：

``` syntax
C:\Windows\system32>bcdedit /enum {badmemory}
```

如果没有 ECC 内存页预测失败，BCDEdit 工具的输出将显示如以下示例所示：

``` syntax
C:\Windows\system32>bcdedit /enum {badmemory}

RAM Defects
-----------
identifier              {badmemory}
```

如果预测 ECC 内存页失败， **{badmemory}** 对象包含**badmemorylist**值。 此值包含 PFA 预测的页将会失败的内存 PFNs 的列表，如下面的示例中所示：

``` syntax
C:\Windows\system32>bcdedit /enum {badmemory}

RAM Defects
-----------
identifier              {badmemory}
badmemorylist           0xffe38
                        0x100f
```

### <a name="clearing-the-current-list-of-pfns"></a>清除当前的 PFNs 列表

若要清除 PFNs BCD 系统存储中的列表，请运行以下命令：

``` syntax
C:\Windows\system32>bcdedit /deletevalue {badmemory} badmemorylist
```

**请注意**  不正确更改到 BCD 系统存储区可以防止 Windows 启动。 因此，必须的命令，其结果之前仔细查看重启 Windows。

 

 

 




