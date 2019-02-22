---
title: 文件共享 (SMB) 符号服务器
description: 运行 SMB 符号服务器是只需创建文件共享和授予用户对该文件共享的访问权限。
ms.assetid: C5CF9665-9289-48EB-AA12-8881F812488A
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2bbaeed3a565e8854074439b410d2cc17494fff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545937"
---
# <a name="file-share-smb-symbol-server"></a>文件共享 (SMB) 符号服务器


运行 SMB 符号服务器是只需创建文件共享和授予用户对该文件共享的访问权限。

## <a name="span-idcreatingasmbfilesharesymbolstorespanspan-idcreatingasmbfilesharesymbolstorespanspan-idcreatingasmbfilesharesymbolstorespancreating-a-smb-file-share-symbol-store"></a><span id="Creating_a_SMB_File_Share_Symbol_Store_"></span><span id="creating_a_smb_file_share_symbol_store_"></span><span id="CREATING_A_SMB_FILE_SHARE_SYMBOL_STORE_"></span>创建 SMB 文件共享符号存储区


使用 Windows 资源管理器或计算机管理来创建文件共享并将安全性分配。 这些步骤假定符号，将位于*d:\\SymStore\\符号*。 完成这些步骤使用 Windows 资源管理器：

1. 打开**Windows 资源管理器**。

2. 右键单击*d:\\SymStore\\符号*，然后选择**属性**。

3. 单击**共享**选项卡。

4. 单击**高级共享**... .

5. 检查*共享此文件夹*。

6. 单击**权限**。

7. 删除*每个人都*组。

8. 使用**添加...**，添加需要访问权限的用户/安全组。

9. 添加每个用户/安全组、 授予读取或读取 / 更改访问权限。

10. 单击**确定**（权限对话框）。

11. 单击**确定**（高级共享对话框）。

12. 按**关闭**（属性对话框）。

完成这些步骤使用计算机管理：

1. 类型*计算机*窗口启动 （解析为 Windows 8 中的此电脑） 中。

2. 右键单击并选择*管理*。

3. 导航到*系统工具 |共享文件夹 |共享*。

4. 右键单击并选择**新建 |共享。** .

5. 按**下一步**（创建共享文件夹向导对话框）。

6. 输入**d:\\SymStore\\符号**作为文件夹路径。

7. 按**下一步**两次。

8. 选择**自定义权限**。

9. 按**自定义...** .

10. 删除*每个人都*。

11. 使用**添加...**，添加需要访问权限的用户/安全组。

12. 添加每个用户/安全组、 授予读取或读取 / 更改访问权限。

13. 按**确定**（自定义权限对话框）。

14. 按**完成**两次以完成该过程。

## <a name="span-idtestthesmbfilesharespanspan-idtestthesmbfilesharespanspan-idtestthesmbfilesharespantest-the-smb-file-share"></a><span id="Test_The_SMB_File_Share"></span><span id="test_the_smb_file_share"></span><span id="TEST_THE_SMB_FILE_SHARE"></span>测试 SMB 文件共享


配置调试程序要使用此符号路径：

```text
srv*C:\Symbols*\\MachineName\Symbols
```

若要查看正在引用在调试器中的 Pdb 的位置，请使用 lm （模块列表） 命令。 Pdb 的路径应所有开始使用 c:\\符号。 通过运行"！ 干扰性的符号"，".reload /f"，会看到大量的符号的符号和中的映像的下载的日志记录\\ \\MachineName\\符号文件服务器到 c:\\符号。

## <a name="span-idfilesharesymbolpathspanspan-idfilesharesymbolpathspanspan-idfilesharesymbolpathspanfile-share-symbol-path"></a><span id="File_Share_Symbol_Path"></span><span id="file_share_symbol_path"></span><span id="FILE_SHARE_SYMBOL_PATH"></span>文件共享符号路径


有多个方法可用于配置调试器的符号路径 (.sympath) 若要使用文件共享。 符号路径的语法确定本地或不是，将缓存符号文件和缓存位置。

（无本地缓存） 的直接文件共享使用：

```text
srv*\\MachineName\Symbols
```

本地缓存的文件共享的文件复制到特定的本地文件夹 (例如 c:\\符号):

```text
srv*c:\Symbols*\\MachineName\Symbols
```

本地缓存的文件共享的文件复制到 %dbghelp\_主目录 %\\符号文件夹：

```text
srv**\\MachineName\Symbols
```

第二个"\*"在如上所示示例中，表示默认的本地服务器缓存。

如果 DBGHELP\_HOMEDIR 变量未设置，DBGHELP\_HOMEDIR 默认为调试器可执行文件文件夹 (例如 c:\\Program Files\\Windows 工具包\\10.0\\调试器\\x86)，并使缓存以 c： 驱动器中发生\\Program Files\\Windows 工具包\\10.0\\调试器\\x86\\Sym.

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[符号存储区文件夹树](symbol-store-folder-tree.md)

 

 






