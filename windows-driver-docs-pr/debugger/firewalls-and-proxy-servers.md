---
title: 防火墙和代理服务器
description: 防火墙和代理服务器
keywords:
- SymSrv、防火墙和代理服务器
- 防火墙和 SymSrv
- internet 防火墙和 SymSrv
- 代理服务器和 SymSrv
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6a6056150458fa99bc462eca443b25efe558bec
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838185"
---
# <a name="firewalls-and-proxy-servers"></a>防火墙和代理服务器


## <span id="ddk_firewalls_and_proxy_servers_dbg"></span><span id="DDK_FIREWALLS_AND_PROXY_SERVERS_DBG"></span>


如果使用 SymSrv 来访问符号，并且计算机位于使用代理服务器的网络上，或者符号存储位于防火墙外部，则可能需要进行身份验证才能进行数据传输。

当 SymSrv 接收到身份验证请求时，调试器可以显示身份验证请求，或根据配置方式自动拒绝请求。

SymSrv 已集成对代理服务器的支持。 它可以使用默认代理服务器 [SymProxy](symproxy.md)，也可以使用所选的另一台代理服务器。

### <a name="span-idauthentication_requestsspanspan-idauthentication_requestsspanauthentication-requests"></a><span id="authentication_requests"></span><span id="AUTHENTICATION_REQUESTS"></span>身份验证请求

可以将调试器配置为允许身份验证请求。 当防火墙或代理服务器请求授权时，将出现一个对话框。 在调试器可下载符号之前，必须 (通常输入一些信息) 用户名和密码。 如果输入的信息不正确，则将重新显示该对话框。 如果选择 " **取消** " 按钮，则对话框将消失，且不会传输任何符号信息。

如果将调试器配置为拒绝所有身份验证请求，则不会显示任何对话框，并且如果需要身份验证，则不会传输任何符号。

如果拒绝身份验证请求，或者如果调试器自动拒绝身份验证请求，则 SymSrv 将不会再进一步联系到符号存储区。 如果要续订 contact，必须重新启动调试会话或使用 [**！ symsrv close**](-symsrv.md)。

**注意**   如果使用的是 KD 或 CDB，则 "身份验证" 对话框可能会出现在打开的窗口之后。 如果出现这种情况，则可能需要移动或最小化某些窗口才能找到此对话框。

 

在 WinDbg 中，默认情况下允许身份验证请求。 默认情况下，在 KD 和 CDB 中，默认情况下会自动拒绝身份验证请求。

若要允许身份验证请求，请使用 [**！符号提示**](-sym.md) 或 [**. symopt-0x80000**](-symopt--set-symbol-options-.md)。 若要拒绝所有请求，请使用 **！符号提示符** **symopt + 0x80000**。 若要显示当前设置，请使用 **！符号**。

在对身份验证权限状态进行任何更改之后，必须使用 [**. reload.sql (重载模块)**](-reload--reload-module-.md) 。

### <a name="span-idchoosing_a_proxy_serverspanspan-idchoosing_a_proxy_serverspanchoosing-a-proxy-server"></a><span id="choosing_a_proxy_server"></span><span id="CHOOSING_A_PROXY_SERVER"></span>选择代理服务器

若要为 Windows 选择默认的代理服务器，请在 "控制面板" 中打开 " **Internet 选项** "，选择 " **连接** " 选项卡，然后选择 " **LAN 设置** " 按钮。 然后，你可以输入代理服务器名称和端口号，或选择 " **高级** " 来配置多个代理服务器。 有关更多详细信息，请参阅 Internet Explorer 的帮助文件。

若要选择要使用的特定代理服务器 symsrv，请将 \_ NT \_ SYMBOL \_ proxy 环境变量设置为与代理服务器的名称或 IP 相同，后跟一个冒号和端口号。 例如：

```console
set _NT_SYMBOL_PROXY=myproxyserver:80
```

如果以这种方式选择代理服务器，则任何使用 SymSrv 的 Windows 调试器都将使用该代理服务器来访问符号服务器。 任何其他使用 Dbghelp.dll 作为其符号处理程序的调试工具也将使用它。 此设置不会影响任何其他程序。

 

 





