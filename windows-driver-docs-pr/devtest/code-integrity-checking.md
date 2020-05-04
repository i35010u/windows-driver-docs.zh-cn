---
title: 代码完整性检查
description: 驱动程序验证程序的代码完整性检查
ms.assetid: ad6c4762-354d-446d-bcda-a2e99c37c589
keywords:
- 驱动程序验证程序的代码完整性检查
ms.date: 09/14/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d0048d134d47f30896ed17546cbcad7c7c862ba
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "82104605"
---
# <a name="code-integrity-checking"></a>代码完整性检查

[Device Guard](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/bg-p/WindowsHardwareCertification)可以使用硬件技术和虚拟化将代码完整性（CI）决策功能与 Windows 操作系统的其余部分隔离开来。 使用基于虚拟化的安全性来隔离代码完整性时，内核内存可执行的唯一方式是通过代码完整性验证。 这意味着内核内存页永远不能为可写且可执行（W + X）和可执行代码不能直接修改。 代码完整性检查确保这些代码完整性规则的兼容性，并检测以下冲突：

<table>
  <tr>
    <th>错误代码</th>
    <th>代码完整性问题</th>
  </tr>
  <tr>
    <td>0x2000
        <ul>
            <li>2-驱动程序代码中检测到错误的地址。</li>
            <li>3-池类型。</li>
            <li>4-池标记（如果已提供）。</li>
        </ul><br/>    </td>
    <td>调用方指定了可执行的池类型。 （应为： NonPagedPoolNx）</td>
  </tr>
  <tr>
    <td>0x2001:
        <ul><li>2-驱动程序代码中检测到错误的地址。</li>
        <li>3页保护（WIN32_PROTECTION_MASK）。
    </td>
    <td>调用方指定了可执行页保护。 （应为：已清除 PAGE_EXECUTE * 位）</td>
  </tr>
  <tr>
    <td>0x2002:
        <ul><li>2-驱动程序代码中检测到错误的地址。</li>
            <li>3页优先级（MM_PAGE_PRIORITY 逻辑或在 MdlMapping * 上）。</li></ul>
    </td>
    <td>调用方指定了可执行的 MDL 映射。 （应为： MdlMappingNoExecute）。</td>
  </tr>
  <tr>
    <td>0x2003:
        <ul><li>2-图像文件名（Unicode 字符串）。</li>
            <li>3-节标头的地址。</li>
            <li>4-节名称（UTF-8 编码的字符串）。</li></ul>
    </td>
    <td>映像包含可执行文件和可写部分。</td>
  </tr>
  <tr>
    <td>0x2004:
        <ul><li>2-图像文件名（Unicode 字符串）。</li>
            <li>3-节标头的地址。</li>
            <li>4-节名称（UTF-8 编码的字符串）。</li></ul>
    </td>
    <td>图像包含不是页面对齐的部分。</td>
  </tr>
  <tr>
    <td>0x2005:
        <ul><li>2-图像文件名（Unicode 字符串）。</li>
            <li>3-IAT 目录。</li>
            <li>4-节名称（UTF-8 编码的字符串）。</li><ul>
    </td>
    <td>此图像包含位于可执行部分中的 IAT。</td>
  </tr>
</table>

### <a name="activating-this-option"></a>激活此选项：

您可以使用驱动程序验证器管理器或 Verifier 命令行为一个或多个驱动程序激活代码完整性检查。 有关详细信息，请参阅[选择驱动程序验证程序选项](https://docs.microsoft.com/windows-hardware/drivers/devtest/selecting-driver-verifier-options)。 您必须重新启动计算机以激活或停用代码完整性检查选项。

* **在命令行中**

    在命令行中，代码完整性检查由**0x02000000 （第25位）** 表示。 例如：

    `verifier /flags 0x02000000 /driver MyDriver.sys`

    此功能将在下一次启动后处于活动状态。

* **使用驱动程序验证器管理器**

1. 启动驱动程序验证器管理器。 在命令提示符窗口中键入 Verifier。
2. 选择 "创建自定义设置（对于代码开发人员）"，然后单击 "下一步"。
3. 选择（检查）代码完整性检查。
4. 重新启动计算机。
