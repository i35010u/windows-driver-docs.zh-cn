---
title: 跨计算机执行
description: 跨计算机执行
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7aa0cd6151759b57410daf50137c47e1328df1de
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790863"
---
# <a name="cross-machine-execution"></a>跨计算机执行


TAEF 支持在一台计算机上执行 Te.exe，但在单独的计算机上运行测试。 TAEF 对所需的二进制文件进行身份验证、授权和部署，以执行测试并将所有信息记录回原始控制台。

## <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>先决条件


为了远程执行测试，需要满足以下要求：

-   你必须在 **目标计算机** 上安装并运行 (x86 或 x64) 的 [服务](te-service.md)。

### <a name="span-idexecuting_with_domain_accountsspanspan-idexecuting_with_domain_accountsspanspan-idexecuting_with_domain_accountsspanexecuting-with-domain-accounts"></a><span id="Executing_with_domain_accounts"></span><span id="executing_with_domain_accounts"></span><span id="EXECUTING_WITH_DOMAIN_ACCOUNTS"></span>用域帐户执行

-   域帐户必须是目标计算机上的管理员或本地 "Remote TAEF Users" 组的成员。

### <a name="span-idexecuting_with_non-domain_accountsspanspan-idexecuting_with_non-domain_accountsspanspan-idexecuting_with_non-domain_accountsspanexecuting-with-non-domain-accounts"></a><span id="Executing_with_non-domain_accounts"></span><span id="executing_with_non-domain_accounts"></span><span id="EXECUTING_WITH_NON-DOMAIN_ACCOUNTS"></span>用非域帐户执行

-   本地 (非域帐户) 必须在两台计算机上都具有相同的用户名和密码。
-   该用户必须是目标计算机上的本地 "Remote TAEF Users" 组的成员。
-   在主计算机上，本地用户可以执行 Te.exe，或者也可以将本地用户的一般凭据添加到凭据管理器。

    ``` syntax
    cmdkey /generic:<targetmachine> /user:<user_name> /pass:[PLACEHOLDER]
    ```

-   如果在已加入域的计算机上运行，则加入域的计算机必须具有 IPSec 边界排除项。

## <a name="span-idexecuting_tests_remotelyspanspan-idexecuting_tests_remotelyspanspan-idexecuting_tests_remotelyspanexecuting-tests-remotely"></a><span id="Executing_Tests_Remotely"></span><span id="executing_tests_remotely"></span><span id="EXECUTING_TESTS_REMOTELY"></span>远程执行测试


### <a name="span-id_runon_spanspan-id_runon_spanspan-id_runon_spanrunon"></a><span id="_runOn_"></span><span id="_runon_"></span><span id="_RUNON_"></span>runOn

若要远程运行测试，必须指定 **/runOn： &lt; machine name &gt;** 参数，使其与其他命令一起 Te.exe。 如果满足先决条件，用户体验的其余部分将与在本地执行测试时发现的其他体验相同。 所有日志输出都将保存/写入到本地计算机。

例如：

``` syntax
te unittests\wex.common.tests.dll /runon:TAEFTest1
```

-   将你的测试的所有必需的二进制文件发送到目标计算机 (TAEFTest1) 并远程执行 wex.common.tests.dll 中存在的所有 TAEF 测试，同时重新登录到控制台。

如果由于 HRESULT 0x800706BA 而无法连接到远程计算机，并且确保正确拼写了计算机名称，请尝试使用计算机的 IP 地址或使用 **/disableTimeouts** 开关。 有时，DNS 延迟可能会足够大，从而导致连接尝试超时。

**注意：** 如果这是第一次指定 **/runOn：** 命令，可能需要在 Te.exe 的防火墙排除对话框上单击 " **解除阻止** "。

### <a name="span-idtest_dependenciesspanspan-idtest_dependenciesspanspan-idtest_dependenciesspantest-dependencies"></a><span id="Test_Dependencies"></span><span id="test_dependencies"></span><span id="TEST_DEPENDENCIES"></span>测试依赖项

Te.exe 自动确定你的测试的所有本机和托管模块依赖项，并将它们连同你的测试 dll 一起发送到远程计算机。 这不包括 *系统* 二进制文件以及测试所需的任何 COM 库。

可以通过 **/TestDependencies** 命令行参数以分号分隔的文件或要复制的目录列表的形式手动指定其他测试依赖项。

- **文件**

  每个文件规范都可以包含通配符 ( # A0;请 \* ) 。 例如：

  ``` syntax
  te unittests\wex.common.tests.dll /runon:TAEFTest1 /TestDependencies:*verification*.jpg;mysample.txt
  ```
  -   将你的测试的所有必需的二进制文件发送到 TAEFTest1 以及找到的与 **/TestDependencies** 参数中指定的文件相匹配的任何文件。
- **Directories**

  对于包含测试二进制 *文件的目录* ，TAEF 支持递归目录搜索。 例如：

  ``` syntax
  te unittests\wex.common.tests.dll /runon:TAEFTest1 /TestDependencies:unittests\...
  ```

  -   将你的测试的所有必需的二进制文件发送到 TAEFTest1 以及 *run-unittests* 目录内或下面的所有文件/目录。 TAEF 保留目录层次结构。

  ``` syntax
  _    te unittests\wex.common.tests.dll /runon:TAEFTest1 /TestDependencies:unittests\*.jpg...
  ```

  -   将你的测试的所有必需的二进制文件发送到 TAEFTest1 以及 *run-unittests* 目录内或下面的所有 jpg 文件。 TAEF 保留目录层次结构。

  <strong>注意：</strong>如果为测试目录或测试目录 *下* 不存在的目录指定递归或非递归目录搜索，则所有文件都将复制到远程计算机，但会平展目录层次结构。

可以通过[DeploymentItem 元数据](deploymentitem-metadata.md)aso 指定测试依赖项

## <a name="user-context"></a>用户上下文 


默认情况下，TAEF 会尝试在远程计算机上使用用户上下文来运行测试。 它通过以下方法实现此目的：

-   枚举远程计算机上的所有活动会话，并查找你拥有的会话。
    -   如果 TAEF 在远程计算机上查找到你拥有的会话，它将在该会话中运行该会话 () 。

        **注意：** 这不一定是控制台会话。 它可以是远程桌面会话。

    -   如果 TAEF 在远程计算机上 **找不到** 您拥有的会话，它将以登录到控制台会话的用户（在该桌面上 (）运行测试，) 。
    -   最后，如果没有在远程计算机上拥有会话，并且没有人登录到控制台会话，TAEF 将在会话0中运行测试， (非交互式) 。

### <a name="span-idrunasspanspan-idrunasspanspan-idrunasspanrunas"></a><span id="RunAs"></span><span id="runas"></span><span id="RUNAS"></span>方式

如果除了 **/runOn** 以外，还指定了 [/RunAs](runas.md)值，TAEF 除了需要满足 **/runAs** 设置所需的试探法外，还使用了上述试探法。 例如：

``` syntax
te unittests\wex.common.tests.dll /runon:TAEFTest1 /runas:system
```

-   用系统帐户执行 TAEFTest1 wex.common.tests.dll 中存在的所有 TAEF 测试。

## <a name="span-idhow_it_worksspanspan-idhow_it_worksspanspan-idhow_it_worksspanhow-it-works"></a><span id="How_It_Works"></span><span id="how_it_works"></span><span id="HOW_IT_WORKS"></span>工作原理


-   Te.exe 连接到在远程计算机上运行的 Te 的实例。
    -   Windows 身份验证 (协商) 通过 Te 身份验证。
    -   Te 将验证你是否为远程计算机上的管理员或本地 "Remote TAEF Users" 组的成员。
-   Te 在 *RemoteTests* 下创建与测试 dll 同名的目录。
-   Te.exe 生成在远程计算机上执行测试所需的文件的列表。 此列表包括：
    -   必需的 TAEF 二进制文件
    -   测试 dll 的所有本机和/或托管二进制依赖项 (排除系统二进制文件) 
    -   **/TestDependencies** 参数中指定的任何其他文件
-   Te.exe 会将测试依赖项列表连同每个文件的 CRCs 一起发送到 Te 服务。
-   Te：服务查找远程计算机上的每个文件，并对 CRC 值进行比较。 所有匹配项都将从列表中删除，并且会将该列表发送回客户端。
-   如果依赖项列表中遗留有任何文件，Te.exe 会将每个依赖项发送到 Te。
    -   Te 服务将这些文件保存在 &lt; &gt; \\ RemoteTests 目录 \\ &lt; 中。 &gt;
-   Te.exe 要求 Te 服务在远程计算机上使用正确的 [用户上下文](#user-context)启动新的 Te.ProcessHost.exe 实例。
-   Te.exe 连接到远程 Te.ProcessHost.exe 实例，并开始执行测试。

 

 





