---
title: SymProxy 自动安装
description: 这些步骤与下面的 Install .cmd 脚本一起使用有助于自动将 SymProxy 安装到默认的 IIS 安装。
ms.date: 03/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: 17cc269d94d8656b927a1c4dcac6b711de1a7000
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822591"
---
# <a name="symproxy-automated-installation"></a>SymProxy 自动安装


这些步骤与下面的 Install .cmd 脚本一起使用有助于自动将 SymProxy 安装到默认的 IIS 安装。 你可能需要将这些步骤调整为你的环境的特定需求。

1. Create D： \\ SymStore \\ 符号文件夹。

   - 向所有人授予读取权限

   - 向 \\ SymProxy 应用程序池用户帐户授予对 (域 \\ 用户) 的读取写入权限

2. 共享 D： \\ SymStore \\ 符号作为符号。

   - 授予每个人 (或更具体) 的读取权限

3.  (可以选择) 在 D： SymStore 符号中创建名为 index2.txt 的空文件 \\ \\ 。
4.  (选择 ") 创建名为% WINDIR% \\ system32 \\ inetsrv \\ symsrv 的空文件。 这会接受 Microsoft 公共符号存储的 EULA。
5. 确定 cmd.exe 的参数并运行它。
6. 使用你创建的服务器名称配置客户端符号路径。
   ```dbgcmd
   SRV*\\MachineName\Symbols*https://MachineName/Symbols
   ```

安装 .cmd 脚本需要3个参数：

-   虚拟目录路径 (例如 D： \\ SymStore \\ 符号 ) 
-   应用程序池) 的用户名 (
-   应用程序池) 的密码 (

若要清除 MIME 类型继承，需要使用 XML 文件来驱动关联的 AppCmd.exe 命令。 将下面显示的 staticContentClear.xml 文件放在安装 .cmd 脚本所在的同一文件夹中，以实现此结果。

示例安装 .Cmd 参数用法：

```console
Install.cmd D:\SymStore\Symbols CONTOSO\SymProxyService Pa$$word
```

## <a name="span-idinstallcmdspanspan-idinstallcmdspaninstallcmd"></a><span id="install.cmd"></span><span id="INSTALL.CMD"></span>安装 .cmd


```bat
@echo off

SET VirDirectory=%1
SET UserName=%2
SET Password=%3

::
::  SymProxy dll installation. 
::

copy symproxy.dll %windir%\system32\inetsrv
copy symproxy.man %windir%\system32\inetsrv
copy symsrv.dll %windir%\system32\inetsrv

lodctr.exe /m:%windir%\system32\inetsrv\symproxy.man
wevtutil.exe install-manifest %windir%\System32\inetsrv\symproxy.man
regedit.exe /s symproxy.reg

::
::  Web server Configuraiton
::

IF not exist %VirDirectory% mkdir %VirDirectory%

rem Make the 'Default Web Site'
%windir%\system32\inetsrv\appcmd.exe add site -site.name:"Default Web Site" -bindings:"http/*:80:" -physicalPath:C:\inetpub\wwwroot

rem Enabled Directory Browsing on the 'Default Web Site'
%windir%\system32\inetsrv\appcmd.exe set config "Default Web Site" -section:system.webServer/directoryBrowse /enabled:"True"

rem Make the 'SymProxy App Pool'
%windir%\system32\inetsrv\appcmd.exe add apppool -apppool.name:SymProxyAppPool -managedRuntimeVersion:
%windir%\system32\inetsrv\appcmd.exe set apppool -apppool.name:SymProxyAppPool -processModel.identityType:SpecificUser -processModel.userName:%UserName% -processModel.password:%Password% 

rem Make the 'Symbols' Virtual Directory and assign the 'SymProxy App Pool'
%windir%\system32\inetsrv\appcmd.exe add app -site.name:"Default Web Site" -path:/Symbols -physicalpath:%VirDirectory%
%windir%\system32\inetsrv\appcmd.exe set app -app.name:"Default Web Site/Symbols" -applicationPool:SymProxyAppPool

rem Disable 'web.config' for folders under virtual directories in the 'Default Web Site'
%windir%\system32\inetsrv\appcmd.exe set config -section:system.applicationHost/sites "/[name='Default Web Site'].virtualDirectoryDefaults.allowSubDirConfig:false

rem Add the 'SymProxy ISAPI Filter'
%windir%\system32\inetsrv\appcmd.exe set config -section:system.webServer/isapiFilters /+"[name='SymProxy',path='%windir%\system32\inetsrv\SymProxy.dll',enabled='True']

rem Clear the MIME Types on the 'Default Web Site'
%windir%\system32\inetsrv\appcmd.exe set config -in "Default Web Site" < staticContentClear.xml

rem Add * to the MIME Types of the 'Default Web Site'
%windir%\system32\inetsrv\appcmd.exe set config "Default Web Site" -section:staticContent /+"[fileExtension='.*',mimeType='application/octet-stream']"
```

## <a name="span-idstaticcontentclearxmlspanspan-idstaticcontentclearxmlspanstaticcontentclearxml"></a><span id="staticcontentclear.xml"></span><span id="STATICCONTENTCLEAR.XML"></span>staticContentClear.xml


```xml
<?xml version="1.0" encoding="UTF-8"?>
<appcmd>
    <CONFIG CONFIG.SECTION="system.webServer/staticContent"                  path="MACHINE/WEBROOT/APPHOST">
        <system.webServer-staticContent>
            <clear />
        </system.webServer-staticContent>
    </CONFIG>
</appcmd>    
```

## <a name="span-idtesting_the_symproxy_installation_spanspan-idtesting_the_symproxy_installation_spanspan-idtesting_the_symproxy_installation_spantesting-the-symproxy-installation"></a><span id="Testing_the_SymProxy_Installation_"></span><span id="testing_the_symproxy_installation_"></span><span id="TESTING_THE_SYMPROXY_INSTALLATION_"></span>测试 SymProxy 安装


系统现在应准备好获取并提供文件。 若要对其进行测试，请先通过运行 iisreset.exe 来重新启动 IISAdmin 服务。 这会将 ISAPI 筛选器重载为当前 IIS 和 SymProxy 配置。

将调试器配置为使用此符号路径：

```dbgcmd
srv*\\MachineName\Symbols*https://MachineName/Symbols
```

如果启用了 *MissTimeout* (默认情况下将其设置为300秒) ，运行. reload.sql/f 命令两次应该导致第二次执行速度快得多。

若要查看所引用 Pdb 的位置，请使用 "lm (list" 模块) 命令。 Pdb 的路径应以 \\ \\ MachineName \\ 符号开头。

如果在网站上启用了目录浏览，请浏览到 https://MachineName/Symbols 以查看缓存的文件。

打开性能监视器并查看符号代理计数器。

打开事件查看器并查看 Microsoft \\ Windows \\ SymProxy 事件。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[安装 SymProxy](installing-symproxy.md)

 

 






