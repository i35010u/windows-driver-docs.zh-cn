---
title: 程序集配置文件
description: 程序集配置文件
ms.assetid: 53BAC457-BB6A-44a8-AD8D-3B621F41A245
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43e45ed79f1bb9c33ade51578d80b83751308555
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383043"
---
# <a name="assembly-config-files"></a>程序集配置文件


TAEF 支持测试程序集配置文件。 配置文件应具有与测试程序集 +".config"相同的名称。 如果具有名为的测试程序集中**MyUnitTests.dll**，你的配置文件应命名为**MyUnitTests.dll.config**。

配置文件应放置在与测试程序集文件相同的目录中。

## <a name="span-iddotnetcfspanspan-iddotnetcfspannet-configuration-files"></a><span id="dotnet_cf"></span><span id="DOTNET_CF"></span>.NET 配置文件


.NET 配置文件是采用以下形式的 XML 文件：

```cpp
<configuration>
    <appSettings>
        <add key="AssemblySetup" value="Assembly setup configuration information"/>
        <add key="ClassSetup" value="Class setup configuration information"/>
        <add key="TestSetup" value="Test setup configuration information"/>
        <add key="Test" value="Test configuration information"/>
    </appSettings>
</configuration>
```

请注意，在配置文件是一系列名称 / 值对。

## <a name="span-idreadingcfspanspan-idreadingcfspanreading-the-configuration-file-from-your-tests"></a><span id="reading_cf"></span><span id="READING_CF"></span>从你的测试中读取配置文件


可以使用**System.Configuration.ConfigurationManager**类，以从你的配置文件中读取数据。 例如，

```cpp
NameValueCollection appStgs = ConfigurationManager.AppSettings;
Log.Comment(appStgs["AssemblySetup"]);
```

 

 





