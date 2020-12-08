---
title: 文件共享 (SMB) 符号服务器
description: 运行 SMB 符号服务器只是创建文件共享并向用户授予对该文件共享的访问权限。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1de5ed493436d356971564e1ee0253e3cecf6050
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838203"
---
# <a name="file-share-smb-symbol-server"></a>文件共享 (SMB) 符号服务器


运行 SMB 符号服务器只是创建文件共享并向用户授予对该文件共享的访问权限。

## <a name="span-idcreating_a_smb_file_share_symbol_store_spanspan-idcreating_a_smb_file_share_symbol_store_spanspan-idcreating_a_smb_file_share_symbol_store_spancreating-a-smb-file-share-symbol-store"></a><span id="Creating_a_SMB_File_Share_Symbol_Store_"></span><span id="creating_a_smb_file_share_symbol_store_"></span><span id="CREATING_A_SMB_FILE_SHARE_SYMBOL_STORE_"></span>创建 SMB 文件共享符号存储区


使用 Windows 资源管理器或 "计算机管理" 来创建文件共享并分配安全性。 这些步骤假设符号位于 *D： \\ SymStore \\ 符号* 中。 使用 Windows 资源管理器完成以下步骤：

1. 打开 **Windows 资源管理器**。

2. 选择并按住 (或右键单击) *D： \\ SymStore \\ 符号* ，然后选择 " **属性**"。

3. 选择 " **共享** " 选项卡。

4. 选择 **高级共享**.。。 .

5. 选中 " *共享此文件夹*"。

6. 选择“权限”。

7. 删除 *Everyone* 组。

8. 使用 " **添加 ...**" 添加需要访问权限的用户/安全组。

9. 对于添加的每个用户/安全组，授予 "读取" 或 "读取/更改" 访问权限。

10. 选择 **"确定"** (权限 "对话框) 。

11. 选择 **"确定" ("** 高级共享" 对话框) 。

12. 按) **关闭** (属性 "对话框。

使用 "计算机管理" 完成以下步骤：

1. 在 Windows 8) 中，键入 " *计算机* 在 Windows 启动 (解析为此电脑"。

2. 选择并按住 (或右键单击) 并选择 " *管理*"。

3. 导航到 " *系统工具" |共享文件夹 |共享*。

4. 选择并按住 (或右键单击) 并选择 " **新建" |共享 ...** .

5. 按 **下** (创建共享文件夹向导对话框) 。

6. 输入 **D： \\ SymStore \\ 符号** 作为文件夹路径。

7. 按两次 " **下一步** "。

8. 选择 " **自定义权限**"。

9. 按 "**自定义 ...** " .

10. 删除 *所有人*。

11. 使用 " **添加 ...**" 添加需要访问权限的用户/安全组。

12. 对于添加的每个用户/安全组，授予 "读取" 或 "读取/更改" 访问权限。

13. 按 **"确定" ("** 自定义权限" 对话框) 。

14. 按两次 " **完成** " 以完成该过程。

## <a name="span-idtest_the_smb_file_sharespanspan-idtest_the_smb_file_sharespanspan-idtest_the_smb_file_sharespantest-the-smb-file-share"></a><span id="Test_The_SMB_File_Share"></span><span id="test_the_smb_file_share"></span><span id="TEST_THE_SMB_FILE_SHARE"></span>测试 SMB 文件共享


将调试器配置为使用此符号路径：

```text
srv*C:\Symbols*\\MachineName\Symbols
```

若要查看在调试器中引用的 Pdb 的位置，请使用 lm (list 模块) 命令。 Pdb 的路径应以 C： \\ 符号开头。 通过运行 "！符号干扰" 和 "reload.sql/f"，你将看到从 \\ \\ MachineName \\ 符号文件服务器到 C：符号下载符号和图像的广泛的符号日志记录 \\ 。

## <a name="span-idfile_share_symbol_pathspanspan-idfile_share_symbol_pathspanspan-idfile_share_symbol_pathspanfile-share-symbol-path"></a><span id="File_Share_Symbol_Path"></span><span id="file_share_symbol_path"></span><span id="FILE_SHARE_SYMBOL_PATH"></span>文件共享符号路径


可以通过多种方式配置调试器的符号路径， ( sympath) 使用文件共享。 符号路径的语法确定符号文件是在本地缓存，还是在缓存中缓存。

直接文件共享使用 (没有本地缓存) ：

```text
srv*\\MachineName\Symbols
```

文件共享的文件到特定本地文件夹的本地缓存 (例如 c： \\ 符号) ：

```text
srv*c:\Symbols*\\MachineName\Symbols
```

将文件共享的文件本地缓存到% DBGHELP.DLL \_ HOMEDIR% \\ 符号文件夹中：

```text
srv**\\MachineName\Symbols
```

\*上面所示的示例中的第二个 "" 表示默认的本地服务器缓存。

如果 \_ 未设置 Dbghelp.dll HOMEDIR 变量，则 Dbghelp.dll \_ HOMEDIR 默认为 "调试器可执行文件" 文件夹 (例如 C： \\ Program files \\ windows 工具包 \\ 10.0 \\ 调试器 \\ x86) 并导致在 c： program files 中发生缓存 \\ \\ windows 工具包 \\ 10.0 \\ 调试器 \\ x86 \\ 符号。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[符号存储文件夹树](symbol-store-folder-tree.md)

 

 






