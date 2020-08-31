---
title: TxtSetup.oem 文件的 Config.DriverKey 节
description: DriverKey 部分指定要在注册表中为特定组件选项设置的值。
ms.assetid: 0b9fe0ff-2b97-416e-8ced-62b59eabf94a
keywords:
- Txtsetup.oem 文件设备和驱动程序安装的 DriverKey 节
topic_type:
- apiref
api_name:
- Config.DriverKey Section of a TxtSetup.oem File
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9149246d4f8a1d20167d14527d143f373d99f1d2
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89094901"
---
# <a name="configdriverkey-section-of-a-txtsetupoem-file"></a>TxtSetup.oem 文件的 Config.DriverKey 节


**Config。**<em>DriverKey</em>部分指定要在注册表中为特定组件选项设置的值。 Windows 自动在**Services \\ **<em>DriverKey</em>项中创建所需的值。 使用此部分来指定**要在 " \\ **<em>services</em> <em>DriverKey</em> " ** \\ 和 "services**subkey_name<em>DriverKey</em>" 下** \\ **的值下创建的其他密钥 \\ *subkey_name*。

``` syntax
[Config.DriverKey]
value = subkey_name,value_name,value_type,value
...
```

<a href="" id="subkey-name"></a>*subkey_name*  
指定**服务 \\ **<em>DriverKey</em>树下的项的名称，Windows 将在其中放置指定的值。 如果该项不存在，则 Windows 将创建该项。

如果*subkey_name*为空字符串 ( "" ) ，则该值放置在<em>DriverKey</em>**服务 \\ **下。

*Subkey_name*可以指定多个级别的子项，如 "subkey1 \\ subkey2 \\ subkey3"。

<a href="" id="value-name"></a>*value_name*  
指定要设置的值的名称。

<a href="" id="value-type"></a>*value_type*  
指定注册表项的类型。 *Value_type*可以是以下项之一：

<a href="" id="reg-dword"></a>REG_DWORD  
允许使用一个 *值* ;它必须是最多包含八个十六进制数字的字符串。

例如：

``` syntax
value = parameters,NumberOfButtons,REG_DWORD,2
```

<a href="" id="reg-sz-or-reg-expand-sz"></a>REG_SZ 或 [REG_EXPAND_SZ](/windows/desktop/SysInfo/registry-value-types)  
允许使用一个 *值* ;它被解释为要存储的以 null 结尾的字符串。

例如：

``` syntax
value = parameters,Description,REG_SZ,"This is a text string"
```

<a href="" id="reg-binary"></a>REG_BINARY  
允许使用一个 *值* ;它是十六进制数字的字符串，每对都解释为一个字节值。

例如 (存储字节流00、34、ec、4d、04、5a) ：

``` syntax
value = parameters,Data,REG_BINARY,0034eC4D045a
```

<a href="" id="reg-multi-sz"></a>REG_MULTI_SZ  
允许使用多个 *值* 参数;每个被解释为 MULTI_SZ 字符串的一个组件。

例如：

``` syntax
value = parameters,Strings,REG_MULTI_SZ,String1,"String 2",string3
```

<a href="" id="value"></a>value  
指定值;其格式取决于 *value_type*。

下面的示例演示了一个 **配置。**<em>DriverKey</em> 部分：

``` syntax
; ...
[Config.OEMSCSI]
value = parameters\PnpInterface,5,REG_DWORD,1
; ...
```

 

