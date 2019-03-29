---
title: 跨计算机执行
description: 跨计算机执行
ms.assetid: FDDD2320-E853-45a8-9820-12FB16365B9C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c65d90e3dc148cef086aadbe67a89bff47e7a234
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575359"
---
# <a name="cross-machine-execution"></a>跨计算机执行


TAEF 支持一台计算机上执行 Te.exe，但在单独的计算机上运行测试的功能。 TAEF 进行身份验证，授权，并将部署的必要二进制文件执行的测试并返回到原始控制台日志的所有信息。

## <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>先决条件


远程执行测试所需，还有下列要求：

-   必须安装并运行[Te.Service](te-service.md) （x86 或 x64） 上**目标计算机**。

### <a name="span-idexecutingwithdomainaccountsspanspan-idexecutingwithdomainaccountsspanspan-idexecutingwithdomainaccountsspanexecuting-with-domain-accounts"></a><span id="Executing_with_domain_accounts"></span><span id="executing_with_domain_accounts"></span><span id="EXECUTING_WITH_DOMAIN_ACCOUNTS"></span>执行使用域帐户

-   域帐户必须是管理员或本地目标计算机上的"远程 TAEF 用户"组的成员。

### <a name="span-idexecutingwithnon-domainaccountsspanspan-idexecutingwithnon-domainaccountsspanspan-idexecutingwithnon-domainaccountsspanexecuting-with-non-domain-accounts"></a><span id="Executing_with_non-domain_accounts"></span><span id="executing_with_non-domain_accounts"></span><span id="EXECUTING_WITH_NON-DOMAIN_ACCOUNTS"></span>执行带有非域帐户

-   本地 （非域帐户） 必须存在具有相同的用户名和两台计算机上的密码。
-   该用户必须是本地目标计算机上的"远程 TAEF 用户"组的成员。
-   在主机上本地用户都可以执行 Te.exe，，或者，或者，可能会将泛型凭据为本地用户添加到凭据管理器。

    ``` syntax
    cmdkey /generic:<targetmachine> /user:<user_name> /pass:<password>
    ```

-   如果你已加入域的计算机上运行，已加入域的计算机必须具有 IPSec 边界排除项。

## <a name="span-idexecutingtestsremotelyspanspan-idexecutingtestsremotelyspanspan-idexecutingtestsremotelyspanexecuting-tests-remotely"></a><span id="Executing_Tests_Remotely"></span><span id="executing_tests_remotely"></span><span id="EXECUTING_TESTS_REMOTELY"></span>远程执行测试


### <a name="span-idrunonspanspan-idrunonspanspan-idrunonspanrunon"></a><span id="_runOn_"></span><span id="_runon_"></span><span id="_RUNON_"></span>/runOn:

若要远程运行测试，必须指定 **/runOn:&lt;机器名&gt;** Te.exe 其余部分的命令参数。 如果满足先决条件时，用户体验的其余部分将具有与执行本地测试时发现的相同。 所有日志输出将保存/都写入到本地计算机。

例如：

``` syntax
te unittests\wex.common.tests.dll /runon:TAEFTest1
```

-   将用于测试的所有必要二进制文件发送到目标计算机 (TAEFTest1) 和远程执行 wex.common.tests.dll 时返回到你的控制台日志记录中存在的所有 TAEF 测试。

如果无法连接到远程计算机，所以 HRESULT 0x800706BA 并且您确信您的计算机名称是否拼写正确，请尝试使用计算机的 IP 地址，或者使用 **/disableTimeouts**切换。 有时，DNS 延迟可能足够大，导致连接尝试超时。

**注意：** 如果这是首次指定 **/runOn:** 命令时，可能需要单击**解除阻止**Te.exe 防火墙排除对话框上。

### <a name="span-idtestdependenciesspanspan-idtestdependenciesspanspan-idtestdependenciesspantest-dependencies"></a><span id="Test_Dependencies"></span><span id="test_dependencies"></span><span id="TEST_DEPENDENCIES"></span>测试依赖项

Te.exe 自动确定的所有测试的本机和托管模块依赖项，并将其发送到测试 dll 以及在远程计算机。 这不包括*系统*二进制文件，以及你的测试要求任何 COM 库。

你可以手动指定其他测试通过的依赖关系 **/TestDependencies**形式的以分号分隔列表的文件或目录复制的命令行参数。

- **文件**

  每个文件规范可包含通配符字符 (test.txt; 测试\*.dll; 等等。)。 例如：

  ``` syntax
  te unittests\wex.common.tests.dll /runon:TAEFTest1 /TestDependencies:*verification*.jpg;mysample.txt
  ```
  -   将所有必要的二进制文件发送到 TAEFTest1，以及任何文件在测试中找到的匹配中指定的文件 **/TestDependencies**参数。
- **目录**

  TAEF 支持递归目录搜索的目录存在*或以下*包含测试二进制文件的目录。 例如：

  ``` syntax
  te unittests\wex.common.tests.dll /runon:TAEFTest1 /TestDependencies:unittests\...
  ```

  -   用于测试的所有必要二进制文件发送到 TAEFTest1 以及所有文件/目录中或低于*unittests*目录。 TAEF 保留的目录层次结构。

  ``` syntax
  _    te unittests\wex.common.tests.dll /runon:TAEFTest1 /TestDependencies:unittests\*.jpg...
  ```

  -   用于测试的所有必要二进制文件发送到 TAEFTest1 以及所有 jpg 文件中或低于*unittests*目录。 TAEF 保留的目录层次结构。

  <strong>注意：</strong>如果指定目录不存在的目录搜索递归或非递归*等于或低于*测试目录中，所有文件将都复制到远程计算机，但将目录层次结构平展。

你可以 aso 指定测试依赖项通过[DeploymentItem 元数据](deploymentitem-metadata.md)

## <a name="user-context"></a>用户上下文 


默认情况下，TAEF 尝试使用您的用户上下文在远程计算机上运行测试。 这是通过：

-   枚举远程计算机上的所有活动会话，并寻找由您负责的会话。
    -   如果 TAEF 找到由你拥有远程计算机的会话，它运行的测试在该会话中 （在该桌面等）。

        **注意：** 这不一定是控制台会话。 这可能是远程桌面会话。

    -   如果 TAEF**找不到**你所拥有的远程计算机运行测试的用户都将记录到控制台会话 （在该桌面等） 的会话。
    -   最后，如果您不拥有远程计算机上的会话，并且没有人登录到控制台会话，TAEF 将运行测试在会话 0 中 （非交互式）。

### <a name="span-idrunasspanspan-idrunasspanspan-idrunasspanrunas"></a><span id="RunAs"></span><span id="runas"></span><span id="RUNAS"></span>RunAs

如果指定[/runAs](runas.md)值设置为除 **/runOn**，TAEF 使用除所需满足上述启发式方法 **/runAs**设置。 例如：

``` syntax
te unittests\wex.common.tests.dll /runon:TAEFTest1 /runas:system
```

-   执行 wex.common.tests.dll TAEFTest1 上使用系统帐户中存在的所有 TAEF 测试。

## <a name="span-idhowitworksspanspan-idhowitworksspanspan-idhowitworksspanhow-it-works"></a><span id="How_It_Works"></span><span id="how_it_works"></span><span id="HOW_IT_WORKS"></span>其工作原理


-   Te.exe 连接到远程计算机运行的 Te.Service 的实例
    -   Windows 身份验证 （协商） 身份验证与 Te.Service。
    -   Te.Service 授权你通过验证你管理员或远程计算机上的本地"远程 TAEF 用户"组的成员。
-   Te.Service 创建下的目录*RemoteTests*，使用与测试 dll 相同的名称。
-   Te.exe 中生成远程计算机上执行测试所需的文件的列表。 此列表包括：
    -   有必要 TAEF 二进制文件
    -   本机和/或托管二进制的所有依赖项测试 dll （不包括系统二进制文件）
    -   指定由你在任何其他文件 **/TestDependencies**参数
-   Te.exe 向 Te.Service 测试依赖项列表，以及每个文件的 Crc。
-   Te.Service 查找远程计算机上每个文件，并将 CRC 值进行比较。 从列表中，删除所有匹配项和列表发回给客户端。
-   如果有依赖关系列表中剩余的任何文件，Te.exe 向 Te.Service 发送每个依赖项。
    -   Te.Service 将其保存在&lt;Te.Service 目录&gt;\\RemoteTests\\&lt;测试 dll 名称&gt;目录。
-   Te.exe 要求以启动使用正确的远程计算机上的新 Te.ProcessHost.exe 实例 Te.Service[用户上下文](#user-context)。
-   Te.exe 连接到远程 Te.ProcessHost.exe 实例并开始执行测试。

 

 





