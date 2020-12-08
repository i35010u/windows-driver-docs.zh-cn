---
title: 代码完整性检查
description: 驱动程序验证程序的代码完整性检查
keywords:
- 驱动程序验证程序的代码完整性检查
ms.date: 09/14/2017
ms.localizationpriority: medium
ms.openlocfilehash: 723fcb96c49def910f60b24a9411b8a31d958260
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795095"
---
# <a name="code-integrity-checking"></a>代码完整性检查

[受虚拟机监控程序保护的代码完整性](/windows/security/threat-protection/device-guard/enable-virtualization-based-protection-of-code-integrity) 可以使用硬件技术和虚拟化将代码完整性与 Windows 操作系统的其余部分 (CI) 决策功能。 使用基于虚拟化的安全性来隔离代码完整性时，内核内存可执行的唯一方式是通过代码完整性验证。 这意味着内核内存页永远不能为可写的，并且可执行 (W + X) 并且可执行代码不能直接修改。 代码完整性检查确保这些代码完整性规则的兼容性，并检测以下冲突：

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
            <li>4-如果提供) ，则为 (池标记。</li>
        </ul><br/>    </td>
    <td>调用方指定了可执行的池类型。 需要 (： NonPagedPoolNx) </td>
  </tr>
  <tr>
    <td>0x2001:
        <ul><li>2-驱动程序代码中检测到错误的地址。</li>
        <li>3页保护 (WIN32_PROTECTION_MASK) 。
    </td>
    <td>调用方指定了可执行页保护。 应 (：已清除 PAGE_EXECUTE * 位) </td>
  </tr>
  <tr>
    <td>0x2002:
        <ul><li>2-驱动程序代码中检测到错误的地址。</li>
            <li>3- (MM_PAGE_PRIORITY 逻辑或对 MdlMapping * ) 的页优先级。</li></ul>
    </td>
    <td>调用方指定了可执行的 MDL 映射。 需要 (： MdlMappingNoExecute) 。</td>
  </tr>
  <tr>
    <td>0x2003:
        <ul><li>2- (Unicode string) 的图像文件名。</li>
            <li>3-节标头的地址。</li>
            <li>4-节名称 (UTF-8 编码字符串) 。</li></ul>
    </td>
    <td>映像包含可执行文件和可写部分。</td>
  </tr>
  <tr>
    <td>0x2004:
        <ul><li>2- (Unicode string) 的图像文件名。</li>
            <li>3-节标头的地址。</li>
            <li>4-节名称 (UTF-8 编码字符串) 。</li></ul>
    </td>
    <td>图像包含不是页面对齐的部分。</td>
  </tr>
  <tr>
    <td>0x2005:
        <ul><li>2- (Unicode string) 的图像文件名。</li>
            <li>3-IAT 目录。</li>
            <li>4-节名称 (UTF-8 编码字符串) 。</li><ul>
    </td>
    <td>此图像包含位于可执行部分中的 IAT。</td>
  </tr>
</table>

### <a name="activating-this-option"></a>激活此选项：

您可以使用驱动程序验证器管理器或 Verifier.exe 命令行为一个或多个驱动程序激活代码完整性检查。 有关详细信息，请参阅 [选择驱动程序验证程序选项](./selecting-driver-verifier-options.md)。 您必须重新启动计算机以激活或停用代码完整性检查选项。

* **在命令行中**

    在命令行中，代码完整性检查由 **0x02000000 (位 25)** 表示。 例如：

    `verifier /flags 0x02000000 /driver MyDriver.sys`

    此功能将在下一次启动后处于活动状态。

* **使用驱动程序验证器管理器**

1. 启动驱动程序验证器管理器。 在命令提示符窗口中键入 Verifier。
2. 选择 "为代码开发人员 (创建自定义设置") ，然后单击 "下一步"。
3. 选择 (检查) 代码完整性检查。
4. 重新启动计算机。

## <a name="related-topics"></a>相关主题

[评估 HVCI 驱动程序兼容性](../driversecurity/use-device-guard-readiness-tool.md)
