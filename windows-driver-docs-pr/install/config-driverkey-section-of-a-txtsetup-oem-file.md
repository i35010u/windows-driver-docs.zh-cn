---
title: Config.DriverKey TxtSetup.oem 文件的节
description: Config.DriverKey 部分指定要为特定组件选项的注册表中设置值。
ms.assetid: 0b9fe0ff-2b97-416e-8ced-62b59eabf94a
keywords:
- Config.DriverKey 部分中的 TxtSetup.oem 文件的设备和驱动程序安装
topic_type:
- apiref
api_name:
- Config.DriverKey Section of a TxtSetup.oem File
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cf88e4b0b1fe90c0d951b7f1a4f4bff37dc3ce12
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543769"
---
# <a name="configdriverkey-section-of-a-txtsetupoem-file"></a>Config.DriverKey TxtSetup.oem 文件的节


一个**配置。**<em>DriverKey</em>部分指定要为特定组件选项的注册表中设置值。 Windows 会自动创建所需的值中**Services\\**<em>DriverKey</em>密钥。 使用本部分中指定其他密钥，从而下创建**Services\\**<em>DriverKey</em>和值下**Services\\**  <em>DriverKey</em>并**服务\\**<em>DriverKey</em>\\*subkey_name*。

``` syntax
[Config.DriverKey]
value = subkey_name,value_name,value_type,value
...
```

<a href="" id="subkey-name"></a>*subkey_name*  
指定的名称下的项**Services\\**<em>DriverKey</em>树 Windows 放置指定的值的位置。 如果不存在，则 Windows 创建的密钥。

如果*subkey_name*是空字符串 ("")，值置于下**Services\\**<em>DriverKey</em>。

*Subkey_name*可以指定多个级别子项，如"subkey1\\subkey2\\subkey3"。

<a href="" id="value-name"></a>*value_name*  
指定要设置的值的名称。

<a href="" id="value-type"></a>*value_type*  
指定注册表项的类型。 *Value_type*可以是以下之一：

<a href="" id="reg-dword"></a>REG_DWORD  
一个*值*允许; 它必须是包含最多八个十六进制数字的字符串。

例如：

``` syntax
value = parameters,NumberOfButtons,REG_DWORD,2
```

<a href="" id="reg-sz-or-reg-expand-sz"></a>REG_SZ 或[REG_EXPAND_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)  
一个*值*允许它被解释为要存储的以 null 结尾的字符串。

例如：

``` syntax
value = parameters,Description,REG_SZ,"This is a text string"
```

<a href="" id="reg-binary"></a>REG_BINARY  
一个*值*允许; 它是一个字符串的十六进制数字，其中每个对会解释为一个字节值。

例如 (存储字节流 00,34、 ec、 4 d 04，5a):

``` syntax
value = parameters,Data,REG_BINARY,0034eC4D045a
```

<a href="" id="reg-multi-sz"></a>REG_MULTI_SZ  
多个*值*允许使用参数; 每个被解释为 MULTI_SZ 字符串的一个组件。

例如：

``` syntax
value = parameters,Strings,REG_MULTI_SZ,String1,"String 2",string3
```

<a href="" id="value"></a>*value*  
指定的值;其格式取决于*value_type*。

下面的示例演示**配置。**<em>DriverKey</em>部分：

``` syntax
; ...
[Config.OEMSCSI]
value = parameters\PnpInterface,5,REG_DWORD,1
; ...
```

 

 





