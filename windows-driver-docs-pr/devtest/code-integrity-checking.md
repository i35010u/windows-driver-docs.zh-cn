---
title: 代码完整性检查
description: 驱动程序验证程序的代码完整性检查
ms.assetid: ad6c4762-354d-446d-bcda-a2e99c37c589
keywords:
- 驱动程序验证程序的代码完整性检查
ms.date: 09/14/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7a1d3584df9d82f19f22716d405658c2340b011
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526380"
---
# <a name="code-integrity-checking"></a>代码完整性检查

[Device Guard](https://blogs.msdn.microsoft.com/windows_hardware_certification/2015/05/22/driver-compatibility-with-device-guard-in-windows-10/)可以使用硬件技术和虚拟化隔离的 Windows 操作系统其余部分中的代码完整性 (CI) 决策制定函数。 当使用基于虚拟化的安全隔离代码完整性，内核内存可能会变得可执行文件的唯一方法是通过代码完整性验证。 这意味着可写内容和可执行文件 (W + X) 的内核内存页面可以永远不会是不能直接修改可执行代码。 代码完整性检查确保这样的代码完整性规则，兼容性，并且检测到以下冲突：

<table>
  <tr>
    <th>错误代码</th>
    <th>代码完整性问题</th>
  </tr>
  <tr>
    <td>0x2000:
        <ul>
            <li>2-驱动程序中的地址&#39;s 代码检测到错误。</li>
            <li>3-池类型。</li>
            <li>4-池标记 （如果有的话）。</li>
        </ul><br/>    </td>
    <td>调用方指定的可执行池类型。 (预期：NonPagedPoolNx)</td>
  </tr>
  <tr>
    <td>0x2001:
        <ul><li>2-驱动程序中的地址&#39;s 代码检测到错误。</li>
        <li>3-页保护 (WIN32_PROTECTION_MASK)。
    </td>
    <td>调用方指定的一种可执行文件的页上的保护。 (预期： 清除 PAGE_EXECUTE * 位)</td>
  </tr>
  <tr>
    <td>0x2002:
        <ul><li>2-驱动程序中的地址&#39;s 代码检测到错误。</li>
            <li>3-页面优先级 (MM_PAGE_PRIORITY 逻辑上或者&#39;d MdlMapping *)。</li></ul>
    </td>
    <td>调用方指定的可执行文件的 MDL 映射。 (预期：MdlMappingNoExecute)。</td>
  </tr>
  <tr>
    <td>0x2003:
        <ul><li>2-图像文件名 （Unicode 字符串）。</li>
            <li>3-部分标头的地址。</li>
            <li>4-部分名称 （utf-8 编码字符串）。</li></ul>
    </td>
    <td>映像包含一个可执行文件和可写部分。</td>
  </tr>
  <tr>
    <td>0x2004:
        <ul><li>2-图像文件名 （Unicode 字符串）。</li>
            <li>3-部分标头的地址。</li>
            <li>4-部分名称 （utf-8 编码字符串）。</li></ul>
    </td>
    <td>映像包含一个部分，其中不对齐的页。</td>
  </tr>
  <tr>
    <td>0x2005:
        <ul><li>2-图像文件名 （Unicode 字符串）。</li>
            <li>3-IAT 目录。</li>
            <li>4-部分名称 （utf-8 编码字符串）。</li><ul>
    </td>
    <td>映像包含位于可执行文件的部分中的 IAT。</td>
  </tr>
</table>

### <a name="activating-this-option"></a>激活此选项：

您可以激活端口/微型端口接口使用驱动程序验证程序管理器或 Verifier.exe 命令行检查一个或多个驱动程序。 有关详细信息，请参阅[选择 driver verifier 选项](https://docs.microsoft.com/windows-hardware/drivers/devtest/selecting-driver-verifier-options)。 必须重新启动计算机以激活或停用检查选项的微型端口端口/接口。

* **在命令行**

    在命令行中，在由表示端口微型端口接口检查**0x02000000 (位 25)**。 例如：

    `verifier /flags 0x02000000 /driver MyDriver.sys`

    在下一次启动后，该功能将处于活动状态。

* **使用驱动程序验证程序管理器**

1. 启动驱动程序验证器管理器。 在命令提示符窗口中键入验证程序。
2. 选择创建自定义设置 （适用于代码开发人员），然后单击下一步。
3. Select(check) 端口微型端口接口检查。
4. 重新启动计算机。
