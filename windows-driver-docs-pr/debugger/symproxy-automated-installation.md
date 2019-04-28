---
title: SymProxy 自动安装
description: 下面的脚本 Install.cmd 以及这些步骤可帮助自动 SymProxy 安装到默认的 IIS 安装。
ms.assetid: 9E5433D8-D024-4E2B-AEAA-2271C133FD0E
ms.date: 03/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: 793172c6f2b0b1fda5e43be688c38b532886c25e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335478"
---
# <a name="symproxy-automated-installation"></a>SymProxy 自动安装


下面的脚本 Install.cmd 以及这些步骤可帮助自动 SymProxy 安装到默认的 IIS 安装。 您可能需要使这些步骤适应您的环境的特定需求。

1. 创建 d:\\SymStore\\符号文件夹。

   - 向所有人授予读取

   - 授予读取\\写入 SymProxy 应用程序池用户帐户 (域\\用户)

2. 共享 d:\\SymStore\\作为符号的符号。

   - 向所有人授予读取 （或更具体）

3. （可选）创建空的文件在 d： 调用 index2.txt\\SymStore\\符号。
4. （可选）创建一个空文件，名为 %WINDIR%\\system32\\inetsrv\\symsrv.yes。 它接受 EULA 以供 Microsoft 公共符号存储区。
5. 确定 Install.cmd 参数并运行它。
6. 配置在客户端符号路径中使用你创建的服务器名称。
   ```dbgcmd
   SRV*\\MachineName\Symbols*https://MachineName/Symbols
   ```

Install.cmd 脚本需要 3 个参数：

-   虚拟目录路径 (例如 d:\\SymStore\\符号)
-   用户名 （适用于应用程序池）
-   密码 （适用于应用程序池）

若要清除的 MIME 类型继承，XML 文件需要驱动器相关联的 AppCmd.exe 命令。 将 staticContentClear.xml 文件如下所示在 Install.cmd 脚本所在的同一文件夹中来实现此目标。

示例 Install.Cmd 参数的用法：

```console
Install.cmd D:\SymStore\Symbols CONTOSO\SymProxyService Pa$$word
```

## <a name="span-idinstallcmdspanspan-idinstallcmdspaninstallcmd"></a><span id="install.cmd"></span><span id="INSTALL.CMD"></span>Install.cmd


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

## <a name="span-idtestingthesymproxyinstallationspanspan-idtestingthesymproxyinstallationspanspan-idtestingthesymproxyinstallationspantesting-the-symproxy-installation"></a><span id="Testing_the_SymProxy_Installation_"></span><span id="testing_the_symproxy_installation_"></span><span id="TESTING_THE_SYMPROXY_INSTALLATION_"></span>测试 SymProxy 安装


现在应该准备好获取并提供文件系统。 若要对其进行测试，首先通过运行 iisreset.exe 重新启动 IISAdmin 服务。 这将重新加载使用当前的 IIS 和 SymProxy 配置 ISAPI 筛选器。

配置调试程序要使用此符号路径：

```dbgcmd
srv*\\MachineName\Symbols*https://MachineName/Symbols
```

如果*MissTimeout*启用 （它默认设置为 300 秒），两次运行.reload /f 命令应导致执行第二次太多速度更快。

若要查看的 Pdb 所引用的位置，请使用 lm （列出模块） 命令。 Pdb 的路径应以开头\\ \\MachineName\\符号。

如果在网站上启用了目录浏览，浏览到 https://MachineName/Symbols以查看缓存的文件。

打开性能监视器并查看符号代理计数器。

打开事件查看器并查看 Microsoft\\Windows\\SymProxy 事件。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[安装 SymProxy](installing-symproxy.md)

 

 






