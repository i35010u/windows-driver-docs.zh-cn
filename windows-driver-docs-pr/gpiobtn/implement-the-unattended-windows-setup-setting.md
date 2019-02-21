---
title: 实现的无人参与的 Windows 安装程序设置
description: 本主题介绍如何设置无人参与的 Windows 安装程序组件设置。
ms.assetid: 593F8E05-F886-45FE-83EB-8DDD204F7900
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 392db897c42d4a96d02874f84e0a54e286a8ca12
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544153"
---
# <a name="implement-the-unattended-windows-setup-setting"></a>实现的无人参与的 Windows 安装程序设置


本主题介绍如何设置无人参与的 Windows 安装程序组件设置。

我们强烈建议你使用[Windows 系统映像管理器](https://go.microsoft.com/fwlink/p/?linkid=324691)编辑无人参与的 Windows 安装程序文件。

下面是示例输出文件：

``` syntax
<unattend xmlns="urn:schemas-microsoft-com:unattend">
  <settings pass="specialize">
    <component
        name="Microsoft-Windows-GPIOButtons"
        processorArchitecture="x86"> <!-- ... Additional component attributes-->
      <ConvertibleSlateMode>1</ConvertibleSlateMode> <!-- Values: {0 (slate); 1 (laptop)}-->
    </component>
  </settings>
</unattend>
```

 

 




