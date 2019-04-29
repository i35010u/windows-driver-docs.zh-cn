---
title: 防火墙和代理服务器
description: 防火墙和代理服务器
ms.assetid: 6b438602-299e-4cc5-ac75-ac9ee3cb50bb
keywords:
- SymSrv、 防火墙和代理服务器
- 防火墙和 SymSrv
- internet 防火墙和 SymSrv
- 代理服务器和 SymSrv
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d0105e789e4c0148c9d58cbb97c8a75deb9e95f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371675"
---
# <a name="firewalls-and-proxy-servers"></a>防火墙和代理服务器


## <span id="ddk_firewalls_and_proxy_servers_dbg"></span><span id="DDK_FIREWALLS_AND_PROXY_SERVERS_DBG"></span>


如果您使用 SymSrv 访问符号，和您计算机位于使用代理服务器的网络或符号存储区位于防火墙之外，身份验证可能需要进行数据传输。

当 SymSrv 收到身份验证请求时，调试器可以显示的身份验证请求，也可以自动拒绝该请求，具体取决于配置的方式。

SymSrv 支持集成的代理服务器。 它可以使用默认的代理服务器， [SymProxy](symproxy.md)，也可以使用所选的另一台代理服务器。

### <a name="span-idauthenticationrequestsspanspan-idauthenticationrequestsspanauthentication-requests"></a><span id="authentication_requests"></span><span id="AUTHENTICATION_REQUESTS"></span>身份验证请求

调试器可以配置为允许身份验证请求。 当防火墙或代理服务器请求授权时，将出现一个对话框。 必须将输入某种形式的信息 （通常是用户名和密码） 调试器可以下载符号之前。 如果输入不正确的信息，则将重新显示对话框。 如果选择**取消**按钮，对话框会消失，将传输没有对应符号信息。

如果将调试器配置为拒绝所有身份验证请求，没有对话框将出现，并将传输任何符号，如果需要身份验证。

如果拒绝身份验证请求，或如果调试器自动拒绝身份验证请求，将不再 SymSrv 尝试联系符号存储区。 如果你想要续订联系人，您必须重新启动调试会话，或使用[ **！ symsrv 关闭**](-symsrv.md)。

**请注意**  使用 KD 或 CDB，如果身份验证对话框中可能出现后面到打开的窗口。 如果发生这种情况，可能需要移动或最大程度减少为了查找此对话框中的某些窗口。

 

在 WinDbg 中，默认情况下允许的身份验证请求。 在 KD 和 CDB，身份验证请求，则会自动拒绝默认情况下。

若要允许身份验证请求，请使用[ **！ 符号提示**](-sym.md)或[ **.symopt 0x80000**](-symopt--set-symbol-options-.md)。 若要拒绝所有请求，使用 **！ 关闭提示符号**或 **.symopt + 0x80000**。 若要显示的当前设置，请使用 **！ 符号**。

必须使用[ **.reload （重新加载模块）** ](-reload--reload-module-.md)后对身份验证权限状态进行任何更改。

### <a name="span-idchoosingaproxyserverspanspan-idchoosingaproxyserverspanchoosing-a-proxy-server"></a><span id="choosing_a_proxy_server"></span><span id="CHOOSING_A_PROXY_SERVER"></span>选择代理服务器

若要为 Windows 选择默认代理服务器，打开**Internet 选项**控制面板中，选择**连接**选项卡，然后选择**LAN 设置**按钮。 然后可以输入代理服务器名称和端口号，或选择**高级**配置多个代理服务器。 有关更多详细信息，请参阅 Internet Explorer 的帮助文件。

若要选择用于 symsrv 若要使用的特定代理服务器，设置\_NT\_符号\_代理环境变量相同的名称或 IP 的代理服务器后, 跟冒号和端口号。 例如：

```console
set _NT_SYMBOL_PROXY=myproxyserver:80
```

当以这种方式选择的代理服务器，则任何使用 SymSrv 访问符号服务器的 Windows 调试器将使用它。 它还将使用由任何其他使用 DbgHelp 作为其符号的处理程序的调试工具。 其他程序没有将受此设置。

 

 





