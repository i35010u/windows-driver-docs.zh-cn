---
title: 程序集配置文件
description: 程序集配置文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b268b928f4dcc92bd4752a092d907d9d3d4b1170
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819927"
---
# <a name="assembly-config-files"></a>程序集配置文件


TAEF 支持测试程序集配置文件。 配置文件的名称应与你的测试程序集 + ".config" 的名称相同。 如果有一个名为 **MyUnitTests.dll** 的测试程序集，则配置文件应命名为 **MyUnitTests.dll.config**。

应将配置文件放置在测试程序集文件所在的同一目录中。

## <a name="span-iddotnet_cfspanspan-iddotnet_cfspannet-configuration-files"></a><span id="dotnet_cf"></span><span id="DOTNET_CF"></span>.NET 配置文件


.NET 配置文件采用以下形式：

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

请注意，配置文件是名称/值对的集合。

## <a name="span-idreading_cfspanspan-idreading_cfspanreading-the-configuration-file-from-your-tests"></a><span id="reading_cf"></span><span id="READING_CF"></span>从测试中读取配置文件


可以使用 **System.Configuration.ConfigurationManager** 类从配置文件中读取数据。 例如，

```cs
NameValueCollection appStgs = ConfigurationManager.AppSettings;
Log.Comment(appStgs["AssemblySetup"]);
```

 

 





